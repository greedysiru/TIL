# Understanding TypeScript(15) - Function as Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Function as Types

### Function Type

* TypeScript Built-in Type

```TypeScript
const add = (n1: number, n2: number): number => {
  return n1 + n2;
}

const printResult = (num: number): void => {
  console.log(num);
  return;
}

// Function Type
// combineValues 에는 함수들을 할당할 수 있게 됨
let combineValues: Function;

combineValues = add;
combineValues = printResult;
```



### Special Function Type

* 특수한 함수 타입을 정의할 수 있음
  * Type Alias도 가능

```TypeScript
// 명시적인 함수 타입 할당
let combineValues: (a: number, b: number) => number;

// add 함수는 combineValues의 함수 타입과 일치하여 할당 가능
combineValues = add;
// error, printResults는 combineValues와 일치하지 않아 할당 불가
combineValues = printResult
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

