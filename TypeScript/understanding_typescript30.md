# Understanding TypeScript(30) - Creating a First Class

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Creating a First Class

```TypeScript
// class명은 대문자로 시작(convention)
class Department {
  // filed of a class
  // key: value가 아닌 key: type의 형태
  // instance가 초기화 되었을 때 해당 filed 또한 있어야 함
  name: string;
  
  // instance가 생성될 때 실행되는 method
  // object 초기화 작업을 정의
  constructor(n: string) {
  // filed of a class는 constructor에서 초기화
    this.name = n;
  }
}

// new 키워드와 class를 호출하면 class 내부에 정의된 constructor가 실행
const accounting = new Department('Accounting');
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

