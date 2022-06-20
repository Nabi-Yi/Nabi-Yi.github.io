---
title: "Spring Container & Bean (1)"

categories:
  - Spring
tags:
  - Spring Containter
  - Bean(Spring)
---
### 먼저, Bean 이란?
* 밑에서 알아볼 Spring Container에 의해 등록되어 관리되는 인스턴트화 된 객체이다.  
* 어노테이션 @Bean이 적힌 메서드를 스프링 컨테이너에 등록 시킬 수 있다.
* 원 클래스의 등록 정보, Getter / Setter Methode를 포함한다.
* 스프링 컨테이너에 사용되는 **설정 메타데이터로 생성** 된다.


### 스프링 컨테이너란?  
* 스프링 컨테이너는 내부에 존재하는 Application Bean의 **생성, 관리, 제거** (생명주기) 등을 담당한다.
* **DI를 통해 빈을 연결하고, 객체간 의존 및 결합을 낮춰준다.(Loose Coupling)**
* 스프링 내에선 ```ApplicationContext``` Interface로 있고, ```BeanFactory``` 및 여러 상위 인터페이스를 상속받아 사용한다.  
```java
public interface ApplicationContext extends EnvironmentCapable, ListableBeanFactory, HierarchicalBeanFactory,
		MessageSource, ApplicationEventPublisher, ResourcePatternResolver{...}
```
직접 org.springfamework.context.ApplicationContext.java로 가서 확인 할 수도 있다.  
* ApplicationContext의 구현체로 스프링 컨테이너를 만들어 쓸 수 있다.
* Spring Container를 사용하기 위한 Configuration Metadata(설정 메타데이터)를 XML으로 작성했었으나 Annotation-Based(2.5), Java-Based(3.0) 등도 지원하며 Java-Base가 대세라고 한다.      


### 왜 써야할까?  
앞서 살펴본 IoC / DI 파트에서 말한 **결합, 의존성을 낮추기 위해서** 사용한다.  
스프링 컨테이너가 객체간의 연결을 관리하기 때문에 new 생성자 없이 참조, 의존성 주입이 **편리**해진다.    
코드 모델이 수정 될 때 해당 되는 모든 코드들을 찾아가며 수정해주지 않아도 된다!!!  

### 스프링 컨테이너의 종류  
**BeanFactory**  
* 스프링 컨테이너의 최상위 인터페이스.
* 빈을 등록, 생성, 조회, 반환 등 빈을 관리함.
* getBean() 메소드로 빈을 인스턴스화.(쓰면 안됨)
* @Bean 어노테이션으로 메서드를 스프링 빈으로 등록가능.

**ApplicationContext**  
* BeanFactory를 상속받아 기존 기능 및 검색 등의 부가기능
 - Message Source
 - EnviromentCapable : 개발, 운영 등 환경 변수 등으로 분할 처리 및 앱 구동에 필요한 정보 관리
 - ApplicationEventPublisher : 이벤트 관련 기능
 - ResourceLoader : 파일, CLASSPATH 등 리소스 조회

사실상 ApplicationContext를 많이 사용. BeanFactory를 직접적으로 사용하는 경우는 잘 없음.  
```java
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
```
로 인스턴스화하여 제공된 위치경로 ResourceLoader등을 경유해 외부 리소스로 부터 메타데이터 로드 가능.  

### Bean Definition
BeanDefinition의 속성에 따라 Spring Container가 Bean을 어떻게 생성, 관리 할 지 결정한다.    
BeanDefinition이라는 interface로 추상화 되어있으며 @Bean 당 하나씩 생성된다.  
Spring Container는 설정 정보를 BeanDefinition을 통해 관리하기 때문에 설정 형식이 XML인지 JAVA인지 몰라도 된다.(?)  


### 참조 및 더 읽어볼 거리
[Spring docs - IoC Container](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-basics)  

