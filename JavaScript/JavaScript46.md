# 프론트엔드의 비동기

**본 내용은 10분 테코톡 카일님의 강의를 토대로 작성하였습니다.**



## 1. 비동기는 왜 나타났고 왜 처리해야할까

### 비동기

* 사용자와의 연속적인 상호작용을 처리하여 변경된 정보를 실시간으로 보여줘야 한다.
* 모든 상호작용을 동기적으로 처리하면 사용자가 대기해야하는 시간이 생긴다.
* 코드를 비동기적으로 처리하는 것은 프론트엔드 영역에서 필수



## 2. CallBack

* 비동기 처리 방식

### 문제1. 신뢰성

* **제어의 역전(Inversion Of Contral)**
  * 아래와 같은 이유로 버그가 발생할 수 있다.
  * 필요한 데이터를 콜백에 전달 했는지
  * 호출 시점(빠르거나 느리거나)
  * 호출 횟수

```JavaScript
function browserTasks() {
  // 제어 대상
  console.log('sync task');
  asyncRequest(asyncTask);
}

function asyncRequest(callBackFn){
  // 비동기 요청과 함께 전달된 콜백은 외부 라이브러리에 대한 의존성을 가지게 되어 제어할 수가 없음
  ajax('url', function (data){
    callBackFn(data);
  });
}

function asyncTask(data) {
  console.log(data);
}
```



### 문제 2. 가독성

* 비동기 자체의 한계로, 사람의 사고방식과 다른 흐름으로 인해 가독성이 떨어짐
* 디버깅 작업이 어려움



## 3. Promise

* ES6
* 미래에 값을 반환할 수도 있는 함수를 캡슐화한 객체
* **제어의 재역전**
  * 외부 라이브러리에 콜백함수를 넘기지 않고 결과를 받아와 직접 처리할 수 있음
* 비동기 요청 수행에 대한 세 가지(성공, 실패, 대기)의 상태를 가지고 있다.
* 내부에서 비동기 요청이 끝나고 나면 결과값을 연결된 콜백으로 보내준다.

```JavaScript
function request(){
  // Executor Function
  // resolve, reject: 비동기 요청 수행 결과에따라 데이터를 넘겨줄 콜백
  // Promise 객체가 만들어지는 즉시 실행
  return new Promise(function (resolve, reject) {
    ajax('url', function (data) {
      if (data) {
        resolve(data);
      } else {
        reject('Error');
      }
    });
  });
}

function asyncTask(){
  const Promise = request();
  
  // then, catch: 데이터를 넘겨받을 콜백함수를 연결
  promise
  	.then(function (data) {
    // 받아온 data를 이용한 작업 수행
  })
  	.catch(function (error) {
    // 받아온 error를 이용한 예외 처리
  });
}
```



### 장점과 단점

| 장점                                                         | 고려할 점                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 제어권을 확보하여 콜백 방식에서 신뢰할 수 없었던 여러 상황을 대처<br />체이닝을 통해 구조화된 콜백 작성 | Promise 객체 외부에서 Promise 내의 연쇄적인 흐름에 대한 예외처리가 어려움<br />단일 값 전달의 한계로, 여러 개의 값이 연관성이 부족해도 배열 또는 객체로 감싸야 함<br />단순 콜백 처리와 비교했을 때 성능 저하 |



## 4. Generator

* 비동기를 동기처럼
  * **외부의 값을 기다렸다가 받은 시점에서 함수를 실행**
* ES6
* *****: generator 함수를 작성하기 위한 규칙. function 키워드 뒤 또는 식별자 앞에 선언
* Iterator: generator 호출로 반환된 객체. next()를 가짐
* next(): generator 함수 안의 yield 문으로 넘어가는 메소드
* yield: next()가 호출 되면, 중간에 멈추고 데이터를 받는 지점

```Javascript
function *asyncTask() {
  // 4. 받아온 값을 ㄴ허고 함수를 다시 진행
  const data = yiled request();
  // 받아온 data를 이용한 작업 수행
}

function request() {
  ajax('url', function(data) {
    // 3. 비동기 요청을 마치고 값을 받아옴
    it.next(data);
  });
}

// 1. generator 함수 호출
const it = asyncTask();

// 2. 연결된 함수 로직을 수행하다가 yiled 문 뒤 request()를 호출하고 함수 중단
it.next();
```



## 5. Async Function

* ES2017
* Syntatic Sugar
* 함수 내에서 await 문을 만나면 함수의 실행을 일시 중지
* await 뒤에 있는 프로미스의 수행 결과 값을 받아 함수 재진행
* promise, Generator 매커니즘을 차용하면서 가독성을 높임

```JavaScript
async function asyncTask(){
  // await뒤의 주체가 Promise일때만 기다림
  const data = await request();
  // 받아온 data를 이용한 작업 수행
}

function request() {
  return new Promise(resolve => {
    ajax('url', function (data) {
      resolve(data);
    });
  });
}
```



### 장점과 단점

| 장점                                                         | 고려할 점                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| await를 통해 반환 받은 것이 Promise의 수행된 값이므로 외부에서 예외처리하기 용이<br />높은 가독성 | Promise에대한 선행 이해<br />하나의 함수 안에서 다수의 Promise를 병렬적으로 처리할 수 없음<br />경우에 따라 async 키워드를 관련 함수마다 일일이 선언해야 함 |



# Reference

[[10분 테코톡] 카일의 프론트엔드의 비동기](https://www.youtube.com/watch?v=fsmekO1fQcw&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=4)