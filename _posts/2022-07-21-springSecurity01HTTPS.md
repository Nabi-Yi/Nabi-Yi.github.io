---
title: "HTTPS"

categories:
  - Security
tags:
  - HTTPS
---
### HTTPS
- HTTP + Secure(Socket Layer)
- = HTTP over SSL(TLS)
- 기존 HTTP protocol에 암호화를 걸어 중간 탈취가 일어나더라도 Key가 없으면 해독불가  

### Certificate(인증서)
- 데이터를 제공한 서버가 맞는지 확인
- 인증서에 도메인 정보가 종속. 인증 용이
- 데이터 요청시 서버는 인증서와 함께 응답을 전송
- 클라이언트는 인증서에 작성된 Domain과 응답의 Domain을 비교
- 해커에 의한 탈취가 발생하면 응답의 Domain이 변경되어 데이터 오염을 감지할 수 있음

### CA
- Certificate Authority. 인증서 발급기관
- OS 혹은 브라우저 별로 각기 신뢰할만한 CA 리스트를 이용함.

### 비대칭 키 & 대칭 키
- 키 A로 Encoding -> 키 B로 Decoding
- 공개 키(Public Key)와 암호 키(개인키, private Key)(비대칭 키 방식)
- 비대칭 키 방식은 부담이 커 통신 초기(Hand Shaking)에 대칭 키 생성 용도로 사용
- 이렇게 생성된 임의의 랜덤 스트링에 의해 Session Key 생성
- Session Key로 암호화 된 메시지를 서로 Encoding Decoding해서 검증되면 연결 성립


### 참조 및 더 읽어볼 거리
- <https://en.wikipedia.org/wiki/Man-in-the-middle_attack>



