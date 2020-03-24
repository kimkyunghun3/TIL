```
background - 색상, 이미지경로, 반복, 위치, 스크롤특성;   --일부 생략해도 가능하다

.box {
    background: red url("..") no-repeat left top scroll;

background-color - 요소의 배경색상을 지정 = background 라고 해도된다.
요소의 배경색은 transparent 이다

background-image - 요소의 배경에 하나 이상의 이미지르 삽입
기본 값은 none
url("경로") - 이미지 경로(URL)

url("../img/imgage.jpg");    -- ..은 뒤로 나가는 것을 의미한다
경로를 ',' 를 통해 여러 개 지정할 수 있다. 하나에 대해 완료 한 다음 쉼표를 이용해야 한다.(추가 옵션들을 다 입력)
요소의 범위 내에서 넓이와 높이를 늘리면 반복적으로 나오는데 이를 막기 위해서는 background-repeat:no-repeat 을 이용해야 한다. 

repeat - 배경 이미지를 수직, 수평으로 반복
repeat-x -배경 이미지를 수평으로 설정
repeat-y
no-repeat 반복 없음

background-position
배경 이미지의 위치를 설정
기본 값은 0% 0%로 수치를 입력할 수 있다. 앞은 x축 뒤는 y축을 말한다. 이를 지켜야 한다
방향으로 top bottom left right center로 이용 가능 background-position :방향1, 방향2;   방향1, 방향2 바꿔도 가능하다
단위로 px, em, cm 등 단위로 설정 가능하다.
px와 방향을 같이 사용할 수 있지만, 방향을 1번 2번 중에 입력하는 것은 X, Y을 생각하고 입력해야 적용된다.

background-attachment
요소가 스클로될떄 배경 이미지의 스크롤 여부(특성) 설정
scroll 배경 이미지가 요소를 따라서 같이 스크롤 됨(기본값)
fixed 배경 이미지가 뷰포트에 고정되어, 요소와 같이 스크롤 되지 않음
local 요소 내 스크롤 시 배경 이미지가 같이 스크롤 됨

background-size
배경 이미지의 사이즈를 설정
auto - 배경 이미지가 원래의 크기로 표시됨
px, em, % 등 단위로 지정
width, height 형태로 입력 가능

cover - 배경 이미지의 크기 비율을 유지하여 요소의 더 넓은 너비에 맞춰짐
      - 이미지가 잘릴 수 있음
contain - 배경 이미지의 크기 비율을 유지하며, 요소의 더 짧은 너비에 맞춰
        - 이미지가 잘리지 않음

```