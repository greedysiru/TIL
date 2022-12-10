# 클린코드 자바스크립트 - 변수(호이스팅 주의하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 호이스팅이란

* 런타임 시기에서 선언과 할당이 분리된 것
  * **선언부만 최상단으로 끌어올려지는 것**
* var의 경우 초기화하가 제대로 되어 있지 않았을 때 undefined로 호이스팅 됨
* 런타임에 예측 불가능한 문제를 일으킬 수 있음
* 함수 또한 호이스팅 됨

```JavaScript
var ex = 0;

function outer() {
  var ex;
  console.log(ex); // undefined
  ex = 10;
  
  function inner() {
    var ex = 20;
    console.log(ex); // 20
  }
  
  inner();
  
  ex = 1;
  
  console.log(ex); // 1
}

outer();
```

```JavaScript
var ex;

console.log(typeof ex); // function

function ex() {
  return 'example function';
}
```





## 2. 호이스팅 방지

* let & const로 변수를 선언
* 함수 선언식보다 const를 사용한 **함수 표현식을 사용하기**
* undefined로 호이스팅되지 않고 에러를 발생 시킴
* var사용은 지양하기

```JavaScript
const example = () => return 'example function';
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

