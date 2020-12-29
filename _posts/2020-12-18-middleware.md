---
title: 미들웨어 작성
date: 2020-12-17 16:30:00 +/-TTTT
categories: [Node, Start]
tags: [node,middleware]     # TAG names should always be lowercase
---
#### 미들웨어함수 
`req(요청객체)`, `res(응답객체)`, `next 요청-응답 사이클`에 있는 함수에  접근 가능한 함수를 말한다.

#### 미들웨어
클라이언트에게 `요청`이 오고 그 요청을 보내기 위해 `응답`하려는 중간(미들) `목적`에 맞게 처리하여 거쳐가는 함수들이라고 생각하면 된다.

#### 기능 수행
- 코드 실행
- 요청과 응답객체 변경
- 요청-응답 사이클 종료
- 스택에 다음 미들웨어를 호출

#### 호출요소
![ex](/assets/img/sample/middlewarefunction.JPG)<br>

### 간단한 로그 메시지 인쇄 호출
```javascript
let express = require('express')
let app = express()

let myLogger=(req,res,next)=>{
  console.log('LOGGED');
  next();
}

app.use(myLogger);

app.get('/',(req,res)=>{
  res.send('hi')
})

app.listen(3000,(req,res)=>{
    console.log('ok');
})
```
#### 결과
![ex](/assets/img/sample/logMessageCall.JPG){: width="500" class="normal"}

앱이 요청을 받을 때마다 "LOGGED" 메시지를 단말기에 출력하는 예제이다.<br>
미들웨어는 먼저로드 된 미들웨어 함수가 먼저 실행된다.<br>
앱을 실행 후 locallhost:3000을 인터넷에 `호출하지 않는다면` "LOGGED" 메시지가 영원히 console 창에 `인쇄되지 않을` 것이다.<br>
하지만 인터넷에 localhost:3000을 `호출을 한다면` "LOGGED"메시지는 호출을 할 때 마다 console 창에 `인쇄될` 것이다.<br>

### validateCookies

---
>**참조**<br>
><https://expressjs.com/ko/guide/writing-middleware.html>
><https://psyhm.tistory.com/8>