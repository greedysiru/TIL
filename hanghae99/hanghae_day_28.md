# [항해99 1기] [Chapter3-2] 주특기 심화 - 리액트 심화반 (3) (2021.3.28)



#  Promise

* 자바스크립트는 싱글 쓰레드로 동작하는 언어이다.
  * 메인 쓰레드와 콜스택 하나
* 코어 엔진과 실행환경(런타임)의 도움을 받아 비동기 작업을 동시에 할 수 있다.
  * WebAPI(dom, ajax, setTimeout), Task Queue, Event Loop



## 1. 콜백

* 자바스크립트가 비동기 처리를 하기 위한 패턴 중 하나
  * 그러나, 콜백 헬로 불리는 중첩 문제를 일으킬 수 있다.
* 콜백 헬
  * 비동기 처리 시에는 실행 완료를 기다리지 않고 다음 작업을 실행
  * 비동기 처리 함수 내에서 처리 결과를 반환하는 것으로 원하는 동작을 하지 않을 경우 콜백 함수를 사용한다.
  * 콜백 함수 내에서 또 다른 비동기 작업이 필요한 경우 중첩이 생기게 된다.



## 2. Promise

* 비동기 연산이 종료된 이후 결과를 알기 위해서 사용하는 객체
* 비동기 메소드 -> 동기 메소드처럼 값을 반환
* ES6에서 도입한 비동기 처리 패턴
* 비동기 처리 시점을 명확하게 표현



## 3. Promise 생성

* 생성자 함수를 통해 생성
* 비동기 작업을 수행할 콜백 함수를 인자로 전달 받아서 사용
* resolve, reject: excutor 실행자(실행 함수)
  * resolve: 작업이 성공한 경우 호출할 콜백
  * reject: 작업이 실패한 경우 호출할 콜백

```JavaScript
// Promise 객체
const promise = new Promise ((resolve, reject) => {
  if (...) {
      ...
      resolve('성공');
      } else{
      ...
      resolve('실패');
}
});
```



## 4. Promise의 상태값

* pending: 비동기 처리 수행 전 (resolve, reject가 아직 호출되지 않음)
* fulfilled:  수행 성공(resolve가 호출)
* rejected: 수행 실패(reject가 호출)
* settled: 성공 or 실패(resolve나 reject가 호출된 상태)



## 5. Promise 후속 처리 메소드

* Promise로 구현된 비동기 함수는 Promise 객체를 반환
* Promise로 구현된 비동기 함수를 호출하는 측에서는 Promise 객체의 후속 처리 메소드를 통해 비동기 처리 결과(성공 결과나 에러메시지)를 받아서 처리해야 한다.
* **.then(성공 시, 실패 시)**
  * 첫 인자는 성공 시 실행, 두번째 인자는 실패 시 실행
* **.catch(실패 시)**

```JavaScript
// Promise1
let promise1 = new Promise((resolve, reject) => {
	setTimeout(() => resolve("완료"), 1000);
});

// resolve
promise.then(result => {
	console.log(result); // 완료
}, error => 류
	console.log(error); // 실행되지 않는다.
});


// Promise2
let promise2 = new Promise((resolve, reject) => {
	setTimeout(() => reject(new Error("오류")), 1000);
});

// reject
promise.then(result => {
	console.log(result); // 실행되지 않는다.
}, error => {
	console.log(error); // Error: 오류
});

// Promise3 - catch
let promise = new Promise((resolve, reject) => {
	setTimeout(() => reject(new Error("오류!"), 1000);
});

promise.catch((error) => {console.log(error};);
```



## 6. Promise chaining

* Promise에 후속 처리 메소드를 chaining 해서 여러개의 Promise를 연결할 수 있다.
  * 콜백 헬 해결

```JavaScript
new Promise((resolve, reject) => {
	setTimeout(() => resolve("promise 1"), 1000);
}).then((result) => { // 후속 처리 메서드 하나
	console.log(result); // promise 1
	return "promise 2";
}).then((result) => { // 연달아 then으로 이어주기
	console.log(result);
	return "promise 3";
}).then(...);
```



## 7. async, await

### async

* 함수 앞에 async를 붙여서 사용
* 항상 Promise를 반환
  * Promise가 아니어도 Promise로 감싸서 반환

```JavaScript
// async는 function 앞에 쓴다.
async function myFunc(){
  return 'Promise return';
}

myFunc().then(result => {console.log(result)});
```



### await

* async와 함께 사용
* 함수 안에서만 동작
* awiat는 Promise가 처리될 때가지 기다리고 이후에 결과를 반환

```JavaScript
async function myFunc(){
	let promise = new Promise((resolve, reject) => {
		setTimeout(() => resolve("완료"), 1000);
	});

    console.log(promise);

	let result = await promise; // 여기서 기다린다.

    console.log(promise);

	console.log(result); // then(후처리 함수)를 쓰지 않았는데도, 1초 후에 "완료"가 콘솔에 찍힌다
}
```



# Reference

[스파르타코딩클럽 리액트 심화반](https://spartacodingclub.kr/online/react/plus)

