# 클린코드 자바스크립트 - 분기 다루기(부정조건문 지양하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 부정조건문 지양하기

* 부정조건문은
  * 보는 사람으로 하여금 생각을 여러번하게 만듦
* 프로그래밍 언어는 if문이 처음오게 되어있음
  * true부터 실행시키는 것이 명시적임



### NaN

* Not a Number
* 부정문이 포함되어 사람이 이해기 어려움

```JavaScript
// 숫자일 때만 동작하는 로직을 구현하기 위해 부정조건문을 써야함
if (!isNaN(example)) {
  // ...
}

// 아래처럼 isNaN을 정리하는게 이해하기 쉬움
// NaN 자료형이 아니고 타입이 number인지 검사하여 boolean으로 return
const isNumber = (num) => !Number.isNaN(num) && typeof num === 'number';

if (isNumber) {
  // ...
}
```



### 부정조건문을 사용할 수밖에 없을 때

* Early Return
* Form Validation
* 보안 혹은 검사하는 로직



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

