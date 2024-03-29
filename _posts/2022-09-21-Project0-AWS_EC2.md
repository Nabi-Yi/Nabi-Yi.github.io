---
title: "프로젝트 :  AWS EC2 구성"

categories:
- Project
tags:
- CI/CD
- EC2
---
### AWS EC2
- 프로젝트를 본격적으로 진행하기 앞서 차후 웹 서버의 배포 및 개발 단계에서 프론트분들이 테스트 하실 수 있도록 간단한 배포 환경을 구성해놓고자 했다.    
이러한 자그마한 프로젝트에 쓰기 좋은 [AWS BeanStalk](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/Welcome.html)이라는 훌륭한 프로비져닝 서비스가 있지만.. 일단은 깡으로 EC2를 구성을 해보자는 욕심으로 하나씩 직접 차근차근 붙여나가고자 한다.    

- EC2 자체에 대한 설명보다는 구축 방법, 진행순서 등을 위주로 글을 작성했다. EC2자체에 대한 설명은 [공식문서](https://docs.aws.amazon.com/ec2/)를 참고해보자.

### AWS IAM
- 본격적으로 EC2를 이용하기 전에, 해야할 것이 있는데 IAM설정을 해주고 IAM계정을 이용하는 것이 좋다. IAM계정은 ROOT계정이 아닌 ROOT계정에서 설정한 일부 서비스에만 접근 가능한 루트계정에 종속된 새끼계정으로 봐도 무방할 것 같다. 이러한 IAM계정을 이용하는 이유는 ROOT계정이 털릴 위험을 최소화하고, 특히 혼자가 아닌 팀이 하나의 ROOT계정 아래서 여러 서비스를 이용 할 때 각각에 맞는 IAM계정을 부여하고 사용함으로써 좀 더 안전하게 서비스를 이용하기 위함을 주 목적으로 생각한다. AWS측에서도 루트계정의 로그인은 최소화하고 대부분의 서비스는 IAM계정을 통해 이용하길 권장하고 있다.  

1.먼저 AWS 가입 후, ROOT 계정으로 로그인한 뒤 상단의 IAM에서 IAM 서비스를 검색하자  
 ![image](https://user-images.githubusercontent.com/104179624/191491677-3db30ded-e10e-4481-8806-c2006be6d974.png)  
2. IAM 콘솔에 들어가면, 왼쪽 탭의 사용자 그룹탭을 들어가 그룹 생성을 클릭.  
이번 프로젝트에는 프론트 2명, 백엔드 2명의 팀원으로 진행되므로 총 4개의 IAM계정을 만들 것인데, 이를 프론트 그룹과 백엔드 그룹으로 나눠 2개의 그룹을 만들 예정이다.   
![image](https://user-images.githubusercontent.com/104179624/191493325-d186defb-2b06-41a1-b357-dca0d0df7300.png)  
3. 적당한 이름을 설정해주고, 권한 설정을 해주자. 백엔드는 서버가 돌아갈 EC2에 대한 권한(EC2FullAccess)와 RDS를 이용할 생각이라면 (RDSFULLACCESS)까지 추가해주자.  
이후 그룹 생성을 클릭하여 마무리.
![image](https://user-images.githubusercontent.com/104179624/191499973-fbd9a9a6-0080-4198-ac87-637ee593ceff.png)   

4. 실질적인 사용자를 추가해보자. 방법은 거의 같다. 왼쪽탭의 사용자 탭을 클릭 후 사용자 추가를 클릭.  
5. 사용자 이름을 입력하고, 엑세스 키와 암호 방식 모두 체크 후에 비밀번호는 자동생성해도 되고, 직접 입력해도 되지만 본인은 자동생성한 키를 사용하기로 했다.    
![image](https://user-images.githubusercontent.com/104179624/191500501-ac7be563-c156-43eb-92c8-13bb9ec476e4.png)  
6. 다음:권한을 눌러 넘어가면, 권한 설정을 할 수 있다. 우리는 이미 그룹을 만들어놨으므로, 백엔드 그룹에 추가해주자. 혹은 기존 정책 직접 연결을 통해 그룹 생성시와 동일하게 권한을 찾아 설정 해 줄 수도 있다.  
![image](https://user-images.githubusercontent.com/104179624/191500585-ff618aaf-f925-432c-b964-7153d530a4af.png)  
7. 태그로 넘어가면, 태그를 설정 할 수 있는데, 태그를 설정하면 이후에 요금 추적 등에 좀 더 용이하다고 한다. 당장은 쓸 일이 없으므로 패스하도 무방하다.
8. 검토 후 생성
9. 생성이 완료되면, 다음과 같이 엑세스 키와 자동생성된(혹은 직접 입력한 비밀번호)가 있는데, .csv다운로드를 통해 저장해두는 것이 좋다. 다른 팀원에게 로그인 정보를 전달할 때는 이메일 전송을 통해 전달 해주자.
![image](https://user-images.githubusercontent.com/104179624/191501565-7c9728f0-3ba5-4b83-8494-0bac1cdbcfa4.png)  
11. 이 후 IAM계정으로 로그인하기 위해선 위 이미지의 https://{AWSIDNUMBER}/signin.aws.amazon.com/console 을 통해 로그인 할 수 있다.

### AWS EC2
1. 
![image](https://user-images.githubusercontent.com/104179624/191506865-cd512a68-89da-4220-bf7d-6f212fb20c98.png)
2. 
![image](https://user-images.githubusercontent.com/104179624/191507138-8d470955-a56e-4d6a-a73c-837f5c5c4640.png)
3. 
![image](https://user-images.githubusercontent.com/104179624/191507707-190d66ea-16fe-49cb-85fe-1ddce9bee553.png)
4. 
![image](https://user-images.githubusercontent.com/104179624/191507774-24768bd3-f076-4423-8611-ee9480656449.png)


### 참조 및 더 읽어볼 거리
- 
