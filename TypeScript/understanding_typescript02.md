# Understanding TypeScript(2) - 타입스크립트 사용하기

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## 타입스크립트 사용하기

### TypeScript 설치하기

* node와 npm install
* terminal에서 아래 커멘드를 입력(mac)

```shell
sudo npm install -g typescript
```

* 이후에 tsc 커멘드로 TypeScript complier를 부를 수 있음

```shell
tsc app.ts
```





### JavaScript 코드

```JavaScript
// DOM API로 elements 가져오기
const button = document.querySelector('button');
const input1 = document.getElementById('num1');
const input2 = document.getElementById('num2');

// 두 수를 더하는 함수
const sum = (num1, num2) => num1 + num2;

// button element에 event listener 등록
button.addEventListener("click", function() {
  // input.value는 항상 string이어서 의도치 않은 동작이 발생하게 됨
  // 의도상 각 input에 입력한 수들이 합쳐진 결과가 로깅되어야 하지만, 암묵적 타입변환으로 인해 각 수를 문자열 취급하여 이어붙인 새로운 문자열이 로깅될 것
  console.log(sum(input1.value, input2.value));
})
```



### JavaScript로 위 코드 개선하기

* JavaScript로 위 코드의 문제를 개선가능하지만, 

```JavaScript
// event listener 함수에 타입 유효성 검사 로직을 추가
const sum = (num1, num2) => {
  if (typeof num1 === 'number' && typeof num2 === 'number') {
    return num1 + num2;
  } else {
    // 문자열로 들어온 경우 숫자로 형변환
    return +num1 + +num2;
  }
}
```



### TypeScript로 위 코드 개선하기

* ts 확장자의 파일은 tsc 커맨드로 js 확장자(JavaScript)로 컴파일할 수 있음
* 컴파일된 js파일에는 TypeScript 관련 문법이 제거

```TypeScript
// !의 의미: non-null assertion, 해당 표현식이 null이 아니라는 의미
// TypeScript는 DOM API가 가져온 요소가 없을 수도 있다고 판별(null)하므로 non-null assertion으로 해당 요소가 반드시 들어온다고 명시해야 함
const button = document.querySelector('button')!;
// as의 의미: type assertion, 해당 표현식이 as 뒤에 오는 type임을 단언
const input1 = document.getElementById('num1')! as HTMLInputElement;
const input2 = document.getElementById('num2')! as HTMLInputElement;

// 함수 파라미터에 무엇이 들어올지 type을 명시
// 두 수의 합을 구하는 함수므로 두 파라미터가 number이어야 함
const sum = (num1: number, num2: number) => num1 + num2;

button.addEventListener("click", function() {
  // 숫자로 형변환
  console.log(sum(+input1.value, +input2.value));
})
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

