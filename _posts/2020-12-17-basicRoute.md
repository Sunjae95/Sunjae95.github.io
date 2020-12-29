---
title: Basic Route
date: 2020-12-17 16:30:00 +/-TTTT
categories: [Node, Start]
tags: [node]     # TAG names should always be lowercase
---
## 기본라우팅
---

URI(또는 경로) 및 특정한 HTTP 요청 메소드(GET, POST 등)인 특정 엔드포인트에 대한 클라이언트 요청에 
애플리케이션이 응답하는 방법을 결정하는 것을 말합니다<br>
각 라우트는 하나 이상의 핸들러 함수를 가질 수 있으며, 이러한 함수는 라우트가 일치할 때 실행됩니다

---
```javascript
app.METHOD(PATH,HANDLER);
```

METHOD => HTTP 요청 메소드(get, post, put, send)<br> 
PATH => 경로 지정 / 만약 path안에 `$`를  넣고 싶으면 `([\$])`라고 해야됨<br>
HANDLER => 일치할때 실행되는 함수<br> 
```javascript
//Example root/app.js
let express = require('express')
let app = express()

app.get('/',(req,res)=>{
  res.send('hi')
})

app.listen(3000,(req,res)=>{
    console.log('ok');
})
```
실행<br>
![ex](/assets/img/sample/routeExampleRun.JPG){: width="400" class="normal"}<br>
결과<br>
![ex](/assets/img/sample/routeExample.JPG){: width="200" class="normal"}


---

>**참조**<br>
><https://expressjs.com/en/guide/routing.html>