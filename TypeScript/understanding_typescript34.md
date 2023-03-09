# Understanding TypeScript(34) - "readonly" Properties

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## "readonly" Properties

* TypeScript keyword
* 초기화 이후 오직 읽기만 가능한 property
* 바뀌지 않을 property에 적용
  * 고유한 식별자를 의미하는 property
  * ex) id


```TypeScript
class Department {

  // 전달받은 파라미터대로 class field가 초기화됨
  constructor(private readonly id:string, public name: string) {

  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

