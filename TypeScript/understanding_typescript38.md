# Understanding TypeScript(38) - Static Methods & Properties

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Static Methods & Properties

* vanilla JavaScript에서도 사용 가능
  * ES6 이후

* instnace를 생성하지 않아도 사용 또는 접근이 가능
  * class의 로직과 연관이 있음
  * instance를 생성하여 접근 불가능
  * class 내부에서도 this를 통해 접근할 수 없음
  * ex) Math

* static keyword로 선언
* static member
  * static keyword로 선언된 property, method


```TypeScript
class Department {
  // static method
  static fiscalYear = 2020;
  protected employees: string[] = [];

  constructor(private readonly id: string, public name: string) {}
  
  // static method
  static createEmployee(name: string) {
    	return {name: name};
  }

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

// Static method 사용
// Department static method를 사용하지 않고도 사용 가능
const employee1 = Department.createEmployee('James');
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

