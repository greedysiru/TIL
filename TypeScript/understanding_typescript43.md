# Understanding TypeScript(43) - Why Interfaces?

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Why Interfaces?

* class들에서 기능을 쉽게 공유할 수 있게 함
  * 특정 구조를 강제

* interface를 class 또는 변수에 지정함에 따라 필수적으로 있어야만 하는 관심사(property, method)에만 집중할 수 있음
  * 강력하고 유연한 코드를 작성할 수 있음

```TypeScript
interface IPerson {
  name: string;
  greet(phrase: string): void;
  say(word: string): void;
  calculate(num1: number, num2: number): number;
}

// Prerson class는 IPerson interface를 구현해야 함
class Person implements IPerson {
  name: string;
  
  constructor(n: string) {
    this.name = n;
  }
  
  greet(phrase: string) {
   	console.log(`${phrase}, I'm ${name}`);
  }
  
  say(word: string) {
    console.log(`I said, ${word}`);
  }
  
  caclulate(num1: number, num2: number) {
    return num1 * num2;
  }
}

let james: IPerson;
james = new Person('james');

let tony: IPerson;
tony = new Person('tony');
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

