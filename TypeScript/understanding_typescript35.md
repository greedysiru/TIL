# Understanding TypeScript(35) - Inheritance

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Inheritance

* 상속
  * 클래스 A를 클래스 B가 상속하면 
  * 클래스 B는 클래스 A의 모든 property, method를 가짐
  * 클래스 B는 클래스 A에 없는 자기만의 property, method를 가질 수 있음
  * 복수의 클래스를 상속할 수는 없음
  * 상속되는 클래스는 sub class라고 칭함
* extends keyword를 사용하여 상속을 구현할 수 있음
* sub class 만의  constructor를 사용해야할 때(자신만의 property를 초기화 해야할 때)는 super 를 사용
  * super는 constructor 안에서 부모 클래스의 constructor를 호출

```TypeScript
class Department {
  private employees: string[] = [];

  constructor(private readonly id: string, public name: string) {}

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }

  addEmployee(employee: string) {
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

// Department Class를 상속
// Departmnet의 property와 method를 상속
class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    // sub class의 constructor에서 super가 가장 먼저 호출되어야 함
    // id property 상속 받고 name은 IT로 초기화
    super(id, 'IT');
    // ITDepartment만 가지는 property
    this.admins = admins;
  }
}

class AccountingDepartment extends Department {
  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
  }

  // AccountingDepartment class만 가지는 methods
  addReport(text: string) {
    this.reports.push(text);
  }

  printReports() {
    console.log(this.reports);
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

