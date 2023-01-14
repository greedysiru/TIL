# 클린코드 자바스크립트 - 객체 다루기(Object.freeze)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Object.freeze

* 객체를 동결하는 메서드
* 인자로 넘긴 객체는 동결이 됨
* 동결
  * 프로퍼티에 새로운 값을 할당하여도 변하지 않음
  * 새로운 프로퍼티를 할당할 수 없음
* Object.isFrozen()
  * 객체의 동결 여부를 체크할 수 있는 메서드

```JavaScript
const CATS = Object.freeze({
  SIRU: "SIRU",
  NUNU: "NUNU",
});

Object.isFrozen(CATS); // true
```



### 깊은 영역에서의 freeze

* freeze는 깊은 영역의 객체는 동결시키지 못함
* 깊은 영역의 프로퍼티 변경 방지를 할 수 없음
* 깊은 영역에 새로운 프로퍼티를 할당할 수 있음

```JavaScript
const CATS = Object.freeze({
  SIRU: "SIRU",
  NUNU: "NUNU",
  OTHERS: {
    MANGO: 'MANGO',
  }
});

Object.isFrozen(CATS.OTHERS); // false
```



### 깊은 영역을 동결하려면

* lodash와 같은 유틸 라이브러리 사용
* 직접 유틸 함수 정의
* stackoverflow
* TypeScript readonly 키워드



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

