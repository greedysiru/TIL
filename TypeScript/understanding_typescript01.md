# Understanding TypeScript(1) - 타입스크립트란, 타입스크립트를 사용하는 이유

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## 타입스크립트란

* JavaScript의 Sueprset
  * JavaScipt에 새 기능과 이점을 더함
  * **Type**
  * 런타임 에러를 방지할 수 있는 기회를 제공
* JavaScript 실행 환경에서 동작하지는 않음
  * Browser, Node.js
* TypeScript 컴파일러에 의해 JavaScript로 컴파일
  * TypeScript의 기능은 TypeScript 컴파일러에 의해 JavaScript의 문법으로 바뀜



## 타입스크립트를 사용하는 이유

* JavaScript는 암묵적 타입변환으로 인해 원하지 않은 동작을 실행할 위험이 있음
* JavaScript는 이런 위험 대해 아무런 신호를 주지 않음

```JavaScript
// 해당 함수는 두 수를 더함
const sum = (num1, num2) => num1 + num2;

// 함수의 의도대로 동작한 경우
sum(1, 2); // 3

// 암묵적 타입 변환으로 인해 런타임에서 함수의 의도대로 동작하지 않은 경우
sum('1', '2'); // '12'
```



* 위와 같은 상황을 방지하기 위해 함수에 올바른 타입이 들어가도록 해야 함
  * TypeScript의 Type이 이를 해결
  * 올바르지 않은 타입의 매개변수를 전달하면 에러 발생

```TypeScript
const sum = (num1: number, num2: number) => num1 + num2;

sum(1, 2); // 3

sum('1', '2'); // Argument of type 'string' is not assignable to parameter of type 'number'.(2345)
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

