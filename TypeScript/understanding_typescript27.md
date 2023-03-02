# Understanding TypeScript(27) - Strict Compilation

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Strict Compilation

* strict: 엄격한 Type Check
  * 해당 옵션은 아래의 옵션들을 모두 활성화한 것과 같음
  * noImplicitAny: any Type을 사용한 경우 오류 발생
  * strictNullChecks: 엄격한 null check
  * strictFunctionTypes: 엄격한 함수 타입 check
  * strictBindCallApply: 함수에서 `bind`, `call` 그리고 `apply` 메서드의 더 엄격한 검사를 활성화
  * strictPropertyInitialization: 클래스 프로퍼티를 생성자에서 초기화 하도록 함
  * noImplicitThis: this 표현식에 any 할당 불가
  * alwaysStrict: 모든 소스 파일에 "use strict" 추가
* stict 옵션은 run time error를 방지하기 위해 필수적인 옵션



### noImplicitAny

* any Type을 사용한 경우 오류 발생
* 함수 파라미터의 경우 any가 추론되면 오류 발생
* 반면, 변수는 발생하지 않음



### strictNullChecks

* 엄격한 null check

```TypeScript
const button = document.querySelector('button');

// Error
// button이라는 DOM Element가 존재함이 보장되지 않음
button.addEventListener('click', () => {
  console.log('Clicked');
});
```

* 위 코드의 Error를 해결하는 코드

```TypeScript
const button = document.querySelector('button');

// DOM Element가 존재할 때만 실행
if (button) {
   button.addEventListener('click', () => {
    console.log('Clicked');
  }); 
}
```

# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

