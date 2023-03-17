# Understanding TypeScript(42) - Using Interfaces with Classes

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Using Interfaces with Classes

* interface는 object의 구조를 설명하는 데만 사용 가능
  * custom type으로도 objecct 구조를 설명 가능
  * inerfaces는 object 만을 설명하는 용도로만 쓰이므로 비교적 명확
* class가 interface를 구현하도록 할 수 있음
  * 복수의 interface를 구현 가능
* interface는 여러 class 간에 기능을 공유하는 데 자주 사용
  * abstract class를 사용하는 것과 비슷
  * 단, interface는 세부 사항 구현이 없음


```TypeScript
interface Greetable {
  name: string;
  greet(phrase: string): void;
}

// Prerson class는 Greetable interface를 구현해야 함
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
