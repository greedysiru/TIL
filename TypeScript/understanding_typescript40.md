# Understanding TypeScript(40) - Singletons & Private Constructors

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Singletons & Private Constructors

* Singletons
  * 객체 지향 프로그래밍의 한 패턴
  * 클래스의 인스턴스가 항상 하나만 존재하도록 함
  * 정적 method, property를 쓰지 않는 경우에서 유용

* Private Constructors
  * 비공개 생성자
  * class 안에서만 접근 가능
  * static method로 private constructor를 실행 -> class instance의 존재 확인 -> 있으면 해당 instnace를 return 하거나 첫 instance를 생성하여 return



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

class AccountingDepartment extends Department {
  private lastReport: string;
  // singleton instance
  private static instance: AccountingDepartment;

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

  // private constructor
 	private constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
    this.lastReport = reports[0];
  }
  
  // 이 클래스의 인스턴스를 갖고 있는지 확인하고 없다면 새 것을 반환
	static getInstance() {
    // instance 존재 확인
    if (AccountDepartment.instance) {
      return this.instance;
    }
    
    this.instance = new AccountDepartment('d2', []); 
    return this.instance;
  }	
  
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

// singletone
const accounting = AccountingDepartment.getInstance(); 
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

