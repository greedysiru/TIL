# 46장. 제너레이터와 async/await(1)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 46.1 제너레이터란?

* 코드 블록의 실행을 일시 중지 했다가 필요한 시점에 재개할 수 있는 특수한 함수



### 일반 함수와의 차이

1. 함수 호출자에게 함수 실행의 제어권을 양도 가능
   - 일반 함수는 제어권이 함수에게 있음
   - 제네레이터는 함수 호출자가 함수 실행을 일시 중지 또는 재개 가능
   - **함수 호출자에게 제어권을 양도(yield)**
2. 함수 호출자와 함수의 상태를 주고받을 수 있음
   - 일반 함수는 외부에서 값을 주입 받아 결과 값을 외부로 반환
   - 제너레이터는 함수 호출자에게 상태를 전달할 수 있고 받을 수도 있음
3. 제너레이터 함수를 호출하면 제너라이터 객체를 반환
   - 이터러블이면서 동시에 이터레이터인 제너레이터 객체를 반환



## 46.2 제너레이터 함수의 정의

* **function*** 키워드로 선언
  * function 키워드와 함수 이름 사이면 어디든지 상관없음
* 하나 이상의 yield 표현식 포함

```JavaScript
function* gene() {
  yield 1;
}
```



## 46.3 제너레이터 객체

* 제너레이터 함수를 호출하면 제너레이터 객체를 생성해 반환
  * 제너레이터 객체는 이터러블이면서 이터레이터
  * 제너레이터 : Symbol.itertator 메서드를 상속받는 이터러블
  * 이터레이터 : 이터레이터 리절트 객체를 반환
* return, throw 메서드를 가짐
* return 메서드
  * 인수로 전달받은 값을 value 프로퍼티 값으로, done 프로퍼티를 true로 갖는 이터레이터 리절트 객체를 반환



## 46.4 제너레이터의 일시 중지와 재개

* 제너레이터는 yield 키워드와 next 메서드를 통해 실행을 일시 중지했다가 필요한 시점에 다시 재개 가능
* 코드 블록의 yield 표현식까지만 실행
* yield
  * 제너레이터 함수의 실행을 일시 중지
  * 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환
* next 메서드
  * yield 표현식까지 실행되고 이터레이터 리절트 객체 반환
  * 이터레이터 리절트 객체의 value는 yield된 값이 할당
  * 전달한 인수는 yield 표현식을 할당받는 변수에 할당

```JavaScript
function* gen() {
  yield 1;
  yield 2;
}

const generator = gen();

console.log(generator.next()); // {value: 1, done: false}
console.log(generator.next()); // {value: 2, done: false}
console.log(generator.next()); // {value: undefined, done: true}
```



## 46.5 async/await

* ES8
* 가독성 좋게 비동기 처리를 동기 처리처럼 동작하도록 구현하도록 도입
* await 키워드는 만드시 async 함수 내부에서 사용
* async 함수는 언제나 프로미스를 반환
* 클래스의 constructor 메서드는 async 메서드가 될 수 없음
  * 인스턴스를 반환해야 하므로
* await
  * settled상태가 되면 프로미스가 reslove한 처리 결과 반환
* 병렬적으로 비동기 처리를 하는 경우에는 Promise.all을 활용
* try, catch 문을 사용하여 에러 핸들링 가능
  * HTTP 통신에서 발생한 네트워크 에러
  * try 코드 블록 내의 모든 문에서 발생한 일반 에러

```JavaScript
const asyncFunc = async () => {
  try {
     const res = await fetch('https://amazingsite.co.kr/cats');
		  return res; 
  } catch(error) {
    console.log(error);
  }
};

```

