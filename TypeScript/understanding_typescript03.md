# Understanding TypeScript(3) - 타입 사용하기

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## 타입 사용하기

### Primitive Types

* TypeScript의 Primitive Types는 lowercase
* number: 실수와 정수 구분 없는 숫자
  * ex) 1, 5.3, -10
* string: 문자열
  * 'james', 'siru'
* boolean: true, false
  * JavaScript의 truthy, falsy는 아님



### type 지정하기

* `:type`의 형식으로 type을 지정

```TypeScript
const add = (num1: number, num2: number) => num1 + num2;
```



### TypeScript의 특징

* type system을 통해 런타임 에러를 방지할 수 있음
  * VSC와 같은 modern IDE와 같은 경우, TypeScript Error를 표시해 줌
* type system은 컴파일 전에 type check를 함
* 런타임에 관여하지 않음
* 브라우저는 TypeScript를 이해할 수 없어 JavaScript로 컴파일하는 과정이 필요



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

