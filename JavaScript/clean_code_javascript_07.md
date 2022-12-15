# 클린코드 자바스크립트 - 타입 다루기(undefined & null)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. undefined vs. null

* undefined: 정의하지 않은 것
* null: 없다는 것을 명시적으로 표현



## 2. 타입변환에서의 차이

* null, undefined는 암묵적 타입변환에서 혼란의 여지를 일으킬 수 있음
* 컨벤션을 갖추어 null, undefined로 인해 발생할 오류를 방지해야 함

```JavaScript
// null
!null // true
!!null // false

null === false // false
!null === true // true

typeof null // Object

// 산술연산자와 만나면 null은 0취급
null + 10 // 10

// undefined
// 선언했지만, 값은 할당하지 않음
let ex;

ex // undefined

!undefined // true

undefined == null // true
undefined === null // false
!undefined === !null // true

typeof undefined // 'undefined'

undefined + 10 // NaN
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

