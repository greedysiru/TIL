# 클린코드 자바스크립트 - 경계 다루기(min - max)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. min, max

* 최소값, 최대값을 다룰 때 명시적으로 두 값을 상수로 선언하면 가독성이 좋아짐

```JavaScript
const getRandomNumber(min, max) => Math.floor(Math.random() * (max - min + 1)) + min;

// 상수
const MIN_NUMBER = 10;
const MAX_NUMBER = 20;

// 함수 내부를 보지 않아도 상수명으로 어떤 의도로 동작할 지 알 수 있음
const randomNumber = getRandomNumber(MIN_NUMBER, MAX_NUMBER);
```



## 2. 경계 다루기

* min, max가 포함이 되는지 안되는지에 대한 컨벤션이 필요할 때가 있음
  * 이상, 이하 vs 초과, 미만
* 변수 네이밍을 통해 컨벤션을 정의할 수 있음



### 초과, 미만

* limit를 네이밍에 포함하여, 해당 수를 포함하지 않는다는 의미를 내포함

```JavaScript
const MIN_NUMBER_LIMIT = 10;
const MAX_NUMBER_LIMIT = 20;
```



### 이상, 이하

* in을 네이밍에 포함하여, 해당 수를 포함한다는 의미를 내포

```JavaScript
const MIN_IN_NUMBER = 10;
const MAX_IN_NUMBER = 20;
```







## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

[[MDN] Math.random()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/random)

