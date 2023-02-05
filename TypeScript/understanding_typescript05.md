# Understanding TypeScript(5) - Type Assignment & Type Inference

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Type Assignment & Type Inference

### Type Assignment

* 타입을 지정하는 것

```TypeScript
const add = (num1: number, num2: number) => num1 + num2;
```



### Type Inference

* TypeScript가 타입을 추론하는 것
* 변수가 초기화된 시점에 무엇이 할당되었는지에 따라 추론됨

```TypeScript
const specialNumber = 5; // 해당 변수의 타입을 5로 추론

// const가 아니라, let의 경우 TypeScript는 다르게 추론
let someNumber = 5; // number 타입으로 추론
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

