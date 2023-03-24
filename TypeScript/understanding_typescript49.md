# Understanding TypeScript(48) - Intersectin Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Intersectin Types

### Type alias를 사용한 방식

* &를 사용하여 Type을 결합
* Object의 경우
  * 개체 속성들이 조합됨
* Union의 경우
  * 공통된 유형이 추론됨

```TypeScript
type Admin = {
  name: string;
  privileages: string[];
};

type Employee = {
  name: string;
  // JavaScript Date Type(Built-in)
  statDate: Date;
}

// Admin, Employee 두 Type이 조합
type ElevatedEmployee = Admin & Employee;

const e1: ElevatedEmployee = {
  name: 'James',
  privileages: ['create-client'],
  startDate: new Date(),
}

type Combinable = string | number;
type Numeric = number | boolean;

// Combinable, Numeric 두 Type의 교집합
type Universal = Combinable & Numeric;
```



### Interface를 사용한 방식

* extends keyword를 사용
  * 여러 interface를 상속한다는 의미

```TypeScript
interface Admin {
  name: string;
  privileages: string[];
};

interface Employee {
  name: string;
  statDate: Date;
}

interface ElevatedEmployee extends Employee, Admin


const e1: ElevatedEmployee = {
  name: 'James',
  privileages: ['create-client'],
  startDate: new Date(),
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

