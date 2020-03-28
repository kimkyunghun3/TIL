```

| 웹 어플리케이션 설계 모델(Web Application Architecture)

웹 어플리케이션은 크게 MVC 패턴을 따르게 되며 Model, View, Controller로 나뉘게 된다. 

Model : DB와 상호작용하며 비즈니스 로직을 처리하는 모듈 
View : Client에게 보여지는 결과화면을 반환하는 모듈
Controller : Client 요청이 들어왔을 때 그 입력을 처리하고 어떤 로직을 실행시킬 것인지 제어하는 모듈


웹 프로그래밍을 구축할 때의 설계 모델은 Model1, Model2 크게 2가지가 있다. 두 모델의 큰 차이는 클라이언트의 요청 사항을 모듈화되지 하나의 파일로 처리할 것이냐 각각의 기능을 담당하는 모듈들이 역할을 분담해서 처리할 것이냐로 결정된다. .



Model1는 WAS(Web Application Server)에서 모든 파일에 클라이언트가 요청한 로직을 처리하는 경우다. JSP(Java Server Page)에서 View, Controller의 역할을 담당하며 그 결과를 클라이언트에게 반환한다. 


Model1은 아키텍처가 간단하고 JSP에 거의 모든 로직을 집어넣기 때문에 작은 웹 어플리케이션을 제작할 때는 큰 무리가 없지만 대규모 웹 어플리케이션을 제작하게 될 시 유지보수에 큰 어려움이 따른다.

Model2는 이 Model1방식을 보완한 아키텍처다. MVC 패턴에 맡게 Model, Controller, View 부분로 모듈화됬고 JSP는 로직 처리가 없이 단순히 Client에게 보여지는 뷰만을 담당한다. 


이 방식은 각각이 모듈화되어 있어 유지보수가 매우 쉬워지는 큰 장점이 있다. 현재의 웹어플리케이션은 거의 Model2방식을 따른다 보면 된다.


| 스프링 MVC 모델 (Spring MVC Model)

스프링 MVC는 Model2 방식을 따르며 이 Model2의 아키텍처에 맞게 설계되어 있다.


DispatcherServlet가 Client요청을 받음 (중앙 제어실과 같음)
HandlerMapping이 알맞은 Controller를 찾음
HandlerMapping에 실행할 Controller의 메서드를 찾음 
Controller의 메서드를 실행하며 그 결과 Model로서 DispatcherServlet에 반환
ViewResolver는 알맞은 JSP파일을 찾음
View는 JSP파일을 Model의 정보를 토대로 Client에게 반환


```