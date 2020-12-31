---
title: Variable
date: 2020-11-25 22:23:00 +/-TTTT
categories: [Node, Start]
tags: [node,DataTypes]     # TAG names should always be lowercase
---

### Use strict
개발할때 엄격하게 개발하겠다고 선언하는 것임 개발할 때 기초가 되어 좋음

### let(Mutable)
`let`ES6에서 추가된 문법  
![javascriptBasicImage](/Sunjae95.github.io/assets/img/start/javascriptBasic.png){: width="360" .normal}  
```javascript
let name = 'seonjae';
console.log(name);  //seonjae
```    
어플리케이션을 실행하면 메모리가 할당되는데 방금 나는 `let`이라는 키워드를 통해 name이라는 변수를 생성하면, name은 그림과 같이 어떠한 블록을 가리키게 된다. 박스에는 'seonjae'라는 값이 있지만 공백이든 다른 값을 넣어서 바꿀 수도 있다.  

   
또한 `let` EC6이전의 `var`와 같은 기능이기에 `var`로 정의되어있다면 `let`으로 사용하는 것을 추천한다.
  
왜냐하면 `var`는 선언하기도 전에 쓸수있기때문에 어디에서든 선언해도 호출된다. 또한 `Block scope`를 무시하기 때문에 아무리 `Block`안에 선언되도 전역에서 호출도 가능하다.  

### Block scope
 ```javascript
 let globalName = 'global name';
 {
    let name = 'seonjae';
    console.log(name);  //seonjae
 }
console.log(name);  //seonjae   하지만 이 줄은 공백으로 나옴
```  
`Block scope`는 `Block`내에서만 작동하는것이라 생각하면된다. 그래서 `Block`내에서 선언한 변수는 전역에서는 사용할 수가 없다.  
  
**밖에서는 안이 보이지 않고, 안에서만 밖을 볼 수 있다.**
  
`global변수`는 어플리케이션이 실행되고 종료될때까지 유지되기 때문에 개발시 최소한으로 사용하는것이 좋다.
  
### Constants(Immutable)
![javascriptBasicImage](/Sunjae95.github.io/assets/img/start/javascriptBasic2.png){: width="360" .normal}  
`const` 값을 선언한 다음에는 값을 못바꾼다.   
- `const`를 사용하는 이유  
1. 보안때문에 해커들이 혹시 변수를 바꿔서 침입불가
2. 스레드에서 값을 변경할 경우가 있는데 동시에 스레드가 값을 변경 위험
3. 나중에 코드 변경시 실수를 방지
  
### Symbol  
고유한 식별자가 필요하면 사용한다. 보통 식별자를 `string`타입으로 선언하는데 이렇게 하면 다른 식별자가 똑같은 `string`이면 같다고 나올 수 있기 때문에 `symbol`을 사용한다.  

```javascript
const symbol1 = Symbol('id');
const symbol2 = Symbol('id');
console.log(symbol1 === symbol2);  //false
```
  
### Dynamic typing  
다음은 javascript의 유연성을 보여주는 예시이다.  
주의하면서 변수 선언하고 사용을 해야된다.  
```javascript
let text = 'hello';
console.log(`value: ${text}, type: ${typeof text}`);    //value: hello, type: string
text = 1;
console.log(`value: ${text}, type: ${typeof text}`);    //value: 1, type: number
text = '7' + 5;
console.log(`value: ${text}, type: ${typeof text}`);    //value: 75, type: string
text = '8' / '2';
console.log(`value: ${text}, type: ${typeof text}`);    //value: 4, type: number
```
>**참조**  
><https://www.youtube.com/watch?v=OCCpGh4ujb8&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=3L>