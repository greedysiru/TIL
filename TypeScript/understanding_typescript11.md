# Understanding TypeScript(11) - Union Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Union Types

* TypeScript에게 여러 타입을 허용토록 하는 Type 정의
* 변수, 함수의 파라미터, 함수의 리턴 등의 타입을 유연하게 정의할 수 있음



### 활용 예시

```TypeScript
// 숫자를 받으면 더하고 문자열을 받으면 합치는 함수
// 각 파라미터는 두 개의 type을 받고 해당 함수는 두 개의 타입을 리턴
const combine = (input1: number | string,input2: number | string): number | string => {
  let result;
  // 각 타입에 대한 분기처리를 하여 TypeScript Error를 해결
  if (typeof input1 === "number" && typeof input2 === "number") {
    result = input1 + input2;
  } else {
    result = input1.toString() + input2.toString();
  }
  return result;
};

const combinedAges = combine(30, 26);
const combinedNames = combine("Max", "Anna");
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

