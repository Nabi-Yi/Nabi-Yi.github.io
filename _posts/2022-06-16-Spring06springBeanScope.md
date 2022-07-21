---
title: "Bean Scope"

categories:
  - Spring
tags:
  - Spring Containter
  - Bean(Spring)
---
### Bean Scope
Bean Scope는 Bean Definition을 만들 때 Bean이 존재 할 수 있는 범위를 지정해주는 것을 의미한다.  
ApplicationContext를 이용하여 6개의 범위를 설정 할 수 있다.
* Singleton : 기본 값이며 단일 객체 인스턴스에 대한 단일 bean definition의 범위를 지정한다. 스프링 컨테이너의 시작과 함께 생성 및 종료.
* prototype : 컨테이너가 빈의 생성과 DI까지만 관여하고 더는 관리하지 않는다.
* request : 웹 요청이 들어오고 나갈 떄까지 유지된다.
* session : 웹 세션이 생성되고 종료될 때 까지 유지된다.
* application : 웹의 서블릿 컨텍스트와 같은 범위로 유지된다.
* websocket : Websocket의 lifecycle까지 생명주기를 확장한다.

### Singleton Scope
위 6개의 스코프 중 기본값이고 가장 많이 접할 Singleton을 알아보자.  
Singletone은 **클래스의 인스턴스가 1개만 생성되는 것을 보장**해서, 하나의 공유 인스턴스로 Controller가 모든 요청을 관리한다.  

생성된 단일 인스턴스는 싱글톤 빈의 캐시에 저장된다. 모든 해당 빈에 대한 요청과 참조는 해당 캐시된 개체를 반환한다.  
![](https://nabi-yi.github.io/assets/images/220616_singleton.jpg){: .align-center}  

### Singleton Pattern
스프링 컨테이너를 사용하지 않고, 자바 코드로 싱글톤 패턴을 구현 할 수 있다. 

다음과 같이 SingletonService 클래스를 생성하고
```java
public class SingletonService {
    //static 영역에 공유개체 생성
    private static final SingletonService instance = new SingletonService();
    //해당 Singleton 개체가 필요하면 getInstance로만 호출 
    public static SingletonService getInstance(){ 
        return instance;
    }
    private  SingletonService(){
    //생성자 제한
    }
    public void logic(){
        System.out.println("Call Singleton");
    }
}
```
외부에서 객체가 필요한 경우  
```java
static SingletonService singletonService = SingletonService.getInstance();
```
와 같이 호출하여 사용한다. 이렇게 **static 영역에 하나의 개체를 생성하고 모두 그 개체를 참조하게 하여** 싱글톤 패턴을 구현할 수 있다.  
이렇게 직접 패턴을 구현하는 경우
* 패턴 구현에 필요한 자체 코드가 길어지고
* 클래스를 지정하여 가져오기 때문에 테스트와 수정이 어렵고
* private 생성자를 이용하므로 extend가 힘드므로 유연성이 떨어지는  
단점들이 있다. 또한 Multi-Thread 환경에서 공유 속성이 있을 경우 데이터 오염 문제가 생길 수 있기 때문에 싱글톤 패턴에선 변경가능한 변수가 없는 것이 좋다.(읽기전용?)

### Singleton by Spring Container  
싱글톤 컨테이너의 역할을 하는 스프링 컨테이너를 사용하면 훨씬 쉽게 싱글톤 객체를 만들 수 있고, 위의 단점도 커버해준다.  
다음과 같이 클래스 생성 후  **@Configuration**, **@Bean** 어노테이션을 사용한다.
@Bean의 Default Scope가 Singleton이므로 Singleton Bean을 사용 할 수 있다.
```java
@Configuration
public class AppConfig {
    @Bean
    public SingletonService singletonService() {
        return new SingletonService();
    }
}
```
이 후 외부에서 필요 할 때
```java
static ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
static SingletonSerivce singletonService = ac.getBean("singletonService",SingletonService.class);
```
와 같이 호출하여 사용 할 수 있다.  

훨씬 간편하게 사용 할 수 있으나, 컨테이너를 사용하는  경우에도 **Singleton 객체는 Stateless 해야하는데, 패턴 때와 마찬가지로 외부에서 객체 내부의 값을 변경하지 않고 읽기만 가능해야한다.**(공유 값이 없어야한다).  

공유 값이 있을 경우, static메모리 사용과 마찬가지 경우로 의도치 않은 오류가 발생 할 수 밖에 없다.  

### 참조 및 더 읽어볼 거리
[Spring docs - IoC Container](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-basics)  
멀티쓰레드에서의 동기, 비동기도 관리를 해주는가?