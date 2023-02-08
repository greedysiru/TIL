# Understanding TypeScript(8) - Working with Tuples

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Working with Tuples

### Tuple

* TypeScript에서만 지원하는 Type
* 고정된 length를 가진 array
* 각각의 요소의 Type 또한 고정
* 엄격한 형태의 배열을 정의하여 사용할 때 유용



### Literal Array에서의 타입 추론

```TypeScript
const person = {
  name: "James",
  age: 30,
  hobbies: ["Sports", "Cooking"],
	// role은 이와 같이 타입 추론 됨 (property) role: (string | number)[]
  role: [2, "author"],
};

// role property의 길이와 타입이 고정되지 않음
// 아래 코드들은 실행
person.role.push('admin');
person.role[1] = 10;
```



### Tuple Type Assignment

```TypeScript
const person: {
  name: string;
  age: number;
  hobbies: string[];
  // tuple type assignment
  role: [number, string];
} = {
  name: "James",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: [2, "author"],
};

// error
person.role[1] = 10;
// error
person.role = [0, "admin", "user"];
// push가 되는 이유: TypeScript의 Exception
person.role.push("admin");
```






# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

