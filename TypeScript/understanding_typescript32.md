# Understanding TypeScript(32) - "private" and "public" Access Modifiers

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## "private" and "public" Access Modifiers

* class의 property를 외부에서 접근하거나 조작 가능한 경우 application의 복잡도가 높아질 수 있음

```TypeScript

class Department {
  name: string;
  // 문자열을 요소로 하는 배열
  // 외부에서 접근 가능
  employees: string[] = [];
  constructor(n: string) {
    this.name = n;
  }
  
  describe() {
    console.log(`Department: ${this.name}`);
  }
  
  addEmployee(employee: string) {
    this.employees.push(employee);
  }
  
  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

const accounting = new Department('Accounting');

accounting.addEmployee('James');
accounting.addEmployee('Siru');

// 외부에서 접근 가능한 property이므로 외부에서 접근하거나 조작할 수 있음
accouting.employee[2] = 'Nunu';

accounting.decribe();
accouting.printEmployeeInformation();
```



### private

* class의 property를 외부에서 접근 또는 조작할 수 없게 함
  * 오직 class 내부에서만 접근, 조작할 수 있음
* method에도 적용할 수 있음
* TypeScript에서 지원
  * 런타임에서 동작하는 것이 아님

```TypeScript

class Department {
  name: string;
  private employees: string[] = [];
  // ...
}

```



### public

* class 외부에 property 또는 method를 공개할 수 있음
* TypeScript에서 지원

```TypeScript

class Department {
  public name: string;
  // ...
}

```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

