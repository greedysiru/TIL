# 타입스크립트 입문 - 타입 호환, 타입 모듈화

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 타입 호환(Type Compatibility)

* 타입스크립트 코드에서 특정 타입이 다른 타입에 잘 맞는지를 의미



### 구조적 타이핑

* 코드 구조 관점에서 타입이 서로 호환되는지의 여부를 판단

```TypeScript
interface Pet {
  name: string;
}

let myCat: Pet;
let siru = { name: 'siru', age: 5 };
// siru의 속성 중에 name이 있으므로 Pet 타입과 호환
myCat = siru;
```



### 타입 호환 예제 - 인터페이스, 클래스

* 타입 호환이 될지의 여부는 class, interface의 차이는 영향이 없다.
* 내부적으로 존재하는 속성과 타입의 정의에 대해서 비교하여 호환 여부가 결정 됨
* 구조적으로 작은 것에 큰 것은 호환이 되지 않음
* 구조적으로 큰 것에 작은 것은 호환이 됨
* 클래스 타입끼리 비교시, 스태틱 멤버와 생성자를 제외하고 속성만 비교

```TypeScript
interface Developer {
  name: string;
  skill: string;
}

interface Person {
 name: string
}

class PersonClass {
  name: string;
}

let developer: Developer;
let person: Person;

developer = person; // error, developer 객체가 구조적으로 더 커서 호환이 안 됨

person = developer; // person 객체가 구조적으로 더 작아서 호환이 됨

developer = new PersonClass(); // error, developer가 구조적으로 더 커서 Person Class가 호환이 안 됨
```



### 타입 호환 예제 - 함수, 제네릭

* 함수, 제네릭의 경우도 인터페이스, 클래스와 같이 내부 파라미터와 속성의 타입 그리고 구조에 따라 호환 여부가 결정

```TypeScript
let add = function(a: number) {
  // ...
}

// sum의 구조가 add보다 구조적으로 더 크다
let sum = function(a: number, b: number) {
  // ...
}

// add는 하나의 인자만 받아서 할당이 되지 않음(호환이 되지 않음)
add = sum;
// sum은 두개의 인자를 받고 있으므로 할당이 됨(호환이 됨)
sum = add;

// 제네릭
// 비어있는 인터페이스
interface Empty<T> {
  // ...
}

let empty1: Empty<string>;
let empty2: Empty<number>;

// 비어있는 인터페이스이므로 구조적으로 차이가 없어 호환
empty1 = empty2;
empty2 = empty1;

interface NotEmpty<T> {
  data: T;
}

let notEmpty1: NotEmpty<string>;
let notEmpty2: NotEmpty<number>;

// 제네릭에의해 구조적인 타입 차이가 생겨서 서로 호환이 되지 않음
notEmpty1 = notEmpty2;
notEmpty2 = notEmpty1;
```



## 2. 타입 모듈화

* 타입스크립트의 모듈 시스템은 ES6+의 Modules 개념과 유사
* 서비스 구현 시, 타입을 모듈화하는 것이 편리



### 타입 모듈화 예시

```TypeScript
// types.ts
export interface Todo {
  title: string;
  checked: boolean;
}
```

```TypeScript
// app.ts
import {Todo} from './types';
let itme: Todo = {
  title: '할 일 1',
  checked: false,
}
```



### 자바스크립트의 모듈 시스템(Import & Export)

* 자바스크립트의 코드를 모듈화 할 수 있는 기능
* import와 export로 표준화
* 자바스크립트의 유효 범위는 기본적으로 전역으로 시작 됨
  * 각 파일의 변수 스코프가 겹쳐서 문제 발생
* 다른 파일에 정의된 모듈(변수, 함수)을 가져와서 활용할 수 있음

# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)