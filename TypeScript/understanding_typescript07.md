# Understanding TypeScript(7) - Arrays Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Arrays Types

* JavaScript Array
  * numbers, strings, booleans, objects, other arrays들이 선형으로 나열된 자료형



### Literal Array에서의 타입 추론

```TypeScript
const person = {
  name: "James",
  age: 30,
  // Literal Array로 이루어진 Property
  hobbies: ["Sports", "Cooking"],
};
// 위 person 객체 hobbies property의 타입 추론은 아래와 같이 됨
/*
hobbies: string[]
*/
for (const hobby of person.hobbies) {
  // string built-in method를 사용할 수 있음
  // why? TypeScript는 hobbies property가 string으로 이루어진 array란 것을 알고 있음
  console.log(hobby.toUpperCase());
}
```



### Array Type Assignment

```TypeScript
let favoriteActivites: string[];
favoriteActivites = ["Sports"];
// 아래와 같이 다른 자료형을 넣게 되면 error
favoriteActivites = ['Spores', true, 1]; // Error
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

