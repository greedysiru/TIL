# 클린코드 자바스크립트 - 함수 다루기(Rest Parameters)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Rest Parameters

* 가변인자
  * 들어오게 되는 인자의 수가 변할 수 있음
* Rest Parameters를 활용해서 가변인자를 다룰 수 있음



### arguments

* 함수에서 받은 인자들을 가지고 있는 객체
* Iterator
  * 배열이 아니어서 배열 메서드를 사용하기 위해 Array.from 메서드가 필요
* 함수 선언식일 때만 arguments 객체를 가짐
* 추가적인 인자를 받을 수 없음

```JavaScript
function sumTotal() {
  return Array.from(arguments).reduce((acc, cur) => acc + cur);
}

sumToal(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
```



### Rest Parameters

* (...)을 사용하여 표현
  * spread operator와 다른 것임에 주의
* 함수 선언부에서 명시해야 함
* Rest Parameter로 들어온 것은 배열
* 명시적으로 추가적인 인수를 받을 수 있음
* 인자중에서 가장 마지막에 들어가야 함
  * 다른 인자와 사용할 시, 무조건 마지막에 들어가야 함

```JavaScript
// 추가적인 인수를 받을 수 있음
function sumTotal(initValue, ...args) {
  return args.reduce((acc, cur) => acc + cur, initValue);
}

sumToal(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

