# 클린코드 자바스크립트 - 객체 다루기(Object Destructuring)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Object Destructuring

### 매개변수에서의 활용

* 함수에서 정의한 매개변수의 순서는 호출시에도 지켜야 함
  * 호출 시에 순서를 지키지 않으면 오류가 발생
  * destructuring으로 이를 해결

```JavaScript
function Cat(name, age, color) {
  this.name = name;
  this.age = age;
  this.color = color;
}

// 반드시 정의한 시점에서의 순서와 맞추어 호출해야 함
const siru = new Cat('siru', 8, 'chaos');

// 하나의 객체로 묶으면 사용성이 높아짐
function Cat({name, age, color}) {
  this.name = name;
  this.age = age;
  this.color = color;
}

// 호출시에 순서를 지키지 않아도 됨
const siru = new Cat({
  name: 'siru',
  age: 8,
  color: 'chaos'});
```



### 명시적으로 매개변수 표현하기

* 필수적인 파라미터와 옵셔널 파라미터를 구분지어줄 수 있음

```JavaScript
// name은 필수값
function Cat(name, {age, color}) {
  this.name = name;
  // 옵셔널 파라미터를 고려하여 기본값을 nullish operator로 넣어주기
  this.age = age ?? 'unknown';
  this.color = color ?? 'unknown';
}

const siru = new Cat('siru', {
  age: 8,
  color: chaos,
});
```



### 배열에서의 활용

* 보통 대괄호([])를 사용하여 destucturing
  * 배열의 길이가 길고 필요한 요소의 인덱스가 크면 접근하는 것이 불편
* JavaScript에서의 배열은 객체
  * 이를 활용하여 원하는 인덱스의 배열 요소만 가져올 수 있음

```JavaScript
const cats = ['siru', 'mango', 'nunu'];

// 대괄호를 사용한 구조분해 할당
const [firstCat, , thirdCat] = cats;

// 중괄호를 사용한 구조분해 할당
const {0: firstCat, 2: thridCat} = cats;
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

