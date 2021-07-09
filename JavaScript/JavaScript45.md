# [얄팍한 코딩사전] 비동기 프로그래밍

**상세 내용 [블로그](https://greedysiru.tistory.com/599) 참고**



# 1. Synchronous vs. Asynchronous

## Synchronous 

> **코드가 작성된 순서대로 각 작업이 마무리 되는대로 실행**

* 각 작업이 마무리될때까지 기다려야 한다.
* 뒤의 작업이 지체된다.



## Asynchronous

> **코드가 작성된 순서대로 각 작업을 기다리지 않고 실행**

* 쓰레드와 프로세스가 여럿이 돌고 있는 것
* 멀티태스킹



## JavaScript의 Asynchronous

```JavaScript
function asyncBlackBeanEaters (name) {
  console.log(`${name}에게 배달`);
  
  http.get("http://localhost:3000/eat-noodle-rand",
    function (){
    console.log(`${name} 식사 완료`);
  }
 );
}

let eaters = ['유민상', '김준현', '문세윤', '김민경', '돈스파이크'];
for (let i = 0; i < eaters.length; i++){
  asyncBlackBeanEaters(eaters[i]);
}
```

| 동기 실행이라면                                              | 실제 실행(비동기 실행)                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| > 유민상에게 배달<br />> 유민상 식사 완료<br />> 김준현에게 배달<br />> 김준현 식사 완료<br />> 문세윤에게 배달<br />> 문세윤 식사 완료<br />> 김민경에게 배달<br />> 김민경 식사 완료<br />> 돈스파이크에게 배달<br />> 돈스파이크 식사 완료 | > 유민상에게 배달<br />> 김준현에게 배달<br />> 문세윤에게 배달<br />> 김민경에게 배달<br />> 돈스파이크에게 배달<br />> 콜백함수들이 서버에서 응답받은 순서애 따라 무작위로 식사완료 출력 |



### why?

* JavaScript는 웹 브라우저나 Node.js의 JavaScript 엔진에서 실행된다.
  * JavaScript를 돌리는 하나의 쓰레드
  * **함수는 나중에 실행된 것이 먼저 실행되는 스택**
  * 다른 포함 레벨의 함수들이 처리되는 순서는 역순
  * 같은 포함레벨에서의 함수들은 순서대로 처리
* JavaScript가 도는 환경에는 JavaScript 엔진 뿐만아니라 Web API가 함께 동작
  * Web API: 타이머, AJAX, 파일 데이터 읽기, 시간을 소요하는 작업들을 수행
  * Web API가 처리하는 태스크는 브라우저나 Node.js가 비동기 처리로 보낸다.
  * 비동기 처리가 끝난대로 테스크의 콜백함수들은 Task Queue로 보내진다.
  * 이벤트 루프가 콜백함수들을 JavaScript에서 실행되도록 한다.
  * 시간이 걸리는 작업을 비동기 처리하면 브라우저 화면이 버벅거리는 것을 방지한다.



# 2. Promise

* ES6에 도입
* 비동기 처리를 위한 Callback hell 방지
* 각 비동기 작업을 마치면 then으로 순차 작업을 할 수 있다.
  * 비동기 작업을 동기 작업처럼



# 3. async await

* Promise를 쉽게 다룰 수 있는 문법적 설탕
* 함수 선언 앞에 **async** 키워드를 붙이고 동기 작업을 할 부분 앞에 **await** 를 붙이기



# Reference

[비동기 프로그래밍](https://www.youtube.com/watch?v=m0icCqHY39U)