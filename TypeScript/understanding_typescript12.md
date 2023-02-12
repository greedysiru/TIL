# Understanding TypeScript(12) - Literal Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Literal Types

* 상수에 특정 값이 할당되었을 때 TypeScript는 해당 상수의 Type을 Literal Type으로 취급
  * let의 경우에는 더 넓은 타입으로 추론 됨

```TypeScript
const PIE = 3.14; // const PIE: 3.14

// 반면, let인 경우에는 number로 추론 됨
let PIE = 3.14; // const PIE: number
```



### 활용 예시

```TypeScript
// union type과 literal type을 활용하여 특정 파라미터가 두 고정된 값을 받도록 할 수 있음
const combine = (input1: number | string,input2: number | string. resultConversion: 'as-number' | 'as-text'): number | string => {
  let result;
  // TypeScript는 resultConversion에 두 값만이 올 것임을 알고 있으므로 다른 값과 비교하려하면 Error를 발생 시킴
  if (resultConversion === 'as-number') {
    ...
  }
};
```








# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

