# Understanding TypeScript(36) - Overriding Properties & The "protected" Modifier

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Overriding Properties & The "protected" Modifier

* base class로부터 상속받은 property와 method를 overriding할 수 있음
* private인 property는 sub class에서 접근할 수 없음
* protected는 class 외부에서 접근할 수는 없으나 sub class에서는 접근 가능

```TypeScript
class Department {
  // sub class에서 접근 가능
  protected employees: string[] = [];

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

class AccountingDepartment extends Department {
  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
  }

  // overriding
  addEmployee(name: string) {
    if (name === 'James') {
      return;
    }
    
    this.employees.push(name);
  }

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

