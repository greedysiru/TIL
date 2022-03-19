# 12장 - 함수(4)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수

* IIFE
  * Immediately Invoked Function Expression
* 단 한번만 호출되며 다시 호출될 수 없음
* 익명 함수로 주로 사용
* 그룹 연산자로 반드시 감쌀 것
  * 함수 리터럴을 평가해서 함수 객체를 생성하기 위해
* 값을 반환할 수 있음
* 인수를 전달 가능

```JavaScript
(function () {
  console.log('즉시 실행 함수!');
}()); // 즉시 실행 함수!
```



### 12.7.2 재귀 함수

* 자기 자신을 호출하는 함수
* 함수 내에서 자기 자신을 호출할 때 사용한 식별자는 **함수 이름**
  * 함수 호출은 자동으로 생성된 식별자
* 재귀 함수는 **탈출 조건**을 반드시 만들어야 함
  * 탈출 조건이 없으면 무한 반복에 빠져 스택 오버플로가 발생
* 대부분 반복문으로 구현할 수 있으므로 재귀 함수는 지양할 것

```javascript
function callMyPetManyTimes(n) {
  if (n === 0) {
    return;
  }
  console.log('siru');
  callMyPetManyTimes(n - 1);
}

callMyPetManyTimes(5);
```



### 12.7.3 중첩 함수

* 함수 내부에 정의된 함수
  * 또는 내부 함수라고도 함
  * 외부 함수는 내부 함수를 포함한 함수
* 일반적으로 자신을 포함하는 외부 함수를 돕는 헬퍼 함수 역할을 함

```JavaScript
const introducePet = (petName) => {
  const name = petName;
  
  const makeIntroduceString = () => {
    console.log(`이 친구는 ${name} 입니다.`);
  }
  
  makeIntroduceString();
}

introducePet('siru'); // 이 친구는 siru 입니다.
```





### 12.7.4 콜백 함수

* 함수의 매개변수에 전달되어 실행되는 함수
* 로직을 전달 받아 수행할 수 있어 유연한 구조를 가질 수 있음
* 고차 함수 : 콜백 함수를 전달받은 함수
* 비동기 처리에서 주로 사용
  * 콜백 지옥을 일으키는 단점이 있음

```JavaScript
// api 호출하는 함수가 있다고 할 때, 이 함수는 콜백함수를 넘겨 받아 다음 동작을 실행
api.get('url', function(response) {
  cosnole.log(`이 api의 실행 결과는 ${response} 입니다.`);
})
```



### 12.7.5 순수 함수와 비순수 함수

* 순수 함수 : 어떤 외부 상태에 의존하지 않고 변경 하지 않는 함수
  * 부수 효과가 없음
* 비순수 함수 : 어떤 외부 상태에 의존하고 변경 하는 함수
  * 부수 효과가 있음
* 외부 상태를 변경하면 상태 변화를 추적하기 어려움
* 함수형 프로그래밍
  * 순수 함수와 보조 함수만을 사용하여 불변성을 지향하는 프로그래밍 패러다임
