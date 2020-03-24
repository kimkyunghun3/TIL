```

① Http 요청

  Client에서 웹 애플리케이션에 요청을 하기 위해 Http 요청을 한다.
  요청을 하기 위한 여러 메타 데이터(URL, 파라미터 정보, Http method, header, cookie 등)를 전달하면 HttpServletRequest라는 객체로 요청 메타 정보를 담는다.
  HttpServletRequest는 Http 요청 메타 데이터를 담는 객체다.

② Controller 선택

  직접 작성한 Controller로 가장 먼저 요청을 받는 것 처럼 보이지만 실제 처음 요청 받는 부분은 DispatcherServlet에서 처리하게 된다. 즉 DispatcherServlet에서 컨트롤러로 Http 요청을 위임하는 것이다. 

HandlerMapping : DispatcherServlet에서 Controller로 요청을 위임하기 위해 어떤 Controller를 사용할 것인지 결정하기 위해 사용하는 객체이다. @Controller, @RequestMapping을 사용할 때는 DefaultAnnotationHandlerMapping이 기본 HandlerMapping 전략이다.
HandlerAdapter : HandlerMapping에서 Controller를 선택했다면, Controller를 DispatcherServlet이 실행하기 위해서는 HandlerAdapter가 필요하다. Controller를 구현하는 여러가지 방법이 존재하기 때문에 HandlerAdapter가 필요하다. @Controller, @RequestMapping을 사용할 때는 AnnotationMethodHandlerAdapter가 기본 HandlerAdapter 전략이다.
DefaultAnnotationHandlerMapping과 AnnotationMethodHandlerAdapter API 문서를 보면 알겠지만 3.2 이후로 Deprecated되고 RequestMappingHandlerMapping과 RequestMappingHandlerAdapter로 대체 되었다. (참고)

③ Controller 책임

  MVC에서 "C"에 해당하는 Controller의 책임은

요청(Http 요청)을 해석한다.
해석한 요청을 처리하기 위한 비즈니스 로직이 수행될 수 있도록 Service Layer를 선택한다.
비즈니스 로직 수행 후 모델을 결과로 받는다. (④번에 해당한다.)
어떤 View를 사용할지 결정한다.

⑤ 모델과 뷰 반환
  Controller는 자신의 책임을 모두 수행한 후 생성된 모델과 뷰를 반환한다. 보통 Controller는 View의 구현체를 바로 반환하지 않고 View의 정보를 반환한다. View의 구현체를 반환하지 않고 정보를 반환하는 이유는 DispatcherServlet에서 View의 정보를 이용해 ViewResolver로 구현체를 생성하기 때문이다. 


⑥,⑦ View 생성과 모델 참조

  Controller에서 전달 받은 Model과 View 정보를 토대로 ViewResolver를 사용해 Client에게 보여줄 View를 생성한다.
  ①에서 요청 정보를 HttpServletRequest에 받는다고 했는데 이 영역에서는 응답을 하기 위한 응답 정보를 HttpServletResponse 객체를 사용한다. 기본 ViewResolver 구현체는 InternalResourceViewResolver가 있다.

⑧ Client에게 응답한다.
```