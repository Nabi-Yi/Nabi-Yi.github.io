---
title: "Hashing"

categories:
  - Security
tags:
  - Hashing
---
### Hashing
- 어떠한 문자열에 **임의의 연산 알고리즘**을 적용하여 다른 문자열로 변환하는 것
- Client - Server - DB에서. DB에 저장 할 때 해싱하여 저장하면 데이터가 탈취되어도 좀 낫다.
- DB에 password와 같은 민감한 정보를 저장할 때 이용한다.
- 해시 값을 계산하는데(encoding) 오래 걸리지 않아야 한다.
- 중복 해시 값을 최대한 피해야 하며, 모든 값은 고유한 해시 값을 가진다.
- 아주 작은 단위의 변경이라도 완전히 다른 해시 값을 가져야 한다.
- SHA1 , SHA256

### Salt
- 일정한 알고리즘을 이용할 때, 해당 알고리즘을 통한 해시 값은 항상 같음
- 때문에 기존 문자열에 Salt값을 추가 한 후 Hashing하여 더 예상하기 힘든 해시 값을 생성
- Password에 Salt를 추가할 때, 각 유저와 패스워드 별로 Unique한 값을 가져야 한다.
- 비밀번호를 변경 할 때 마다 새로운 임의의 Salt를 사용해야 한다.(재사용 절대 불가)
- Salt가 DB의 유저 테이블에 함께 저장되어야 한다.

### Process
- 회원가입 시 password + salt의 해시 값을 DB의 유저테이블에 저장. Salt도 따로 저장.
- Client가 ID와 Password를 Server에 전송
- Server는 해당 ID에 대한 인증정보를 DB에 요청
- Server에서 password와 받은 salt값을 가지고 생성된 해시 값을 DB에서 받은 해시 값과 비교 하여 인증
- 


### 참조 및 더 읽어볼 거리
- 레인보우 테이블
- SHA1
- SHA256

