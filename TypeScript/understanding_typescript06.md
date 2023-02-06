# Understanding TypeScript(6) - Object Types

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Object Types

* JavaScript Object
  * key, value 짝이 `{}` 에 묶여있는 자료형
* TypeScript에서 특별한 Object Type을 정의할 수 있음
* 존재하지 않는 객체의 property에 접근하려하면 TypeScript는 Error 를 발생시킴



### Object Type

* key, type 짝이  `{}` 에 묶여 표현 됨

```TypeScript
type someObject = {
  someProp1: number;
  someProp2: string;
};
```





### Literal Object에서의 타입 추론

```TypeScript
const person = {
  name: "James",
  age: 30,
};
// 위 person 객체의 타입 추론은 아래와 같이 됨
/*
const person: {
	name: string;
	age: number;
}
*/

// 때문에 아래와 같이 없는 property에 접근하지 못함
console.log(person.nickName); // Error
```



### built-in object type

* TypeScript에는 built-in object type이 있음
* object type이 지정된 object의 property에 접근시 Error 발생
  * TypeScript에게 object type임만 알려줬을 뿐 어떤 Property들을 가지는 지 알려주지 않았기 때문

```TypeScript
// person에 built-in object type 지정
const person: object = {
  name: "James",
  age: 30,
};

// 때문에 아래와 같이 없는 property에 접근하지 못함
console.log(person.name); // Error
```



### specific object type

* 어떤 property를 가질 object type인지를 지정할 수 있음
* 타입 추론보다 권장되는 방식

```TypeScript
// specific object type 지정
const person: {
  name: string;
  age: number
} = {
  name: "James",
  age: 30,
};

// 접근 가능
console.log(person.name);
```





# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

