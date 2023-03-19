# Understanding TypeScript(44) - Readonly Interface Properties

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Readonly Interface Properties

* property를 읽기 전용으로 지정

* 수정을 할 수 없음
  * 수정을 하려면 Error 발생

* custom type에서도 사용 가능


```TypeScript
interface Greetable {
  readonly name: string;
  greet(phrase: string): void;
}

// Prerson class는 IPerson interface를 구현해야 함
class Person implements Greetable {
  // interface에 정의한 대로 readonly
  name: string;
  
  constructor(n: string) {
    this.name = n;
  }
  
  greet(phrase: string) {
   	console.log(`${phrase}, I'm ${name}`);
  }
}

let james: Greetable;
james = new Person('james');
// error
james.name = 'tony';
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

