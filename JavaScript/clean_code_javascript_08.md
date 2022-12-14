# 클린코드 자바스크립트 - 타입 다루기(eqeq 줄이기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 동등 연산자(eqeq)

* 동등 연산자(Equality operator)
  * `==`
* 형 변환이 일어남
  * type casting
* **동등 연산자를 지양해야 함**

```JavaScript
'1' == 1 // true
1 == true // true
```



## 2. 엄격한 동등 연산자(eqeqeq)

* 엄격한 동등 연산자(Strict equality)
  * `===`
* 형 변환을 하지 않고 타입까지 비교
* 엄격한 동등 연산자 사용을 지향
* 동등 연산자의 형 변환을 활용하는 것이 아닌 명시적인 형 변환을 할 것

```JavaScript
'1' === 1 // false
1 === true // false
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

