````
div {
  font-size: 20px;
  color: red;
}

/* 다음과 같이 이해할 수 있습니다. */
선택자 {
  속성: 값;
  속성: 값;
}
선택자의 역할
선택자는 HTML에 스타일(CSS)을 적용하기 위해 HTML의 특정한 요소를 선택하는 사인(sign)입니다.
“빨강 글자색(CSS, color: red;)을 저기 제목(HTML, <h1></h1>)에 적용하겠어!”, “파랑 글자색(CSS, color: blue;)은 여기 본문(HTML, <p></p>)에 적용하겠어!”와 같이 적용할 스타일을 속성(color)과 값(red, blue)으로 나타내고 적용할 대상(H1, P)을 선택자로 나타냅니다.

위 내용을 코드로 구성하면 다음과 같습니다.

<div>
  <h1>제목..</h1>
  <p>본문..</p>
</div>
h1 {
  color: red;
}
p {
  color: blue;
}
속성(Properties)과 값(Value)
속성과 값은 글자색은 무엇, 너비는 얼마, 여백은 얼마 같은 스타일을 지정할 때 사용합니다.

div {
  color: red; /* 글자색은 빨강 */
  font-size: 20px; /* 글자 크기는 20px */
  width: 300px; /* 가로 너비는 300px */
  margin: 20px; /* 바깥 여백은 20px */
  padding: 10px 20px; /* 안쪽 여백은 위아래 10px, 좌우 20px */
  position: absolute; /* 위치는 부모 요소 기준, 흠.. 이게 무슨 뜻일까? */
}
속성과 값은 많이 아는 것이 중요합니다.
글자 크기를 키우고 싶은데 font-size가 어떤 역할을 하는지 모른다면 글자 크기를 조절할 방법이 없습니다.
또한 위치(좌표)를 지정하고 싶은데 position 속성을 모르거나 혹은 그 속성의 값으로 사용하는 absolute가 어떤 의미를 갖는지 모르면 역시 방법이 없습니다.

CSS 선언 방식
이제 내가 작성한 CSS 코드를 어떻게 HTML에 적용할 수 있는지 알아봅시다.

태그에 직접 작성하기(인라인)
이 방법은 HTML 태그에 직접 작성하기 때문에 선택자가 필요하지 않습니다.

<div style="color: red;">태그에 직접 작성1</div> <!-- red -->
<div style="color: red;">태그에 직접 작성2</div> <!-- red -->
<div style="color: red;">태그에 직접 작성3</div> <!-- red -->
<div style="color: red;">태그에 직접 작성4</div> <!-- red -->
HTML에 포함하기(내장)
CSS만 따로 작성하기 때문에 선택자가 필요합니다.
CSS 코드가 HTML의 <style></style> 안에 포함되어 있습니다.

<head>
  <style>
    div {
      color: red;
    }
  </style>  
</head>
<body>
  <div>HTML에 포함1</div> <!-- red -->
  <div>HTML에 포함2</div> <!-- red -->
  <div>HTML에 포함3</div> <!-- red -->
</body>
HTML 외부에서 불러오기
CSS 코드를 완전히 분리할 수 있습니다.
분리된 하나의 CSS 파일을 여러 HTML 파일이 불러와서 사용할 수 있겠네요.

<!-- HTML 1 -->
<head>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>
  <div>HTML에 외부에서 불러오기1</div> <!-- red -->
</body>
<!-- HTML 2 -->
<head>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>
  <div>HTML에 외부에서 불러오기2</div> <!-- red -->
</body>
/* main.css */
div {
  color: red;
}
선택자
위에서 설명했듯 선택자는 HTML의 특정한 요소를 선택하는 사인(sign)입니다.
여러 종류가 있는데 우선 그중 2가지만 알아보겠습니다.

태그로 찾기
선택자를 입력하는 부분에 적용하려는(찾으려는) 태그의 이름을 입력합니다.

/*<h1>은 글자색이 빨강이야!*/
h1 {
  color: red;
}
/*<p>는 글자색이 파랑이야!*/
p {
  color: blue;
}
<h1>제목1</h1> <!--red-->
<h1>제목2</h1> <!--red-->
<p>본문1</p> <!--blue-->
<p>본문2</p> <!--blue-->
만약 ‘제목1’과 ‘본문1’에만 색상을 추가하고 싶다면 어떻게 해야 할까요?
‘태그 선택자’만 가지고는 어렵습니다.

클래스로 찾기
좀 더 명확하게 원하는 요소를 찾기 위해서 ‘클래스 선택자’라는 것이 존재합니다.

/*class="title"은 글자색이 빨강이야!*/
.title {
  color: red;
}
/*class="main-text"는 글자색이 파랑이야!*/
.main-text {
  color: blue;
}
<h1 class="title">제목1</h1> <!--red-->
<h1>제목2</h1>
<p class="main-text">본문1</p> <!--blue-->
<p>본문2</p>
class라는 HTML 속성에 원하는 별명을 입력합니다.
제목에는 title을 본문에는 main-text라는 별명을 지정했습니다.
CSS에서 이 별명을 기준으로 요소를 찾을 수 있습니다.
단, 주의할 점은 선택자에 앞에 .이 붙는다는 것입니다.
.은 클래스를 나타내며 CSS의 .title은 HTML의 class="title"와 동일합니다.
.이 없는 선택자 title은 태그 <title>를 의미하게 되니 전혀 다른 뜻으로 인식됩니다.
이처럼 .과 같은 특수한 기호들을 이용해서 HTML과 CSS를 매칭하므로 누락하기 쉽습니다. 따라서 꼼꼼한 선택자 작성이 중요합니다.

````