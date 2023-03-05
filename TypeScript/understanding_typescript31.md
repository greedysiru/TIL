# Understanding TypeScript(31) - Constructor Functions & "this" Keyword

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Constructor Functions & "this" Keyword

* 일반적으로 생성된 instance의 this는 instance를 가리킴
* 메서드 내부의 this는 호출한 object를 가리킴
  * 예기치 못한 동작을 할 수 있음

```TypeScript

class Department {
  name: string;
  constructor(n: string) {
    this.name = n;
  }
  
  // method: class의 동작을 표현
  describe() {
    // this.name 인스턴스의 name field
    console.log(`Department: ${this.name}`);
  }
}

const accounting = new Department('Accounting');
accounting.describe(); // Department: Accounting
const accountingCopy = { describe: accounting.describe };
// accountingCopy에 할당된 describe 메서드는 Department에 정의된 describe 메서드와 동일한 로직을 실행
// 그러나 accountingCopy는 literal object이므로 describe 메서드 내부의 this는 accountingCopy를 가리킴
// accountingCopy에 정의된 name property가 없어 undefined로 출력
accountingCopy.describe(); // Department: undefined
```



### TypeScript에서 method this 다루기

* 위 문제를 TypeScript로 해결

```TypeScript

class Department {
  name: string;
  constructor(n: string) {
    this.name = n;
  }
  
  // TypeScript 문법
  // method에서 사용할 this가 항상 instance를 가르키도록 함
  // 컴파일 이후에는 삭제
  describe(this: Department) {
    console.log(`Department: ${this.name}`);
  }
}

const accounting = new Department('Accounting');
accounting.describe(); // Department: Accounting
const accountingCopy = { describe: accounting.describe };
// Error 발생
// this가 Department instance를 가리키도록 되어있는데 그렇지 않으므로
accountingCopy.describe();

// 아래와 같이 accountingCopy에 name property를 추가하면 정상 동작
// Department와 똑같이 name property를 가지므로
const accountingCopy = { name: 'some', describe: accounting.describe };
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

