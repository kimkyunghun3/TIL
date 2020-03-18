```
**인라인 텍스트**

<a>
다른 페이지, 같은 페이지 위치(#, 해시 태그), 파일, 이메일 주소, 전화번호 등 다른 URL로 연결할 수 있는 하이퍼링크를 설정.
(Anchor, 외부로 내보내기)

속성	의미	값	기본값	특징
download	이 요소가 리소스를 다운로드하는 용도로 사용됨을 의미	불린(Boolean)	
href	링크 URL	URL		생략 가능
rel	현재 문서와 링크 URL의 관계(Link Types)	license, prev, next…		
target	링크 URL의 표시(브라우저 탭) 위치	_self, _blank	_self	
type	링크 URL의 MIME 타입	text/html…		
a { display: inline; }

** 밑줄과 구분되도록 써야한다. 아니면 사용자가 헷갈릴 수 있다.

<abbr>
약어를 지정.
(Abbreviation, 보통 title 속성을 사용하여 전체 글자나 설명을 제공)

Using <abbr title="HyperText Markup Language">HTML</abbr> is fun and easy!
abbr { display: inline; }

<b>
문체가 다른 글자의 범위를 설정.
(Bring Attention)

특별한 의미를 가지지 않음.
읽기 흐름에 도움을 주는 용도로 사용.
다른 태그가 적합하지 않은 경우 마지막 수단으로 사용.
기본적으로 글자가 두껍게(Bold) 표시됨.
b { display: inline; }

<mark>
사용자의 관심을 끌기 위해 하이라이팅할 때 사용.
(Mark Text, 형광펜을 사용하여 관심있는 부분을 표시하는 것과 같은 의미)

기본적으로 형광펜을 사용한 것처럼 글자 배경이 노란색(Yellow)으로 표시됨.
mark { display: inline; }

<em>
단순한 의미 강조를 표시.
(Emphasis)

중첩이 가능.
중첩될수록 강조 의미가 강해짐.
정보통신보조기기 등에서 구두 강조로 발음됨.
기본적으로 이탤릭체(Italic type)로 표시됨.
em { display: inline; }

** 중첩 사용하는 것은 사용자가 구별하기 어렵지만 정보통신보조기기에서 구분할 수 있다.

<strong>
의미의 중요성을 나타내기 위해 사용.
(Strong Importance)

기본적으로 글자가 두껍게(Bold) 표시됨.
strong { display: inline; }

<i>
<em>, <strong> <mark> <cite> <dfn> 등에서 표현할 수 있는 적합한 의미가 아닌 경우 사용.
(평범한 글자와 구분(아이콘이나 특수기호 같은)하기 위해 사용)

기본적으로 이탤릭체(Italic type)로 표시됨.
i { display: inline; }

<dfn>
용어를 정의할 때 사용.
(Definition)

dfn { display: inline; }

<cite>
창작물에 대한 참조를 설정.
(책, 논문, 영화, TV 프로그램, 노래, 게임 등의 제목)

기본적으로 이탤릭체(Italic type)로 표시됨.
<cite>The Scream</cite> by Edward Munch. Painted in 1893.
cite { display: inline; }

<q>
짦은 인용문을 설정.
(Inline Quotation)

긴 인용문을 설정할 경우 <blockquote>를 사용.
속성	의미	값
cite	인용된 정보의 URL	URL
q { display: inline; }

<u>
밑줄이 있는 글자를 설정.
(Underline)

순수하게 꾸미는 용도의 요소로 사용.
<a>와 헷갈릴 수 있는 위치에서 사용하지 않도록 주의.
<span style="text-decoration: underline;">을 활용할 수 있을 경우에는 사용을 권장하지 않음.
u { display: inline; }

<code>
컴퓨터 코드 범위를 설정.
(Inline Code)

<code>document.getElementById('id-value')</code> is a piece of computer code.

기본적으로 고정폭(Monospace) 글꼴 계열로 표시됨.
code { display: inline; }

<kbd>
텍스트 입력 장치(키보드)에서 사용자 입력을 나타내는 텍스트 범위를 설정.
(Keyboard Input)

<p><kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd></p>, <kbd>ESC</kbd>
kbd { display: inline; }

** CSS이용하여 좀 더 예쁘게 꾸밀 필요가 있다. 

<sup>, <sub>
위 첨자(<sup>)와 아래 첨자(<sub>를 설정.
(Superscripted text, Subscript text)

X<sup>4</sup> + Y<sup>2</sup>, H<sub>2</sub>O
sup, sub { display: inline; }

<time>
날짜나 시간을 나타내기 위한 목적으로 사용.

속성	의미	값
datetime	유효한 날짜 문자	Date
IE 지원 불가
<p>The Cure will be celebrating their 40th anniversary on <time datetime="2018-07-07">July 7</time> in London's Hyde Park.</p>
time { display: inline; }

<span>
본질적으로 아무것도 나타내지 않는 콘텐츠 영역을 설정.

span { display: inline; }

** 특정한 의미 없이 문장 중간에 특정 부분을 색깔 바꾸거나 하는 등 사용할 때 쓰임
** div와 비슷하다. div는 block형식으로 한 줄을 다 쓰지만 span은 그렇지 않다.

<br />
줄바꿈을 설정.

br { display: inline; }

```