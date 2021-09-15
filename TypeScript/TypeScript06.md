# 타입스크립트 입문 - 타입 별칭, 연산자 타입 정의

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 타입 별칭 소개

* 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수
* 타입을 정의할 수 있는 모든 곳에 사용할 수 있음
* IDE 상에서 타입 별칭의 프리뷰를 볼 수 있음
* 코드 가독성을 높일 수 있음
* 확장이 되지 않음
  * 인터페이스는 extends 키워드로 확장이 가능
  * 그러므로 가능한 인터페이스로 타입을 선언할 것
  * **좋은 소프트웨어는 언제나 확장이 용이해야 한다.**



### 예시

```TypeScript
type name = string;
const myName: name = 'siru';
```



## 2. 연산자를 이용한 타입 정의

### Union Type

* 하나의 타입 이상을 사용할 수 있음
* JavaScript에서의 or연산자의 (||)하나를 사용하여 여러 타입을 선언할 수 있음

```TypeScript
// 문자열 또는 숫자를 받아서 출력하는 함수
function logMessage(value: string | number) {
  console.log(value);
}

logMessage('hello');
logMessage(100);
```



### Union Type의 장점

* 타입 가드
  * 특정 타입으로 타입의 범위를 좁혀나가는(필터링 하는) 과정
* 타입 추론
  * 사용되는 변수의 타입을 감지하여 그에 맞는 api를 자동완성



### Union Type의 특징

* 여러개의 인터페이스를 유니온 타입(|)을 이용하여 특정 변수에 타입 정의하였을 때 **모든 인터페이스에 속한 타입만 사용할 수 있다.**
  * 논리 연산자의 or 연산으로 착각하지 않도록 주의
* TypeScript의 입장에서 여러개의 인터페이스 중 어느 것이 들어올 지 예상할 수 없으므로 가장 오류가 나지 않는 방향으로 추론한다.
  * 그러므로 and 연산처럼 모든 인터페이스에 속한 타입만 사용할 수 있게 됨
* 별도의 타입 가드를 이용하여 타입의 범위를 좁혀 다른 속성에 접근이 가능하도록 할 수 있다.

```TypeScript
interface Developer {
  name: string;
  skill: string;
}

interface Person {
  name: string;
  age: number;
}

function askSomeone(someone: Developer | Person) {
  // Union Type을 선언했음에도 불구하고 공통 속성만 접근 가능(name)
  // 공통된(보장된) 속성만 제공
  // 다른 속성 skill, age에 접근 시 TypeError
  console.log(someone.name);
}
```



### Intersection Type

* and연산자(&)를 사용하여 여러 타입을 모두 만족하는 하나의 타입을 만들 수 있음
* 기본 타입에 대해서는 사용 불가
  * ex) string & number: 둘 다 만족 할 수 있는 타입은 없으므로

```TypeScript
interface Developer {
  name: string;
  skill: string;
}

interface Person {
  name: string;
  age: number;
}

// someone은 Developer와 Person 각 인터페이스의 속성을 모두 가지는 파라미터
function askSomeone(someone: Developer & Person) {
  // someone은 모든 속성을 포함하므로 블록 내에서 모든 속성을 접근 가능
  console.log(someone.name);
  console.log(someone.age);
  console.log(someone.skill);
}
```



### Union Type vs. Intersection Type

* UnionType로 이루어진 함수
  * **각 인터페이스**의 규격에 맞춘 변수를 파라미터로 넘길 수 있음
  * 실무에서 많이 사용
* Intersection Type로 이루어진 함수
  * **모든 인터페이스**의 규격을 만족하는 변수만 파라미터로 넘길 수 있음
  * UnionType보다 상대적으로 덜 사용됨

# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)