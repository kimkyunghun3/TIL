```
**CSS 속성**

크기, 여백, 색상 같은 눈에 보이는 스타일을 지정할 수 있습니다.

크기
width(가로 너비)
요소의 가로 너비를 지정합니다.
단위는 px(pixels)을 사용합니다.

div {
  width: 300px;
  요소가로너비: 너비값;
}
height(세로 너비)
요소의 세로 너비를 지정합니다.

div {
  height: 150px;
  요소세로너비: 너비값;
}
font-size(글자 크기)
요소 내용(Text)의 글자 크기를 지정합니다.

div {
  font-size: 16px;
  글자크기: 크기값;
}
여백
margin(요소의 바깥 여백)
요소의 바깥 여백을 지정합니다.
바깥 여백은 요소와 요소 사이의 여백(거리, 공간)을 생성할 때 사용합니다.

div {
  margin: 20px;
  요소바깥여백: 여백값;
}
위 코드는 margin은 요소의 위, 아래, 좌, 우 모두 20px의 여백을 지정하겠다는 의미입니다.
세분화하기 위해 아래와 같이 한 방향씩 지정할 수도 있습니다.
위 코드와 아래 코드는 같은 의미입니다.

div {
  margin-top: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
  margin-left: 20px;
  요소바깥여백-위쪽: 여백값;
  요소바깥여백-오른쪽: 여백값;
  요소바깥여백-아래쪽: 여백값;
  요소바깥여백-왼쪽: 여백값;
}
padding(요소의 내부 여백)
요소의 내부 여백을 지정합니다.
내부 여백은 자식 요소를 감싸는 여백을 의미합니다.

div {
  padding: 20px;
  요소내부여백: 여백값;
}
margin과 같이 한 방향씩 지정할 수 있습니다.

div {
  padding-top: 20px;
  padding-right: 20px;
  padding-bottom: 20px;
  padding-left: 20px;
  요소내부여백-위쪽: 여백값;
  요소내부여백-오른쪽: 여백값;
  요소내부여백-아래쪽: 여백값;
  요소내부여백-왼쪽: 여백값;
}
색상
color(글자 색상)
요소 내용(Text)의 글자 색상을 지정합니다.
정말 많은 입문자가 font-color, text-color로 실수를 합니다만 그런 속성은 없습니다.

div {
  color: red;
  글자색상: 빨강;
}
background(요소 색상)
요소의 배경 색상을 지정합니다.
color는 글자의 색만 지정할 수 있으며, 요소의 (배경)색을 바꾸려면 background-color가 필요합니다.

div {
  background-color: red;
  요소배경: 빨강;
}

```