# TypeScript(5)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. Classes

* TypeScript에서는 객체 지향 프로그래밍 키워드를 사용할 수 있음
  * JavaScript로 컴파일되며 해당 키워드들은 사라짐
  * 해당 키워드들은 TypeScript에서만 사용딤
  * ex) private, protected
* TypeScript에서는 클래스를 Type으로 사용할 수 있음

### 접근 제어자 정리

| 구분      | 선언한 클래스 내 | 상속받은 클래스 내 | 인스턴스  |
| --------- | ---------------- | ------------------ | --------- |
| private   | 접근 가능        | 접근 불가          | 접근 불가 |
| protected | 접근 가능        | 접근 가능          | 접근 불가 |
| public    | 접근 가능        | 접근 가능          | 접근 가능 |



### 추상 클래스

* 다른 클래스가 상속 받을 수 있는 클래스
* 추상 클래스는 인스턴스를 만들 수 없음



### 추상 메소드

* 추상 클래스를 상속받는 클래스들이 반드시 구현(Implement)해야하는 메서드
* Call Signiture만을 가짐



### 인스턴스

* 클래스가 new 생성자로 인해 만들어져 구현된 실체



## 2. 클래스 예시(TypeScript Vs. JavaScript)

### TypeScript

```TypeScript
abstract class Animal {
    constructor(
        private kind: string,
        private gender: string,
        protected name: string,
    ) {}

    abstract cry(): void;
}

class Cat extends Animal {

    cry() {
        console.log('야옹');
    }
}

const siru = new Cat('cat', 'female', 'siru');
```



### JavaScript

* 위와 같은 클래스는 JavaScript에서 아래와 같이 컴파일링 됨

```JavaScript
"use strict";
class Animal {
    constructor(kind, gender, name) {
        this.kind = kind;
        this.gender = gender;
        this.name = name;
    }
}
class Cat extends Animal {
    cry() {
        console.log('야옹');
    }
}
const siru = new Cat('cat', 'female', 'siru')
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

