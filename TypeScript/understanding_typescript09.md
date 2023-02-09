# Understanding TypeScript(9) - Working with Enums

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Working with Enums

### Enum

* TypeScript에서만 지원하는 Type
* `enum {NEW, OLD}`
* Global Constant Identifiers
  * 상수를 관리하기 용이
* Enum으로 관리하는 상수는 관습적으로 대문자를 사용
  * ex) STUDENT_LEVEL

* kebab case를 사용할 수 없음




### JavaScripnt에서의 상수 관리

```JavaScript
const ADMIN = 0;
const READ_ONLY = 1;
const AUTHOR = 2;

const person = {
  name: "James",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: AUTHOR,
};
```



### Enum을 활용한 상수 관리

```TypeScript
// 각 Enum에는 숫자가 할당
enum Role {
  // 1
  ADMIN,
  // 2
  READ_ONLY,
  // 3
  AUTHOR,
}

const person = {
  name: "James",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: Role.ADMIN,
};

if (person.role === Role.AUTHOR) {
  console.log("관리자 입니다.");
}

```

```TypeScript
// Enum에 임의의 수. 문자를 할당할 수 있음
enum Role {
  // 5
  ADMIN = 5,
  // 6
  READ_ONLY,
  AUTHOR = 'AUTHOR',
}
```





### Enum의 TypeScript Compiler 결과

```JavaScript
var Role;
// IIFE
(function (Role) {
    Role[Role["ADMIN"] = 0] = "ADMIN";
    Role[Role["READ_ONLY"] = 1] = "READ_ONLY";
    Role[Role["AUTHOR"] = 2] = "AUTHOR";
})(Role || (Role = {}));
var person = {
    name: "James",
    age: 30,
    hobbies: ["Sports", "Cooking"],
    role: Role.ADMIN
};
if (person.role === Role.AUTHOR) {
    console.log("관리자 입니다.");
}

```








# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

