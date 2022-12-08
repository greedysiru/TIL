# 클린코드 자바스크립트 - 변수(function scope & block scope)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. function scope

* var 키워드는 함수 스코프를 가져, 전역 공간의 스코프가 오염될 가능성이 있음

```JavaScript
var ex = '예시';

if (ex === '예시') {
  var ex = '예시2';
  console.log(ex); // 예시2
}

console.log(ex); // 예시2
```



## 2. block scope

* let, const는 블록 스코프를 가져, 전역 공간의 스코프가 오염되지 않음

```JavaScript
let ex = '예시';

if (ex === '예시') {
  let ex = '예시2';
  console.log(ex); // 예시2
}

console.log(ex); // 예시
```



## 3. let보다는 const를 사용해야하는 이유

* cosnt 키워드는 재할당이 금지됨
  * 본연의 객체, 배열과 같은 레퍼런스를 조작할 때는 이상 없음

```JavaScript
// const 선언, 할당(객체)
const pet = {
  name: 'siru'.
  age: 8,
}

// const 재할당은 에러 발생
// Assignment to constant variable.
pet = {
  name: 'nunu'.
  age: 5,
}

// 점표기법으로 접근하여 재할당은 가능
pet.name = 'nunu';
pet.age = 5;


// const 선언, 할당(배열)
const pets = ['siru'];

// push 메서드로 요소 추가 가능
pets.push('nunu');
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

