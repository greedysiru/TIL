# 클린코드 자바스크립트 - 분기 다루기(드모르간의 법칙)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 드모르간의 법칙

* 부정 연산은 아래의 예서처럼 바꿀 수 있음
  * 부정 연산은 혼동의 여지가 있으므로 드모르간의 법칙을 활용하여 부정 연산을 소거해줌

```JavaScript
// boolean 타입인 두 변수 A, B

// 서로 동치
!(A && B) === !A || !B
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

