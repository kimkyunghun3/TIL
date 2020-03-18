```

문자 콘텐츠
<ol>, <ul>, <li>
각 항목(<li>)의 정렬된 목록(<ol>)이나 정렬되지 않은 목록(<ul>)을 설정.
(Ordered List, Unordered List, List Item, 순서가 필요하거나(<ol>) 순서가 필요하지 않은(<ul>) 목록을 정의)

<ol>과 <ul>은 자식으로 <li>만 포함 가능.
<li>는 단독으로 사용할 수 없으며, <ol>이나 <ul>에 자식으로 포함되어야 함.
정렬된 목록(<ol>)의 항목 순서는 중요도를 의미할 수 있음.
ol, ul { display: block; }
li { display: list-item; }

<ol>
정렬된 목록을 설정.

속성	의미	값	특징
start	항목에 매겨지는 번호의 시작 값	숫자(Number) - start 숫자부터 이어진다	
type	항목에 매겨지는 번호의 유형	a, A, i, I, 1	

<li>
항목을 설정.

속성	의미	값	특징
value	항목의 순서를 설정	숫자(Number)	이하 항목들의 순서가 다시 지정됨

<dl>, <dt>, <dd>
용어(<dt>)와 정의(<dd>) 쌍들의 영역(<dl>)을 설정.
(Description List, Definition Details, Definition Term)

<dl>은 <dd>, <dt>만을 포함해야 함.
키(key)/값(value) 형태를 표시할 때 유용.
<dl>
  <dt>Coffee</dt>
  <dd>Coffee is a brewed drink prepared from roasted coffee beans, the seeds of berries from certain Coffea species.</dd>
  <dt>Milk</dt>
  <dd>Milk is a nutrient-rich, white liquid food produced by the mammary glands of mammals.</dd>
</dl>
dl, dt, dd { display: block; }

<p>
하나의 문단을 설정.
(Paragraph)

일반적으로 정보통신보조기기 등은 다음 문단(<p>)으로 넘어갈 수 있는 단축키를 제공함.
p { display: block; }

<hr />
문단의 분리(주제에 의한)를 위해 설정.
(Horizontal Rule)

대부분의 경우 수평선(border)으로 표시(표현적 관점)되나 의미적 관점으로만 사용해야 함.
hr { display: block; }

<pre>
서식이 미리 지정된 텍스트를 설정.
(Preformatted Text)

텍스트의 공백과 줄바꿈을 유지하여 표시할 수 있음.
기본적으로 Monospace 글꼴 계열로 표시됨.
pre { display: block; }

<blockquote>
일반적인 인용문을 설정.
(Block Quotation)

속성	의미	값
cite	인용된 정보의 URL	URL
blockquote { display: block; }

ol,ul,li부분은 자주 사용하므로 기억해둘 필요가 있다.

```