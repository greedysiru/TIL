# 클린코드 자바스크립트 - 배열 다루기(유사 배열 객체)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 유사 배열 객체

* JavaScript 배열은 객체
* 유사 배열 객체
  * node list
  * arguments
  * key를 index(숫자)로 가지고 length 프로퍼티를 가진 객체의 경우
* 유사배열 객체는 for문을 통해 순회가능하지만, array 전용prototype method는 호출할 수 없음



### Array.from()

* 유사 배열 객체를 배열로 바꿀 수 있음

```JavaScript
const arrayLikeObject = {
  0: 'siru',
  1: 'nunu',
  length: 2,
};

// 유사 배열 객체를 배열로 바꿀 수 있음
const arr = Array.from(arrayLikeObject);

console.log(arr); // [ 'siru', 'nunu' ]

// 변환전의 arrayLikeObject는 배열이 아님
console.log(Array.isArray(arrayLikeObject)); // false

// 변환후의 arr는 배열
console.log(Array.isArray(arr)); // true
```



### arguments

* 함수 선언시 매개변수를 정의하지 않았어도 호출시점에서 가변적으로 받게되는 인자

```JavaScript
function generateCatList() {
  for (let i = 0; i < arguments.length; i++) {
    const element = arguments[i];
    
    console.log(element);
  }
}

generateCatList('siru', 'nunu', 'mango');
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

