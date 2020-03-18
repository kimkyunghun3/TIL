```
<h1>, <h2>, <h3>, <h4>, <h5>, <h6>
문서의 정보 계층을 구조화.
(Heading, 문서나 구분된 영역의 제목을 설정, 문서의 목차)

숫자가 낮을수록 높은 단계(중요한)의 제목.
h1, h2, h3, h4, h5, h6 { display: block; }

<header>
문서의 헤더를 설정.
(보통 로고, 제목, 검색 등을 포함)

header { display: block; }

<footer>
문서의 푸터를 설정.
(보통 작성자, 저작권, 관련 문서 등을 포함)

footer { display: block; }

<main>
문서의 주요 콘텐츠를 설정.

IE 지원 불가
한 문서에 하나의 <main> 요소만 포함 가능.
main { display: block; }

<article>
독립적으로 구분되거나 재사용 가능한 영역을 설정.
(매거진/신문 기사, 블로그 등)

일반적으로 <h1>~<h6>를 포함하여 식별.
작성일자와 시간을 <time>의 datetime 속성으로 작성.
article { display: block; }

<section>
문서의 일반적인 영역을 설정.

일반적으로 <h1>~<h6>를 포함하여 식별.
section { display: block; }

<aside>
문서의 별도 콘텐츠를 설정.
(보통 광고나 기타 링크 등의 사이드바(Side bar)를 설정)

aside { display: block; }

<nav>
다른 페이지 링크를 제공하는 영역을 설정.
(Navigation, 보통 메뉴(Home, About, Contact), 목차, 색인 등을 설정)

nav { display: block; }

<address>
<body>, <article>, <footer> 등에서 연락처 정보를 제공하기 위해 포함하여 사용.

address { display: block; }

<div>
본질적으로 아무것도 나타내지 않는 콘텐츠 영역을 설정.
(Division, 꾸미는 목적으로 사용)

div { display: block; }

각 컨텐츠를 구분하는 다양한 방법이 있으므로 이해하고 사용할 필요가 있다.
```