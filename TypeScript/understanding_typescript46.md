# Understanding TypeScript(46) - Interfaces as Function Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Interfaces as Function Types

* interface로 함수의 구조를 정의
  * 함수 또한 객체이므로 가능

  * 메서드를 정의하는 것과 비슷

  * TypeScript는 익명 함수의 특수 구문을 이해하고 해당 interface를 함수 유형으로 취급



```TypeScript
interface AddFn {
  // 익명 메서드의 형태
  (a: number, b: number): number;
}
// cf) type AddFn = (a: number, b: number) => number;

let add: AddFn;

add = (a: number ,b: number) => a + b;
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

