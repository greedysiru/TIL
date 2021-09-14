# 타입스크립트 입문 - 인터페이스

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 인터페이스란

* 상호 간에 정의한 약속 또는 규칙
* 변수가 어떤 타입으로 이루어져 있는지 명시적으로 알 수 있음
* 함수에게 필요한 파라미터가 어떤 타입을 가졌는지, 어떤 타입을 가진 값을 반환하는 지 알 수 있음
* 코드의 의도를 파악하기 용이



### 예시

```TypeScript
// User 인터페이스는 age를 숫자로, name을 문자로 가지는 객체임을 약속
interface User {
  age: number;
  name: string;
}

var siru: User = {
  age: 6,
  name: '시루',
}
```



## 2. 함수에 인터페이스 적용하기



### 함수의 인자를 정의하기

* 함수의 인자에 인터페이스를 적용할 수 있음
* 인자의 인터페이스와 맞지 않은 것을 전달 받으면 오류가 발생

```TypeScript
interface User {
  age: number;
  name: string;
}

// User 인터페이스를 인자로 사용하는 함수
function getUser(user: User) {
  console.log(user);
}

// User 인터페이스를 지키는 객체가 할당된 변수
const siru = {
  age: 6,
  name: '시루',
}

// 전달하는 인자가 age 또는 name이 없으면 오류가 발생
getUser(siru);
```



### 함수의 구조에 정의하기

* 함수의 파라미터, 리턴값의 타입을 인터페이스를 활용하여 정의
* 인터페이스의 타입에 맞지 않은 정의를 하면 오류 발생

```TypeScript
interface SumFunction {
  (a: number, b: number): number;
}

// sum은 SumFunction 인터페이스의 구조에 맞는 함수가 되어아 함
let sum: SumFunction;

sum = function (a:number, b:number): number {
  return a + b;
}
```



## 3. 인터페이스 딕셔너리 패턴

* key의 타입과 value의 타입을 인터페이스로 정의할 수 있다.
* 메소드를 사용할 때 타입스크립트가 타입을 추론할 수 있다.



### 정규식 딕셔너리 예시

```typescript
// 해당 인터페이스의 key는 문자열 타입이고 value는 정규식
interface StringRegexDicctionary {
  [key: string]: RegExp;
}

let obj: StringRegexDictionary = {
  sth: /abc/,
  cssFile: /\.css$/,
  jsFile: /\.js$/,
}

```



## 4. 인터페이스 확장(상속)

* 객체 지향 프로그래밍의 상속 개념을 인터페이스에서도 사용 가능
* 기존의 인터페이스를 상속 받아 확장한 다른 인터페이스를 정의할 수 있음



### 예시

```TypeScript
// name을 문자열로 age를 숫자로 하는 인터페이스
interface Person {
  name: string;
  age: number;
}

// Person 이라는 인터페이스를 확장한 인터페이스
interface Developer extends Person {
  language: string;
};

// greedysiru 변수는 Person을 확장한 Developer 인터페이스가 정의되어 있음
// Person의 name, age 그리고 Developer의 language가 맞게 할당되어야 함
let greedysiru: Developer = {
  name: 'siru',
  age: 6,
  language: 'JavaScript'
}
```





# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)