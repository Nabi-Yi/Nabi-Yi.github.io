---
title: "Spring Web MVC"

categories:
  - Spring
tags:
  - Spring Web MVC
---
### Spring Web MVC
* 서블릿 API 기반 스프링 Web Framework.
* Spring MVC라고 많이 불림.
* **Model View Controller**
* 클라이언트의 요청을 처리하기 편리하게 해주는 Framework

### Servlet?
* 클라이언트의 요청을 처리하도록 만든 *Java Class file*
* servlet protocol에 맞춰 작성
* Apache Tomcat은 Sevelt Container중 하나
* **Spring MVC 내부에서 Servlet을 기반으로 동작**하므로 우리가 직접 Servlet 코드를 작성하지는 않는다.

### Model
* MVC는 클라이언트의 요청을 전달 받고, 요청 사항을 처리하는 작업을 수행.
* **요청사항을 처리한 결과 데이터** = Model
* Service Layer & Business Logic

### View
* Model을 이용하여 Client Application의 '화면'에 보여지는 Resource를 제공.
*  **JSON**,HTML, PDF, Excel, XML등 다양한 출력 형식
* HTML - Backend + FrontEnd. 직접 렌더링 해서 Client에 전송(SSL?). Thymeleaf, FreeMakser, JSP+JSTL, Tiles.
* PDF,Excel - Model데이터를 가공, 문서 내에서 동적 데이터 변경이 있을 때.
* XML, JSON - 모델 데이터를 Protocol 형태로 변환하여 전송. 해당 데이터를 기반으로 Frontend에서 실제 페이지 출력.  
Frontend측에서 비동기 클라이언트를 만들 수 있다. 영역의 명확한 구분으로 유지보수가 용이함.

### Controller
* 클라이언트의 요청을 직접 전달 받는 Endpoint.
* Model과 View의 중간 연결점.
* Controller에 요청 입력 -> 비즈니스 로직 결과 데이터(Model) -> View로 전달
* 위 과정을 Controller가 중계.


### 참조 및 더 읽어볼 거리



