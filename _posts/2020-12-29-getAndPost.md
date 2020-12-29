---
title: Get and Post
date: 2020-12-29 17:36:00 +/-TTTT
categories: [Node, Start]
tags: [node,http]     # TAG names should always be lowercase
---

#### HTTP
HTTP란 클라이언트와 서버 사이에 이루어지는 요청/응답 프로토콜이다.
예를들어 클라이언트가 서버에 정보를 요청하면 서버는 요청에 응답하여 필요한 정보를 사용자에게 전달하는것이다.

#### GET
클라이언트가 서버로 부터 정보를 조회하기 위해 설계된 메소드이다.
보통 GET요청을 전송할 때 데이터를 Body에 담지 않고, 쿼리스트링을 통해 전송한다.<br>

EX<br>
파일구조<br>
![getImage](/assets/img/node/getLogin3.PNG)<br>
routes-index.js 에서 서버에 현재 있는 위치에서  GET메소드를 통해 불러옴<br>
![getImage](/assets/img/node/getLogin2.JPG)<br>
결과<br>
현재는 빈칸이지만 GET메소드를 사용할 시 빨간표시된곳에 쿼리문을 삽이하여 원하는 정보를 골라서 받아올수있다.<br>
![getImage](/assets/img/node/getLogin.JPG)<br>





#### POST
리소스를 생성/변경하기 위해 설계 되었고 GET과 달리 전송해야될 데이터를 HTTP메시지에 Body에 담아서 전송한다. 보통 길이의 제한없이 데이터를 전송할 수있다. 그래서 POST는 GET과 달리 대용량 데이터를 전송할 수 있다.

EX<br>
views/register.ejs 저장 버튼을 누르면 (원래도메인)/register/check로 넘어가게된다.<br>
```html
<!DOCTYPE html>
<head>
    <title><%= title %></title>
</head>
<body>
    <h1>Register</h1>
    <form action="/register/check" method="POST">
        ID<br>
        <input type="text" name="id" placeholder="id input"><br>
        Password<br>
        <input type="password" name="password" placeholder="password input"><br>            
        <input type="submit" id="save" value="저장" >
        <input type="button" value="취소" onclick="history.go(-1)"><br>
    </form>
</body>
```
routes/register.js router를 통해 register/check에 걸리면 화면에 body를 출력하라는 코드 
```javascript
router.post('/check',(req,res)=>{
    res.send(req.body);
});
```
결과<br>

![getImage](/assets/img/node/postRegster.JPG)<br>{: width="240" .left}
↓변경<br>
![getImage](/assets/img/node/postRegster2.JPG)<br>{: width="240" .right}

<br>
>**참조**<br>
><https://ko.wikipedia.org/wiki/HTTP><br>
><https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/>