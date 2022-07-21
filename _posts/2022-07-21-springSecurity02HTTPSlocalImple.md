---
title: "로컬환경에서 HTTPS 구현해보기"

categories:
  - Security
tags:
  - HTTPS
---
### 사설 HTTPS Cert 만들기
- JAVA(Spring)에서는 PKCS12와 JKS를 지원
- 로컬환경에서는 실제 CA를 이용하기 위험하거나 불가능함.
- mkcert를 이용해 PKCS12형식으로 로컬환경 구현해보기.
- Ubuntu에서 mkcert 설치하기
```
$ sudo apt install libnss3-tools
$ wget -O mkcert https://github.com/FiloSottile/mkcert/releases/download/v1.4.3/mkcert-v1.4.3-linux-amd64
$ chmod +x mkcert
$ sudo cp mkcert /usr/local/bin/
```
- 로컬을 인증된 발급기관으로 추가하고 인증서 생성하기
```
$ mkcert -install
$ mkcert -pkcs12 localhost
```
- localhost에 대해 발급된 인증서가 저장된다. 특정 url을 입력하고 싶으면 추가로 입력해주면 된다.
- 윈도우 탐색기에 \\wsl$ 을 통해 리눅스 폴더에 접근하거나, ubuntu에서 /mnt를 통해 윈도우 폴더에 접근하여 Spring project내에 resource폴더에 생성된 인증서를 복사해준다.
- 설정파일에 ssl정보를 입력해준다.
  - application.properties
  ```
  server.ssl.key-store=classpath:localhost.p12    
  server.ssl.key-store-type=PKCS12                
  server.ssl.key-store-password=changeit          
  ``` 
  - application.yml
  ```
  server:
    ssl:
      key-store: classpath:localhost.p12
      key-store-type: PKCS12
      key-store-password: changeit
  ```


### 참조 및 더 읽어볼 거리
- <https://isgb.otago.ac.nz/infosci/mark.george/Wiki/wiki/mkcert%20and%20CA%20certificates>
- <https://github.com/FiloSottile/mkcert>


