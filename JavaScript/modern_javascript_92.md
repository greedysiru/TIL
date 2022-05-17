# 41장. 타이머



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 41.1 호출 스케줄링

* 호출 스케줄링 : 함수를 일정 시간이 경과된 이후에 호출되도록 하려면, 타이머 함수를 사용
* setTimeout : 일정 시간이 경과된 이후 콜백 함수가 호출되도록 함
* clearTimout : 등록된 타이머를 제거
* setInterval : 일정 시간 마다 콜백 함수가 호출되도록 함
* clearInterval : 등록된 인터벌을 제거
* JavaScript는 하나의 실행 컨텍스트 스택을 가지므로 두 가지 이상의 태스크를 동시에 실행할 수 없음
  * 싱글 스레드로 동작
  * 때문에, 타이머 함수들은 비동기 처리 방식으로 동작



## 41.2 타이머 함수

### 41.2.1 setTImeout / clearTimeout

* setTimeout
  * 두 번째 인수로 전달 받은 수만큼의 밀리 초 이후에 첫 번째 인수로 전달받은 콜백 함수를 한 번 호출
  * 세 번째 인수부터는 콜백 함수에 전달할 인수들을 나열
  * 생성된 타이머를 식별할 수 있는 고유한 타이머 id 반환
* clearTimeout
  * 호출 스케줄링 취소
  * 생성된 타이머 id를 전달받아 타이머 취소

```JavaScript
const cry = () => console.log('야옹');

const customCry = (cry) => console.log('cry');

// 타이머가 완료되면 cry 함수 호출
setTimeout(cry, 1000);

// 타이머가 완료되면 세 번째 인수를 콜백함수에 전달하여 customCry 함수 호출
setTimeout(customCry, 1000, '멍멍');

// 타이머 id를 반환
const timerId = setTimeout(cry, 2000);

// 타이머 id를 전달하여 해당 스케줄링 취소
clearTimeout(timerId);
```



### 41.2.2 setInterval / clearInterval

* setInterval
  * 두 번째 인수로 전달받은 시간으로 첫 번째 인수로 전달받은 콜백함수를 반복 호출하는 타이머 생성
  * 전달할 인수는 setTimeout 함수와 동일
  * 생성된 타이머를 식별할 수 있는 고유한 타이머 id 반환
* clearInterval
  * 호출 스케줄링 취소
  * 생성된 타이머 id를 전달받아 취소

```JavaScript
const cry = () => console.log('야옹');

const customCry = (cry) => console.log('cry');

// 1초마다 cry 함수 호출
setInterval(cry, 1000);

// 세 번째 인수를 콜백함수에 전달하여 1초마다 customCry 함수 호출
setInterval(customCry, 1000, '멍멍');

// 타이머 id를 반환
const timerId = setInterval(cry, 2000);

// 타이머 id를 전달하여 해당 스케줄링 취소
clearInterval(timerId);
```



## 41.3 디바운스와 스로틀

* 이벤트 핸들러가 과도하게 호출된다면 성능에 문제를 일으킬 수 있음
* 디바운스와 스로틀은 연속한 이벤트를 그룹화해서 과도한 이벤트 호출을 방지하는 프로그래밍 기법



### 41.3.1 디바운스

* 짧은 시간 안에 발생한 이벤트를 그룹화해서 마지막에 한 번만 이벤트 핸들러가 호출되도록 함
  * 정의한 딜레이 동안 이벤트가 발생하지 않으면 한 번만 호출
* Ajax 요청과 같은 무거운 처리는 이벤트를 그룹화해서 처리하는 것이 좋음
* Underscore 또는 Lodash의 debounce 사용할 것



### 41.3.2 스로틀

* 짧은 시간 간격으로 연속해서 발생한 이벤트를 그룹화해서 일정 시간 단위로 이벤트 핸들러가 호출되도록 호출 주기를 만듦
  * 정의한 딜레이가 경과하기 이전에 이벤트가 발생해도 아무런 동작을 하지 않음
  * 딜레이가 경과되면, 콜백 함수를 호출하고 새로운 타이머를 재설정
* Underscore 또는 Lodash의 throttle 사용할 것