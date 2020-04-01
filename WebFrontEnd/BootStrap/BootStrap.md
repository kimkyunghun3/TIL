```

--레이아웃--
col-sm : 768px보다 클때
col-md : 970px보다 클때
col-lg : 1170px보다 클때
col-xs : 768px보다 작을때

ex) <div class=:"col-md-4">첫 번째</div>  >> 안에 여러개를 넣어서 조절할 수 있다.(작을 경우 더 작은 기준으로 하도록 설정 가능)
요런식으로 숫자를 정하여 비율을 정할 수 있다.

--콤포넌트--
버튼
<a class="btn btn-default">버튼</a>
default 안에 primary, success, info, warning, danger 을 넣어서 다양한 색깔을 넣을 수 있다.

테이블
<table> </table>
안에 <tr> 속에 <td> 을 넣어서 항목을 넣을 수 있다.

패널
부트스트랩 홈페이지에서 패널을 들어가서 사용한다.
<div class="panel panel-default"> </div> 속에 내용을 넣어서 하면 된다 
panel 속에 paner-heading , panel-body 클래스를 넣어서 지정가능하다.

폼
<ul>
        <li class="form-inline">
            <label for="">아이디 :</label>
            <input type="text" class="form-control">  //form-control 을 통해 폼 수정이 가능하
        </li>
        <li class="form-inline">
            <label for="">비밀번호 :</label>
            <input type="password" class="form-control">
        </li>
        <li class="form-inline">
            <label for="">생년월일 :</label>
            <select name="" id="" class="form-control">   //select을 이용하여 선택할 수 있도록 설
                <option value="">년도</option>
                <option value="">1995</option>
                <option value="">1994</option>
            </select>
            -
            <select name="" id="" class="form-control">
                <option value="">월</option>
                <option value="">01</option>
                <option value="">02</option>
            </select>
            -
            <select name="" id="" class="form-control">
                <option value="">일</option>
                <option value="">30</option>
                <option value="">31</option>
            </select>
        </li>
        <li class="">
            <input type="checkbox">
            <label for="">약관에 동의 하시겠습니까?</label>
        </li>

    </ul>
이렇게 폼을 만들 수 있다.


네비게이션
상단에 네비바를 만들 수 있다.

소스를 받아서 쓰면 된다.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>네비게이션</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
    <script
  src="https://code.jquery.com/jquery-3.4.1.min.js"
  integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo="
  crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>

    <div class="container" style="padding-top: 100px">
        <nav class="navbar navbar-inverse">
            <div class="container-fluid">
                <div class="navbar-header">
                    <!-- 오른쪽 메뉴바 -->
                    <button type="button" class="collapsed navbar-toggle" data-toggle="collapse" data-target="#nav_menu" aria-expanded="false">
                        <span class="sr-only">Toggle navigation</span>
                        <span class="icon-bar"></span> 
                        <span class="icon-bar"></span> 
                        <span class="icon-bar"></span>
                    </button>
                    <a class="navbar-brand" href="#">
                        bootstrap 강의
                    </a>
                </div>
                <div class="collapse navbar-collapse" id="nav_menu">
                    <ul class="nav navbar-nav">
                        <li class="active">
                            <a href="">HTML</a>
                        </li>
                        <li>
                            <a href="">CSS</a>
                        </li>
                        <li>
                            <a href="">PYTHON</a>
                        </li>
                        <li>
                            <a href="">Javascript</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>

    </div>
    
</body>
</html>


```