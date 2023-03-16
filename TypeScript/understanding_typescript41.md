# Understanding TypeScript(41) - A First Interface

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## A First Interface

* Interface
  * Object의 구조를 설명
  * TypeScript 문법
  * 명명은 대문자로 시작
  * property, method의 이름과 type을 정의


```TypeScript
interface Person {
  // properties
  name: string;
  age: number;
  
  // method
  greet(phrase: string): void;
}

let user1: Person;
user1 = {
  name: 'James',
  age: 31,
  
  greet(phrase: string) {
    console.log(`${phrase}, I'm ${name}`);
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

