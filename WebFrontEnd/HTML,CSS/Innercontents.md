```
**내장 콘텐츠**
<iframe>
다른 HTML 페이지를 현재 페이지에 삽입.
(중첩된 브라우저 컨텍스트(프레임)를 표시)

속성	의미	값	기본값
name	프레임의 이름		
src	포함할 문서의 URL	URL	
width	프레임의 가로 너비		
height	프레임의 세로 너비		
allowfullscreen	전체 화면 모드 사용 여부	불린(Boolean)	
frameborder	프레임 테두리 사용 여부	0, 1	1
sandbox	보안을 위한 읽기 전용으로 삽입	불린(Boolean) or
allow-form: 양식 제출 가능,
allow-scripts: 스크립트 실행 가능 ,
allow-same-origin: 같은 출처(도메인)의 리소스 사용 가능	
<iframe width="1280" height="720" src="https://www.youtube.com/embed/Q9yn1DpZkHQ" frameborder="0" allowfullscreen></iframe>
iframe { display: inline; }

#사이즈 조절을 통해 다른 사이트를 넣을 수 있다(원하는 유투브 동영상, 웹사이트 등)

**스크립트**
<script>
스크립트 코드를 문서에 포함하거나 참조(외부 스크립트).

속성	                    의미	                        값	            특징
async	스크립트의 비동기적(Asynchronously) 실행 여부	불린(Boolean)	src 속성 필수
defer	문서 파싱(구문 분석) 후 작동 여부            	불린(Boolean)	src 속성 필수
src	    참조할 외부 스크립트 URL	URL	포함된 스크립트 코드는 무시됨
type	MIME 타입	                          text/javascript(기본값)	
script { display: none; }

*defer을 이용하면 만약 바디의 정보를 script 통해 자스에서 필요로 한다면 script link을 body보다 위에 쓴다면
적용이 안된다. 하지만 defer을 이용하면 HTML 파일을 다 읽은 다음 자스를 보기 때문에 에러가 안난다. 바디 밑으로 자스 링크를
넣을 필요가 없다.

<noscript>
스크립트를 지원하지 않는 경우에 삽입할 HTML을 정의.

<noscript>
  <p>Your browser does not support JavaScript!</p>
</noscript>
noscript { display: inline; }


```