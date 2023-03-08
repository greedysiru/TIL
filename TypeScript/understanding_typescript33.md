# Understanding TypeScript(33) - Shorthand Initialization

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Shorthand Initialization

* constructor에서 class filed를 초기화할 때 단축할 수 있음

```TypeScript
// 단축 전
class Department {
	private id: string;
  public name: string;

  constructor(id:string, n: string) {
    this.id = id;
    this.name = n;
  }
}

// 단축 후
class Department {

  // 전달받은 파라미터대로 class field가 초기화됨
  constructor(private id:string, public name: string) {

  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

