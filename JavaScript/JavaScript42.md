# [드림코딩 by 엘리] JavaScript 기초 강의(12) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/596) 참고**



# async & await

* promise를 더 간결하고 간편하게 사용할 수 있다.
  * promise, async & await를 적재적소에서 사용할 것
* 기존의 promise 위에 간단한 API를 제공
  * syntactic sugar
  * JavaScript의 class



## 1. async

### 비동기 처리가 없을 때

```JavaScript
function fetchUser(){
  // 네트워크로부터 받아오는데 10초가 걸리는 요청
  
  return 'siru';
}

const user = fetchUser();
console.log(user); // 비동기처리를 하지 않으면 10초가 걸리므로 뒤의 코드 실행이 지체된다.
```



### Promise로 비동기처리

```JavaScript
function fetchUser(){
  // 네트워크로부터 받아오는데 10초가 걸리는 요청
  
  return new Promise((resolve, reject) => {
    // 아무것도 선언하지 않으면 state는 pending이 된다.
    resolve('siru');
  })
}

const user = fetchUser();
user.then(console.log);
console.log(user);
```



### async

* 함수앞에 붙여주면 된다.

```JavaScript
async function fetchUser(){
  // 네트워크로부터 받아오는데 10초가 걸리는 요청
  
  return 'siru';
}

const user = fetchUser(); // Promise를 return
user.then(console.log);
console.log(user);
```



## 2. await

* await 뒤의 코드가 끝날 때 까지 기다린다.
  * 동기적으로 동작
* try, catch로 에러처리를 할 수 있다.
  * try 안에서 정상 처리
  * catch 안에서 에러 처리

```JavaScript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(3000); 
  // 3초 후에 resolve를 호출하는 promise 전달
  // await가 끝날 때까지 기다린다.
  return 'apple';
}

async function getBanana() {
  await delay(3000);
  return 'banana';
}

// Promise chaining을 많이 쓰면 쓸수록 콜백지옥과 같이 가독성이 떨어지고 복잡해진다.
function pickFruits1() {
  return getApple()
  .then(apple => {
    getBanana()
    .then(banana => `${apple} + ${banana}`);
  })
}

// await를 사용하여 간단하게 할 수 있다.
async function pickFrutis(){
  const apple = await getApple();
  const banana = await getBanana();
  return `${apple} + ${banana}`''
}

pickFruits().then(console.log);
```



## 유용한 Promise APIs

### all

* Promise 배열을 전달하면, 모든 Promise들이 병렬적으로 다 받을 때 까지 모아준다.

```JavaScript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(3000); 
  // 3초 후에 resolve를 호출하는 promise 전달
  // await가 끝날 때까지 기다린다.
  return 'apple';
}

async function getBanana() {
  await delay(3000);
  return 'banana';
}

function pickAllFruits() {
  return Promise.all([getApple(), getBanana()])
  .then(fruits => fruits.join(' + '));
}

pickAllFruits().then(console.log);
```



### race

* 가장 먼저 전달받은 Promise만 전달한다.

```JavaScript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(2000); 
  // await가 끝날 때까지 기다린다.
  return 'apple';
}

async function getBanana() {
  await delay(1000);
  return 'banana';
}

function pickOnlyOne() {
  return Promise.race([getApple(), getBanana()]);
}

// 가장 먼저 return 되는 banana만 전달
pickOnlyOne().then(console.log);
```



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)

