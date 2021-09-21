# 타입스크립트 입문 - 타입 단언, 타입 가드

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 타입 단언(Type Assertion)

* 타입스크립트의 타입 추론 방식으로는 복잡한 코드 이후 타입을 추론해낼 수 없다.
* 이를 방지하여 타입 추론을 무시하고 직접 타입을 지정할 수 있음
* DOM API 조작 시 사용

```TypeScript
// 타입 단언(type-assertion)
let a; // 타입이 any로 추론
a = 20;
a = 'a';
let b = a; // any, 맨처음에 선언된 any 타입이 b에 할당

let c = a as string // type 단언
```



### 타입 단언 예시

* DOM API 조작
  * DOM API: 웹 페이지의 태그 정보에 접근할 수 있는 API
  * VSC 내부에 DOM에 대한 타입들이 정의되어 있음
* DOM API 조작시, 특정 엘리먼트를 가져오는 코드를 작성했을 때 해당 엘리먼트가 실제로 존재하는지를 보장이 되지 않음
  * 에러 발생
  * 타입 단언으로 해당 엘리먼트가 있다는 것을 보장

```TypeScript
let div = document.querySelector('div') as HTMLDivElement;
```



## 2. 타입 가드

### 예시

* 유니온 타입을 사용했을 때, 명시적으로 할당되는 속성이어도 접근이 안되는 문제가 발생
* 해당 속성이 확실하게 할당될 것인지 보장이 안 되기 때문
* 타입 단언으로 해당 속성이 할당될 것을 보장할 수 있으나 코드 가동성이 줄어들 수 있음

```TypeScript
interface Devloper {
  name: string;
  skill: string;
}

interface Person {
  name: string;
  age: number;
}

function introduce(): Devloper | Person {
  return { name: 'Tony', age: 33, skill: 'Iron Making' }
}

let tony = introduce(); // Developer | Person

console.log(tony.skill); // error, Type 별 공통 속성만 접근할 수 있으므로
console.log(tony.name); // name은 공통 속성이므로 접근 가능

// 타입 단언으로 tony가 Developer 타입임을 보장
// 코드 가독성이 줄어듦
if ((tony as Devloper).skill) {
  let skill = (tony as Devloper).skill;
  console.log(skill);
} else if ((tony as Person).age) {
  let age = (tony as Person).age;
  console.log(age);
}
```



### 타입 가드 소개와 적용

* 특정 타입을 검사하기 위한 함수를 정의
  * 접두사는 is + 타입명을 사용하는 것이 관행
* is 넘겨받은 파라미터가 해당 타입인지를 구분하는 타입 가드 키워드

```typescript
interface Devloper {
  name: string;
  skill: string;
}

interface Person {
  name: string;
  age: number;
}

function introduce(): Devloper | Person {
  return { name: 'Tony', age: 33, skill: 'Iron Making' }
}

let tony = introduce(); // Developer | Person

// 타입 가드 정의
// Developer 타입인지 검사하는 함수
function isDeveloper(target: Devloper | Person): target is Devloper {
  // skill이라는 속성이 있으면 Developer 타입
  return (target as Devloper).skill !== undefined;
}

// 분기문에서 타입 가드를 사용하여 속성에 접근 가능
if (isDeveloper(tony)) {
  console.log(tony.skill);
} else {
  console.log(tony.age);
}
```



# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)