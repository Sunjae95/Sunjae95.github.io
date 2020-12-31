---
title: 비동기
date: 2020-11-28 22:23:00 +/-TTTT
categories: [Node, Start]
tags: [node,asyncAwait]     # TAG names should always be lowercase
---
### async await
`async await`는 `Promise`를 좀 더 간편하고 동기적으로 실행 하는것 처럼 보여준다. `async await`는 `Promise`에 API를 사용했다고 봐도 무방하다. `Promise`같은 경우 chaining을 하게 되다보면 복잡해질수있기 때문에 `async await`를 사용한다. 그렇다고 해서 무조건 `async await`를 쓰면 안된다. `Promise`를 쓰는 것은 유지하고 만약 복잡하거나 깔끔하게 하려면 `async await`를 사용하면 된다.

### async
```javascript
//10초동안 걸리는 함수가 있는 경우 Promise를 활용하여 처리하였음
async function fetchUser(){   //async키워드를 사용하면 Promise로 바뀐다고 생각하면된다.
    //do network reqeust in 10secs...
    return 'seonjae';
}
const user = fetchUser();
console.log(user);
```

### await
```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}
async function getApple() {     //3초후 리턴한다.
    await delay(3000);
    return '🍎';
}
async function getBanana() {
    await delay(3000);
    return '🍌';
}
async function pickFruits() {
    const apple = await getApple();     
    const banana = await getBanana();
    return `${apple} + ${banana}`;
} 
pickFruits().then(console.log);     //🍎 + 🍌
```  
### 병렬처리
```javascript
//1.각각 Promise 선언
async function pickFruits() {
    try{        //이렇게 하면 apple 3초 banana 3초 총 6초가 걸린다. 
    const applePromise = getApple();
    const bananaPromise = getBanana();
    const apple = await applePromise;     
    const banana = await bananaPromise;
    } catch
    return `${apple} + ${banana}`;
} 
//만약 병렬 처리시 위의 예처럼 둘다 실행시에 연관이 없는것이면 Promise API를 사용
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);

//먼저 받아지는걸 받고싶으면 
function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}
pickOnlyOne().then(console.log);
```  

>**참조**<br>
><https://www.youtube.com/watch?v=aoQSOZfz3vQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=13>