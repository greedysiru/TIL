# Understanding TypeScript(45) - Extending Interfaces

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Extending Interfaces

* interface에서 상속을 구현 가능
  * 여러 interface를 상속할 수 있음
  * cf) class에서는 하나의 class만 상속 가능
  * TypeScript 고유 문법이기 때문

* extends keyword 사용
* interface를 분리하는 이유
  * 여러 클래스에 걸쳐 공통인 속성을 하나의 Interface로 묶고 유연하게 적용 가능


```TypeScript
interface Named {
  readonly name: string;
}

// Names interface 확장
interface Greetable extends Names {
  greet(phrase: string): void;
}

class Person implements Greetable {
  name: string;
  
  constructor(n: string) {
    this.name = n;
  }
  
  greet(phrase: string) {
   	console.log(`${phrase}, I'm ${name}`);
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

