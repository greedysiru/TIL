# Understanding TypeScript(39) - Abstract Classes

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Abstract Classes

* 추상 클래스
  * instance를 생성할 수 없음
  * 공통 동작(method), 공통 특성(property)에 대한 명세가 기술되어 있는 클래스

* 추상 메서드
  * 메서드에대한 명세
  * 메서드가 받을 매개변수의 타입과 return할 타입만을 명시
  * 추상 클래스를 extends하는 sub class에서는 명세에 따라 구체적인 구현을 해야 함


```TypeScript
// 추상 클래스
abstract class Department {
  static fiscalYear = 2020;

  protected employees: string[] = [];

  constructor(protected readonly id: string, public name: string) {}

  static createEmployee(name: string) {
    return { name: name };
  }

  // 추상 메서드
  abstract describe(this: Department): void;

  addEmployee(employee: string) {
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

// abstract class인 Department를 상속
class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    super(id, 'IT');
    this.admins = admins;
  }

  // 추상 메서드인 describe 구현
  describe() {
    console.log('IT Department - ID: ' + this.id);
  }
}

class AccountingDepartment extends Department {
  private lastReport: string;

  get mostRecentReport() {
    if (this.lastReport) {
      return this.lastReport;
    }
    throw new Error('No report found.');
  }

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
  
  // 추상 메서드인 describe를 구현
  describe() {
    console.log('Accounting Department - ID: ' + this.id);
  }

  addEmployee(name: string) {
    if (name === 'Max') {
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
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

