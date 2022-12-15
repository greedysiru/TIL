# 클린코드 자바스크립트 - 타입 다루기(형변환 주의하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 암묵적 형변환

* 느슨한 검사(eqeq)는 암묵적 형변환이 일어나서 문제를 일으킴
* JavaScript가 코드를 평가했을 때 암묵적인 형변환을 일으킴

```JavaScript
99 + 'string' // '99string'

!!'string' // true

!!'' // false
```



## 2. 명시적 형변환

* wrapper 객체를 활용해서 명시적으로 형변환할 것
  * 개발자가 명시적인 형변환하기
* 안전하게 형변환을 하여, 오류를 방지

```JavaScript
String(99 + 'string') // '99string'

Boolean('string') // true

Boolean('') // false
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

