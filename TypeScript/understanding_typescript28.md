# Understanding TypeScript(28) - Code Quality Options

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Code Quality Options

* 코드 퀄리티를 위한 옵션들
* noUnusedLocals
* noUnusedParameters
* noImplicitReturns
* noFallthroughCasesInSwitch: switch문에서 break 키워드 누락을 체크



### noUnusedLocals

* 사용되지 않은 지역변수가 있는지 체크
* 전역변수의 경우 사용되지 않아도 허용

```TypeScript
function foo() {
  // some 변수는 사용되지 않아 Error 발생
  let some = 'Hi';
  
  console.log('this is function');
}
```



### noUnusedParameters

* 사용되지 않은 함수 파라미터를 체크

```TypeScript
// some 파라미터가 사용되지 않아 Error 발생
function foo(some: string) {
  console.log('this is function');
}
```



### noImplicitReturns

* 함수가 명시적으로 return을 해야함

```TypeScript
function add(n1: number, n2: number) {
  // 특정 조건에서만 return을 하고 있으므로 Error 발생
  // 모든 케이스에서 return 할 수 있도록 해야 함
  if (n1 + n2 > 0) {
    return n1 + n2;
  }
} 
```





# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

