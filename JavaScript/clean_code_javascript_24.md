# 클린코드 자바스크립트 - 분기 다루기(Nullish coalescing operator)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Nullish coalescing operator

* null 병합 연산자
* 최근에 나온 문법으로, 예전 브라우저 환경에서는 실행이 안 될 수도 있음
  * 폴리필 필요
* `??`로 표현
* 좌측에 있는 연산자가 **null 또는 undefined면 우항으로 작동**
* 단축평가와 null 병합 연산자는 같이 사용할 수 없음
  * 안전장치
  * 괄호로 묶어서 사용하는 것은 가능




### 단축 평가의 문제

* 단축 평가는 피연산자를 Truty, Falsy 로 판별
  * 0의 경우 숫자임에도 불구하고 암묵적 타입 변환으로 인해 false 취급 됨

```JavaScript
// width, height를 입력받아 넓이를 구하는 함수
const getArea = (width, height) => {
  // 단축평가를 사용하여, 좌항이 Falsy일 때 10을 width에 할당
  width = width || 10;
  height = height || 10;
  return width * height;
}

// 정상적인 연산 결과
getArea(3, 10); // 30

// 0은 Falsy에 해당하여 width, height에 기본값인 10이 할당되어 100으로 결과가 리턴
getArea(0, 0); // 100
```



### null 병합 연산자 활용

* null 병합 연산자로 단축 평가에서의 암묵적 타입변환으로 인한 문제를 해결할 수 있음

```JavaScript
const getArea = (width, height) => {
  // null 병합 연산자를 사용하여, width와 height가 전달되지 않은 경우에만 10으로 각 변수 할당
  width = width ?? 10;
  height = height ?? 10;
  return width * height;
}

getArea(3, 10); // 30

getArea(0, 0); // 0
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

