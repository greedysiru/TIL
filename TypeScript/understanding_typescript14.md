# Understanding TypeScript(14) - Function Return Types & "void"

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Function Return Types & "void"

### return types

* 함수가 어떤 type을 return하는지 명시할 수 있음
  * 또는 TypeScript가 함수의 return type을 추론

```TypeScript
// 아래 함수의 Return type은 TypeScript에 의해 추론 됨
// function add(n1: number, n2: number): number
function add(n1: number, n2: number) {
   return n1 + n2;
}


// return type 할당
function add(n1: number, n2: number): number {
  return n1 + n2;
}

// string을 return type 할당하면 에러 발생
// 숫자끼리 합 연산을 하면 string이 나올리가 없으므로
function add(n1: number, n2: number): string {
  return n1 + n2;
}
```



### void

* 함수가 아무것도 return하지 않을 때의 type
  * 런타임에서는 undefined을 return 하는 경우
  * retrun을 명시하지 않았을 때
  * 또는 return keyword 뒤에 아무것도 쓰지 않았을 때

```TypeScript
// 함수가 아무것도 return하지 않을 때의 type(JavaScript 런타임에서는 undefined)
// 아래 함수는 아무것도 return 하지 않으므로 return type은 void
// function printResult(num: number): void
function printResult(num: number) {
   console.log(num);
}
```



### void vs. undefined

* undefined는 TypeScript의 Type 중 하나
* 공통점
  * 둘 다 런타임에서 undefined를 return
* 차이점
  * void는 return을 명시하지 않아도 됨
  * undefined는 return을 명시해야만 함

```TypeScript
// 함수 return type에 undefined를 명시한 경우, error 가 발생
// void가 아닌 return type은 값을 반환해야 하므로
function printResult(num: number): undefined {
  console.log(num);
  // return을 써줘야 함
  return;
}
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

