# Understanding TypeScript(37) - Getters & Setters

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Getters & Setters

* vanilla JavaScript에서도 사용 가능
* getter
  * get keyword 사용
  * class 내부의 property를 return
  * property를 return 할 때 특정 로직을 실행할 수 있음
* setter
  * set keyword 사용
  * 최대 한 개의 매개변수만 가짐
  * class의 property에 할당을 할 때 사용
  * 또는 method를 사용할 수도 있음

```TypeScript
class Department {
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
  // class 내부에서만 접근할 수 있는 property
  private lastReport: string;
  
  // getter
  get mostRecentReport() {
    // lastReport에 값이 있어야 실행
    if (this.lastReport) {
      return this.lastReport; 
    }
    // 없는 경우 Error 발생
    throw new Error('No report found');
  }
  
  // setter
  set mostRecentReport(value: string) {
    if (!value) {
      throw new Error('Please pass in a valid value!');
    }
    this.addReport(value);
  }
  
  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
    this.lastReport = reports[0];
  }

  addEmployee(name: string) {
    if (name === 'James') {
      return;
    }
    
    this.employees.push(name);
  }

  addReport(text: string) {
    this.reports.push(text);
    this.lastReport = text;
  }

  printReports() {
    console.log(this.reports);
  }
}

const accounting = new AccountingDepartment('d2', []);

// property에 할당하는 것처럼 사용
accounting.mostRecentReport = 'Year End Report';
// property를 접근하는 것처럼 점 표기법 사용
console.log(accounting.mostRecentReport);
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

