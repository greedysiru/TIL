# [드림코딩 by 엘리] JavaScript 기초 강의(4) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/510) 참고**



# Procedual language

* 절차지향 언어
* 함수가 프로그램에서 중요한 기능을 담당
* JavaScript는 class가 있지만, prototype을 베이스로하여서 객체지향 언어가 아니라 절차지향 언어이다.



# Function

* sub-program이라고도 부름
* 프로그램안에서 각각의 작은 단위의 기능을 실행
* 여러번 재사용이 가능
* 일을 수행하거나 값을 계산
* 프로그램을 구성하는 fundamental building block
* Input -> Output
* 함수의 이름을 보고 어떤 일을 할 지 추론할 수 있다.
* 전달하는 파라미터, 기대되는 리턴값을 보면서 어떤 수행을 하는지 알 수 있다.



## Function Declaration

> **function name (param1, param2) { body... return};**

* function 키워드를 사용하여 선언
* 한가지 함수는 한가지 일만 하도록 한다.
* 함수의 이름은 동사형으로 짓기 (cf. 변수이름은 명사형)
  * 함수의 이름을 정하기 어렵다면, 함수에서 너무 많은 것을 처리하고 있지 않은지 검토
  * e.g. createCardAndPoint -> createCard, createPoint
* JavaScript에서 function은 object
  * 변수에 할당, 파라미터에 전달, return 가능 (First-class function)



## TypeScript에서 함수 선언

```typescript
function log(messgae: string): number{
  console.log(messgae);
  return 0;
}
```

* TypeScript는 항상 파라미터나 return의 type을 명시하도록 한다.
* 규모있는 프로젝트, 다양한 개발자들과 일을할 때 또는 작성한 것을 라이브러리로 API 제공해야할 때 TypeScript를 사용하는 것을 권장
* 함수의 interface만 봐도 무슨 일을 하는 함수인지 알 수 있다.



## Parameters

* premitive의 경우: 값 자체가 전달된다.
* object: reference가 전달된다.
  * 함수 안에서 object를 변경하면, 변경 사항이 그대로 메모리에 적용된다.

```JavaScript
function changeName(obj){
  obj.name = 'coder';
}

const cat = { name: 'siru' };
changeName(cat);
console.log(cat); // { name: 'coder'};
```



## Default parameters

* ES6 에서 추가
* parameter의 기본값을 설정할 수 있다.

```JavaScript
function showMessage(messgae, from = 'unknown'){
  console.log(`${message} by ${from}`);
}
```



## Rest Parameters

* 배열형태로 파라미터를 전달

```JavaScript
function printAll(...args){
  for (let i = 0; i < arg.length; i++){
    console.log(args[i]);
  }
  
  // 위와 같은 표현 (for ... of 문, forEach문)
  for (const arg of args) {
    console.log(arg);
  }
  
  args.forEach((arg) => console.log(arg));
}

printAll('I', 'AM', 'SIRU');
```



## Local Scope

> **밖에서는 안이 보이지 않고, 안에서만 밖을 볼 수 있다.**

* block안의 지역변수는 안에서만 접근이 가능하다.
  * 밖에서 출력하려하면 에러가 발생
* block 안에서는 global variable을 접근할 수 있다.



## return

* 함수에서는 전달받은 파라미터를 계산하여 return이 가능하다.
* return이 없는 함수는 return undefined와 같다. (생략 가능)



## Early return, early exit

* 함수를 작성할 때, if문을 사용하여 조건이 맞지 않을 때 빠르게 return하도록 한다.
  * 그 이후에 필요한 logic을 작성

```JavaScript
function upgrageUser(user){
  if (user.point <= 10){
    return;
  }
  console.log('good');
}
```



## Function Expression

* 함수를 선언함과 동시에 변수에 할당할 수 있다.
  * anonymous function, unnamed function
* Function Expression은 할당 후에만 호출이 가능하다.
* Function Declaration은 hoisting이 된다.
  * 함수 선언 이전에 호출되어도 JavaScript엔진이 선언문을 제일 위에 올린다.
```JavaScript
const print = function () {
  console.log('print');
}
```



## Callback

* Callbakc fucntion 함수를 전달하는 것

```JavaScript
function randomQuiz(answer, printYes, printNo) {
  if (answer === 'love you') {
    printYes()
  } else {
    printNo();
  }
}
// anonymous function
const printYes = function () {
  console.log('yes!');
}

// named function
// 디버깅시, stack traces에 이름이 나오도록 허거나 재귀함수를 사용할때 named function 사용
const printNo = function print() {
  console.log('No!');
}

randomQuiz('wrong', printYes, printNo);
randomQuiz('love you', printYes, printNo);
```



## Arrow Function

* 함수를 간결하게 만들 수 있다.
* 항상 anonymous fucntion로 만들어진다.
* 다양한 코드를 실행할 때는 block을 사용 가능
  * 단, return 키워드를 사용해야 한다.

```JavaScript
const simple = () => console.log('simple');
const add = (a, b) => a + b;
```



## IIFE

* Immediatly Invoked Function Expression
* 선언함과 동시에 호출

```JavaScript
(function hello() {
  console.log('HI');
})();
```



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)
