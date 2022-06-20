---
title: "Spring AOP"

categories:
  - CheatSheet
tags:
  - Spring
  - AOP
---
### pointcut Expression
(S)는 Spring AOP에서만 메서드 실행.  
* 모든 공개 메서드
```execution(public * * (..))```
* **set** ~이름으로 시작하는 모든 메서드  
```execution(* set* (..))```
* **AccountService 인터페이스에** 의해 정의된 모든 메서드  
```execution(* com.xyz.service.AccountService.*(..))```
* **service 패키지**에 의해 정의된 메서드  
```execution(* com.xyz.service. *.* (..))```
* **service 패키지 또는 하위 패키지** 중 하나에 의해 정의된 메서드  
```execution(* com.xyz.service..*.*(..))```
* service 패키지 내의 **모든 조인 포인트** (S)  
```within(com.xyz.service.*)```
* service 패키지 또는 하위 패키지 내의 모든 조인 포인트 (S)  
```within(com.xyz.service..*)```
* **AccontService 프록시** 가 인터페이스를 구현하는 모든 조인포인트 (S)  
```this(com.xyz.service.AccountService)```
* **AccountService 대상 객체**가 인터페이스를 구현하는 모든 조인포인트 (S)  
```target(com.xyz.service.AccountService)```
* **단일 매개변수를 사용**하고 런타임에 전달된 인수가 **Serializable 과 같은** 모든 조인포인트 (S)  
```args(java.io.Serializable```
* **대상 객체에 @Transactional**이 있는 모든 조인포인트 (S)  
```@target(org.springframework.transaction.annotation.Transactional)```
* **실행 메서드에 @Transactional**이 있는 조인포인트 (S)  
```@annotation(org.springframework.transaction.annotation.Transactional)```
* **단일 매개변수를 사용**하고 전달된 인수의 런타임 유형이 **@Classfied**를 갖는 조인 포인트 (S)  
```@args(com.xyz.security.Classified)```
* **tradeService**라는 이름을 가진 **스프링 빈**의 모든 조인 포인트(S)  
```bean(tradeService)```
* 와일드 표현식 Service라는 이름을 가진 스프링 빈의 모든 조인 포인트 (S)  
```bean(*Service)```