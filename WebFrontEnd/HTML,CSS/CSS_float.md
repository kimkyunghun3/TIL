```
float
요소를 좌우 방향으로 띄움(수평정렬)
none 요소 띄움 없음
left 왼쪽 띄움
right

왼쪽을 하면 왼쪽 옆(사진)으로 글씨가 이어지도록 하는 것이고 오른쪽(사진)으로 하면 오른쪽에도 글씨가 이어지도록 하는 것이다.

float:right을 하면 우측에서부터 쌓기 시작하는 것이기 때문에 오른쪽부터 1,2,3 순서로 된다.
float:left을 하면 반대로 1,2,3 순서로 된다.

float을 이용하지 않는 부분을 만들어도 이는 float이 적용 되어서 이전의 것과 같이 정렬이 되어서 겹치게 된다.
-> 이를 해결하기 위해서 clear: left, right 이용하여 겹치치 않고 수직으로 밑으로 나오게 할 수 있다.

정렬은 float:left 이면 clear:left으로 하면 바로 밑에 나오게 된다. both을 이용하면 이처럼 나오는 문제를 없앨 수 있다.

<부모요소에 clearfix클래스를 추가하여 이용하여 하는 것이 제일 좋다.>

.clearfix:after 을 이용하면 앞에 있는 것들을 div같은 것으로 맵핑한 다음 이를 이용하면 갇혀 있는 것을 해제할 수 있다.
비어 있는 content : ""; 을 추가해야 된다. + clear:both;
**빼야되는 내용은 clearfix div 맵핑 안에 있으면 안된다. 바깥쪽에 빼야만 적용이 된다


display 수정
float 속성이 추가된 요소는 display 속성의 값이 대부분 block으로 수정된다.
원래는 inline으로 되어있는 것들(span)이 display을 쓰게되면 블록으로 바뀌게 된다. 

대부분 block으로 바뀌지만 flext와 inline-flex는 바뀌지 않는다.

clear
flat 속성이 적용되지 않도록 해제한다

none 요소 띄움 허용!
left
right
both 양쪽 모두 띄움 해제

position
요소의 위치 지정 방법의 유향(기준)을 설정
배치하는 것은 아니고 기준을 설정하는 것이다.

static 기준 없음 / 배치 불가능
relative 요소 자신을 기준으로 배치
absolute 위치상 부모 요소를 기준으로 배치
fixed 브라우저를 기준으로 배치
sticky 스크롤 영역 기준으로 배치

position을 통해 기준을 정하는 것이다. 부모를 기준으로 child 밑으로 50px 이런식으로 정할 때 사용한다.

relative는 자기자신을 기준으로 하기 때문에 주변에 형제의 영향을 받기 때문에 대부분 absolute를 이용하는 것이 편하다.

absolute는 1,2,3 순서대로 있을 때 2번에 적용한다면 3번이 2번 자리에 가게 된다. 왜냐하면 2번은 배치할 준비를 하고 있기 떄문에 3번이 2번자리로
가게된다.
parent 부분에는 relative가 선언되어 있어야 된다. 그렇지 않으면 view 전체의 기준으로 정해진다.(화면 전체의 기준) ==fixed

sticky는 스크롤 영역에 맞닿았을 때만 적용되고 1개이상 이어야 한다. top, left, right, bottom 중 하나는 꼭 사용해야 한다. 

<요소 쌓임 순서>
position 속성의 값이 있을 경우 가장 위에 쌓임(값은 무관) -동일한 것은 작성한 순서대로 위에 쌓인다.
position이 모두 존재한다면 z-index 속성의 숫자 값이 높을 수록 위에 쌓임 -- z-index 기본값은 0이다.(가장 밑)

<display 수정>
absolute, fixed 속성 값이 적용된 요소는 display 속성의 값이 대부분 block으로 변환된다. ( flex, inline-flex 제외)


```