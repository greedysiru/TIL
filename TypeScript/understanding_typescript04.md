# Understanding TypeScript(4) - TypeScript Types vs JavaScript Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## TypeScript Types vs JavaScript Types

* JavaScript는 dynamically typed
  * 변수를 숫자로 초기화 하였더라도 그 이후에 다른 타입으로 할당할 수 있음
* TypeScript는 statically typed
  * 변수의 타입을 정해야 함
  * 변수의 타입을 도중에 변경할 수 없음
* typeof 연산자를 사용하여 JavaScript에서도 type check를 할 수 있으나, 런타임에서만 가능하고 인식할 수 있는 타입이 적어 한계가 있음



### typeof

* JavaScript 빌트인 연산자
* 피연산자의 타입을 문자열로 return

```JavaScript
const example = 10;
console.log(typeof example); // number
```



### typeof로 runtime type check하기

```JavaScript
const add = (num1, num2) => {
  if (typeof num1 !== 'number' || typeof num2 !== 'number') {
    throw new Error('숫자를 입력하세요');
  }
}
```





# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

