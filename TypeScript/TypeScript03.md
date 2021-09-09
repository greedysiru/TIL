# 타입스크립트 입문 - 변수와 그외 타입 정의하기

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 기본 타입 - 문자열, 숫자, 배열

* TypeScript는 JavaScript와 달리 변수 선언 시점에서 타입을 지정해야한다.
* :을 이용하여 타입을 정의
  * **Type Annotation**



### 문자열

```TypeScript
let str = 'hello';
```



### 숫자

```TypeScript
let num: number = 10;
```



### 배열

* 타입 선언에 맞지 않는 자료형을 배열안에 넣으면 IDE에서 에러가 발생한다.

```TypeScript
// 숫자로만 이뤄진 배열(제네릭)
let arr: Array<number> = [1, 2, 3];

// 문자열로만 이뤄진 배열(제네릭)
let heroes: Array<string> = ['Capt', 'Thor', 'Hulk'];

// 배열 리터럴
let items: number[] = [1, 2, 3,];
```



## 2. 기본 타입 - 튜플, 객체, 진위값

### 튜플

* 배열의 특정 인덱스에서의 타입을 지정
* 정의하지 않은 타입 또는 인덱스로 접근할 경우 오류가 발생

```TypeScript
let adress: [string, number] = ['gangnam', 777 ];
```



### 객체

```TypeScript
let obj: object = {};

// 객체의 형태이면 허용
let person: object = {
  name: 'capt',
  age: 100
};

// 구체적으로 객체의 각 프로퍼티 타입 지정
let siru: {name: string, age: number} = {
  name: 'siru',
  age: 7
}
```



### 불린

```TypeScript
let show:boolean = true;
```



## 3. 그외 타입 - Enum, Any, Void, Never

### Enum

* C, Java 등의 언어에서 흔하게 사용되는 타입
* 특정 값(상수)의 집합
* 인덱스 번호로 접근 가능
* 인덱스를 사용자 편의로 변경하여 사용 가능

```typescript
enum Avengers { Capt, IronMan, Thor };

let hero1: Avengers = Avengers.Capt;

// 인덱스 번호로도 접근 가능
let hero2: Avengers = Avengers[0];

// 사용자 편의로 인덱스 변경
enum Villains { Thanos = 2, Loki };

let Villain1:Villains = Villains[2]; // Thanos
let Villain2:Villains = Villains[3]; // Loki
```



### Any

* 모든 타입을 허용
* 기존에 자바스크립트로 구현되어 있는 웹 서비스 코드에 타입스크립트를 점진적으로 적용할 때 활용
  * but. 제대로 된 타입 선언을 위해서는 남용하지 말것

```TypeScript
let something: any = 1;
something = 'good';
something = [1, 2, 3, 'good']; // 어느 값을 할당하더라도 오류가 발생하지 않는다.
```



### void

* 변수에 undefined, null 할당
* 함수에는 반환 값을 설정하지 않도록 함

```TypeScript
let nothing:void = undefined;

// 아무것도 반환하지 않는 함수
function notihngFunction(): void {
  console.log('haha');
}
```



### Never

* 함수의 끝에 절대 도달하지 않는다는 의미를 지님
  * 함수의 끝까지 실행되지 않음

```TypeScript
function neverEnd(): never {
  while (true) {
    
  }
}
```

# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)