---
title: "(참고) OSI Model"

categories:
  - Network
tags:
  - OSI Model
---
### OSI Model 이란?
[이전 포스팅](https://nabi-yi.github.io/network/network01HTTP/) 에서 간략히 말했듯, 네트워크 상의 통신 또한 컴퓨터 내의 언어계층도와 유사한 면이 있다.  
우리가 프로그래밍을 할때, 사람이 알아 보기 쉬운 고레벨언어(Java, C 등등) 으로 코딩하면, 이를 컴파일하여 어쌤블리어로 변환하고, 이를 다시 0과1로 변환하는 과정이 있듯 네트워크 또한 7가지 단계로 이러한 과정을 나눈다. (최근에는 TCP/IP모델이 주류(?)이나 직관적으로 이해하긴 OSI모델이 더 좋은 것 같다)  
7단계로 나누기에, OSI 7계층으로도 많이 불리는데, 7가지 계층은 다음과 같다.  
![](https://nabi-yi.github.io/assets/images/220607_OSI.jpg){: .align-center}


그 중 HTTP는 JAVA와 같은 고레벨 언어로, 클라이언트와 서버가 데이터를 송수신함에 있어 지킬 규약, 문법이라고 볼 수 있다. 
이렇게 규약에 맞춰 HTTP 메시지를 작성하면, 이러한 데이터는 Packet이라는 데이터 통신 단위로 감싸지게 되고(인코딩, encryption 등), 통신이므로 이 패킷을 어디로 보낼지 길을 찾는 과정을 거친 후(라우팅, Datalink, Network layer), 전기신호로 물리적 통신을 하는(Physical Layer) 일련의 과정을 거친다. 수신 측에서는 반대 순서로 올라 갈 것이다.


![](https://nabi-yi.github.io/assets/images/220607_httpMessage.jpg){: .align-center}
###### *출처 : Wikipedia*  
이러한 HTTP Message를

![](https://nabi-yi.github.io/assets/images/220607_physical.jpg){: .align-center}
이렇게 디지털 신호로 변환하여 송수신한다.

윗 사진은 시작과 끝만을 나타냈지만.. 사실 중간 과정에 있는 길찾기(라우팅)이나, Acknowledge, Handshaking등 통신 선로(?)를 구축하는 과정, 손실, 왜곡 에러를 수정하는 과정 등.. 통신 자체에 대한 부분도 흥미롭고 신기한 부분이 많다.  
다음 포스팅에는 DNS와 함께 라우팅(길찾기)에 대한 Network Layer와 Physical Layer를 간단하게만 알아보자.