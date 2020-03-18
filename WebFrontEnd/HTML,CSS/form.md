```
**양식**

<form>
웹 서버에 정보를 제출하기 위한 양식 범위를 정의.

<form>이 다른 <form>을 자식 요소로 포함할 수 없음.
속성          	    의미	                         값	                        기본값
action	        전송한 정보를 처리할 웹페이지의 URL	    URL	
autocomplete	사용자가 이전에 입력한 값으로 자동 완성 기능을 사용할 것인지 여부on, off	 on
method	        서버로 전송할 HTTP 방식	           GET, POST    	            GET
name	        고유한 양식의 이름		
novalidate	    서버로 전송시 양식 데이터의 유효성을 검사하지 않도록 지정		
target	        서버로 전송 후 응답받을 방식을 지정	_self, _blank	                _self
form { display: block; }


<input />
사용자에게 입력 받을 데이터 양식.

속성	    의미	값	    기본값 	특징
autocomplete	사용자가 이전에 입력한 값으로 자동 완성 기능을 사용할 것인지 여부	on, off	on	
autofocus	페이지가 로드될 때 자동으로 포커스	불린(Boolean)		문서 내 고유해야 함
checked	양식이 선택되었음을 표시	불린(Boolean)		type 속성 값이 radio, checkbox일 경우만
disabled	양식을 비활성화	불린(Boolean)		
form	<form>의 id 속성 값			해당 <form>의 후손이 아닐 경우만
list	참조할 <datalist>의 id 속성 값			
max	지정 가능한 최대 값	숫자(Number)		type 속성 값이 number일 경우만,
min속성보다 큰 값만 허용
min	지정 가능한 최소 값	숫자(Number)		type 속성 값이 number일 경우만,
max속성보다 작은 값만 허용
maxlength	입력 가능한 최대 문자 수	숫자(Number)	524288	type 속성 값이 text, email, password, tel, url일 경우만
multiple	둘 이상의 값을 입력 할 수 있는지 여부	불린(Boolean)		type 속성 값이 email, file일 경우만,
email일 경우 ,로 구분
name	양식의 이름			
placeholder	사용자가 입력할 값의 힌트			type 속성 값이 text, search, tel, url, email일 경우만
readonly	수정 불가한 읽기 전용	불린(Boolean)		
step	유효한 증감 숫자의 간격	숫자(Number)	1	type 속성 값이 number, range일 경우만
src	이미지의 URL	URL		type 속성 값이 image일 경우만
alt	이미지의 대체 텍스트			type 속성 값이 image일 경우만
type	입력 받을 데이터의 종류	별도 정리	text
value	양식의 초기 값			
데이터 종류(Type)의 값(Values)
type속성에 입력할 수 있는 값의 목록.

<input type="button" />
<input type="checkbox" />
<input type="file" />
<input type="text" />
값	데이터 종류	특징
button	일반 버튼	<button>처럼 사용
checkbox	체크박스	
color	색상	IE 지원 불가
email	이메일	
file	파일	
hidden	보이지 않지만 전송할 양식	value 속성으로 값을 지정
image	이미지 제출 버튼	<img />처럼 사용
number	숫자	
password	비밀	가려지는 양식
radio	라디오 버튼	같은 name 속성 그룹 내 하나만 선택 가능
range	범위 컨트롤	min, max, step, value(기본값) 속성 사용
reset	초기화	해당 <form> 범위 내 모든 양식
search	검색	
submit	제출 버튼	해당 <form> 범위 내 고유한 양식
tel	전화번호	
text	일반 텍스트	
url	절대 URL	
input { display: inline-block; }

*placeholder - 작성 전에 가이드라인 같이 제공되는 것
*autocomplete - 자동완성으로 입력하는 곳 아래에 이전에 입력한 것이 제공되는 것

<label>
라벨 가능 요소(labelable)의 제목(Caption).

for 속성으로 라벨 가능 요소를 참조하거나 콘텐츠로 포함.
라벨 가능 요소: <button>, <input>, <progress>, <select>, <textarea>
속성	의미
for	참조할 라벨 가능 요소의 id 속성 값
<!-- 라벨 가능 요소를 참조 -->
<input type="checkbox" id="user-agreement" />
<label for="user-agreement">동의하십니까?</label>

<!-- 라벨 가능 요소를 포함 -->
<label><input type="checkbox" />동의하십니까?</label>
label { display: inline; }

<button>
선택 가능한 버튼을 지정.

속성	                의미              	값	            특징
autofocus	페이지가 로드될 때 자동으로 포커스	불린(Boolean)	문서 내 고유해야 함
disabled	버튼을 비활성화	불린(Boolean)	
form	<form>의 id 속성 값		해당 <form>의 후손이 아닐 경우만
name	폼 데이터와 함께 전송되는 버튼의 이름		
type	버튼의 타입	button, reset, submit	
button { display: inline-block; }

<textarea>
여러 줄의 일반 텍스트 양식.

속성	의미	값	기본값	특징
autocomplete	사용자가 이전에 입력한 값으로 자동 완성 기능을 사용할 것인지 여부	on, off	on	
autofocus	페이지가 로드될 때 자동으로 포커스	불린(Boolean)		문서 내 고유해야 함
disabled	양식을 비활성화	불린(Boolean)		
form	<form>의 id 속성 값			해당 <form>의 후손이 아닐 경우만
maxlength	입력 가능한 최대 문자 수	숫자(Number)	무한	
name	양식의 이름			
placeholder	사용자가 입력할 값의 힌트			
readonly	수정 불가한 읽기 전용	불린(Boolean)		
rows	양식의 줄 수	숫자(Number)	2	
textarea { display: inline-block; }

<fieldset>, <legend>
같은 목적의 양식을 그룹화(<fieldset>)하여 제목(<legend>)을 지정.

<form>
  <fieldset>
    <legend>Coffee Size</legend>
    <label>
        <input type="radio" name="size" value="tall" />
        Tall
    </label>
    <label>
        <input type="radio" name="size" value="grande" />
        Grande
    </label>
    <label>
        <input type="radio" name="size" value="venti" />
        Venti
    </label>
  </fieldset>
</form>
fieldset, legend { display: block; }

<fieldset>
같은 목적의 양식을 그룹화.

속성	의미	값
disabled	그룹 내 모든 양식 요소를 비활성화	불린(Boolean)	
form	그룹이 속할 하나 이상의 <form>의 id 속성 값	
name	그룹의 이름	
<select>, <datalist>, <optgroup>, <option>
옵션(<option>, <optgroup>)의 선택 메뉴(<select>)나 자동완성(<datalist>)을 제공.

<select>
  <optgroup label="Coffee">
    <option>Americano</option>
    <option>Caffe Mocha</option>
    <option label="Cappuccino" value="Cappuccino"></option>
  </optgroup>
  <optgroup label="Latte" disabled>
    <option>Caffe Latte</option>
    <option>Vanilla Latte</option>
  </optgroup>
  <optgroup label="Smoothie">
    <option>Plain</option>
    <option>Strawberry</option>
    <option>Banana</option>
    <option>Mango</option>
  </optgroup>
</select>
select { display: inline-block; }
datalist { display: none; }
optgroup, option { display: block; }

<select>
옵션을 선택하는 메뉴.

속성	의미	값	기본값
autocomplete	사용자가 이전에 입력한 값으로 자동 완성 기능을 사용할 것인지 여부	on, off	on	
disabled	선택 메뉴를 비활성화	불린(Boolean)	
form	선택 메뉴가 속할 하나 이상의 <form>의 id 속성 값		
multiple	다중 선택 여부	불린(Boolean)	
name	선택 메뉴의 이름		
size	한 번에 볼 수 있는 행의 개수	숫자(Number)	0(1과 같음)
<datalist>
<input>에 미리 정의된 옵션을 지정하여 자동완성(Autocomplete) 기능을 제공하는 데 사용.

<input>의 list 속성 바인딩.
<option>을 포함하여 정의된 옵션을 지정.
<input type="text" list="fruits">

<datalist id="fruits">
  <option>Apple</option>
  <option>Orange</option>
  <option>Banana</option>
  <option>Mango</option>
  <option>Fineapple</option>
</datalist>


<optgroup>
<option>을 그룹화.

속성	의미	값
label	(필수)옵션 그룹의 이름	
disabled	옵션 그룹을 비활성화	불린(Boolean)
<option>
선택 메뉴(<select>)나 자동완성(<datalist>)에서 사용될 옵션.

선택적 빈(Empty) 태그로 사용 가능.
속성	의미	값	특성
disabled	옵션을 비활성화	불린(Boolean)	
label	표시될 옵션의 제목		생략되면 포함된 텍스트를 표시
selected	옵션이 선택되었음을 표시	불린(Boolean)	
value	양식으로 제출될 값		생략되면 포함된 텍스트를 값으로 사용

<progress>
작업의 완료 진행률을 표시.

속성	의미	값	특징
max	작업의 총량	숫자(Number)	
value	작업의 진행량	숫자(Number)	max 속성을 생략할 경우 0~1 사이의 숫자여야 함
<progress value="70" max="100">70 %</progress>
progress { display: inline-block; }

```