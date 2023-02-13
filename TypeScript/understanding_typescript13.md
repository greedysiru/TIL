# Understanding TypeScript(13) - Type Aliases / Custom Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Type Aliases / Custom Types

### Type keword

* TypeScript의 keyword
* Type을 선언하고 할당
* Type을 변수처럼 재활용할 수 있음
* 복잡한 타입을 사용해야할 때 유용
* 원시타입, 리터럴 타입, 커스텀 타입 모두 가능

```TypeScript
type Combinalbe = number | string;
type ConversionDescriptor = "as-number" | "as-text";

const combine = (
  input1: Combinalbe,
  input2: Combinalbe,
  resultConversion: ConversionDescriptor
): number | string => {
  let result;
  if (
    (typeof input1 === "number" && typeof input2 === "number") ||
    resultConversion === "as-number"
  ) {
    result = Number(input1) + Number(input2);
  } else {
    result = input1.toString() + input2.toString();
  }
  return result;
};
```



### Obejct Type Alias

* Object 또한 Type Alias 할당이 가능

```TypeScript
type Cat = {
  name: string,
  age: number,
  isVaccinated: boolean;
}

const siru: Cat = {
  name: 'siru',
  age: 8,
  isVaccinated: true,
}
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

