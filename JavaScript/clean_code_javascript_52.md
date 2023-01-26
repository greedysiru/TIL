# 클린코드 자바스크립트 - 함수 다루기(Closure)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Closure

### Closure 예시

* 외부함수가 실행이 완료되었음에도 불구하고 그 함수의 컨텍스트를 기억하고 있음

```JavaScript
function add(num1) {
  return function sum(num2) {
    return num1 + num2;
  }
}

// 각 함수에는 num1을 기억하고 있는 함수가 할당되어 있음
const addOne = add(1);
const addTwo = add(2);

addOne(3); // 4
addTwo(3); // 5
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

