# 45장. 프로미스(2)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 45.2 프로미스의 생성

* Promise 생성자 함수를 new 연산자와 함께 호출
* 비동기 처리 상태와 처리 결과를 관리하는 객체
* ECMAScript 사양에 정의된 표준 빌트인 객체
* 비동기 처리를 수행할 콜백 함수를 인수로 전달
  * ECMAScript 사양에서는 executor 함수라고 칭함
  * **resolve, reject**
* 비동기 처리가 성공하면 resolve 함수를 호출
* 비동기 처리가 실패하면 reject 함수를 호출
* 프로미스의 상태 정보
  * pending: 비동기 처리가 아직 수행되지 않은 상태(프로미스 생성 직후)
  * fulfilled: 비동기 처리가 수행된 상태(성공, resolve 함수 호출)
  * rejected: 비동기 처리가 수행된 상태(실패, reject 함수 호출)
  * fulfilled, rejected 상태를 settled 상태라고 함

```JavaScript
// 프로미스 생성
const promise = new Promise((resolve, reject) => {
  if (/* 비동기 처리 성공 */) {
    resolve('result');
  } else {
    // 비동기 처리 실패
    reject('failure reason');
  }
});
```



## 45.3 프로미스의 후속 처리 메서드

* 프로미스의 비동기 처리 상태 변화에 따른 후속 처리
* 비동기 처리 상태가 변화하면 후속 처리 메서드에 인수로 처리한 콜백 함수가 선택적으로 호출 됨



### 45.3.1 Promise.prototype.then

* 두 개의 콜백 함수를 인수로 전달받음
* 첫 번째 콜백 함수 : fulfiled 상태가 되면 호출
* 두 번째 콜백 함수 : rejected 상태가 되면 호출



### 45.3.2 Promise.prototype.catch

* 한 개의 콜백 함수를 인수로 전달받음
* 프로미스가 rejected 상태일 때 호출



### 45.3.3 Promise.prototype.finally

* 성공 또는 실패와 상관 없이 무조건 한 번 호출
* 공통 수행 로직을 구현할 때 유용



## 45.4 프로미스의 에러 처리

* 비동기 처리에서 발생한 에러는 Promise.prototype.then 메서드 두 번째 콜백 함수로 처리 가능
  * 첫 번째 콜백 함수에서의 에러를 캐치하지 못하고 가독성이 좋지 않음
* Promise.prototype.catch를 사용하여 에러 핸들링을 할 것



## 45.5 프로미스 체이닝

* 프로미스 객체의 프로토타입 메서드인 then, catch, finally는 프로미스를 반환하므로 연속적으로 호출 가능
* 프로미스 체이닝 또한 콜백 패턴을 사용하므로 가독성이 좋지 않음
  * ES8에서 도입된 async/await를 통해 해결 가능
  * 동기 처리처럼 처리 결과 반환 가능



## 45.6 프로미스의 정적 메서드

### 45.6.1 Promise.resolve / Promise.reject

* 이미 존재하는 값을 래핑하여 프로미스를 생성



### 45.6.2 Promise.all

* 여러 개의 비동기 처리를 모두 병렬 처리할 때 사용
* 배열 등의 이터러블을 인수로 전달받음
  * 각 요소는 프로미스
* 모든 프로미스가 fulfilled 상태가 되면 처리 결과를 배열에 저장해 새로운 프로미스 반환
* 모든 처리를 순차적으로 처리하는 것보다 빠르게 완료 가능



### 45.6.3 Promise.race

* 배열 등의 이터러블을 인수로 전달받음
  * 각 요소는 프로미스
* 가장 먼저 fulfilled 상태가 된 프로미스의 처리 결과를 reslove하는 새로운 프로미스를 반환
* 프로미스가 rejected 상태가 되면 Promise.all 메서드와 동일하게 처리 됨
  * 에러를 reject하는 새로운 프로미스 즉시 반환



### 45.6.4 Promise.allSettled

* 배열 등의 이터러블을 인수로 전달받음
  * 각 요소는 프로미스
* 전달 받은 프로미스가 모두 settled 상태가 되면 처리 결과를 배열로 반환



## 45.7 마이크로태스크 큐

* 태스크 큐와는 별도의 큐
* 프로미스의 후속 처리 메서드의 콜백 함수가 일시 저장
* 그 외의 비동기 함수의 콜백 함수는 태스크 큐에 일시 저장
* 마이크로태스크 큐는 태스크 큐보다 우선순위가 높음
  * 이벤트 루프는 콜스택이 비면 마이크로태스크 큐에서 대기하고 있는 함수를 가져와 실행



### 45.8 fetch

* XMLHttpRequest 객체와 마찬가지로 HTTP 요청 전송 기능을 제공하는 클라이언트 사이드 Web API
* 사용법이 간단
* 대부분의 모던 브라우저에서 제공
* HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환
* fetch가 반환하는 프로미스는 오프라인, CORS 에러에 의해 요청이 완료되지 못한 경우에만 reject
  * 그 외에는 HTTP에러가 일어나도 불리언 타입의 ok 상태를 false로 설정한 Response 객체를 resolve
* aixos는 모든 HTTP에러를 reject하는 프로미스를 반환
  * 모든 에러를 catch에서 처리 가능
  * 인터셉터, 요청 설정 등 다양한 기능 지원

