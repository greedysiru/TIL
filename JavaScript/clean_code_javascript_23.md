# 클린코드 자바스크립트 - 분기 다루기(명시적인 연산자 사용 지향하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 명시적인 연산자 사용 지향하기

### 괄호를 사용하여 명시적인 연산 표현하기

* JavaScript는 연산자 우선 순위가 있음
  * [[MDN] 연산자 우선순위](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
  * 하지만, 이것을 외우는 것은 비효율적
* 우선적으로 계산해야하는 경우, 괄호를 닫아서 연산하기

```JavaScript
// 명시적으로 괄호로 묶어 표현
if ((isLogin && token) || user) {
  // ...
}
```



### 전위, 후위 연산자 지양

* 전위, 후위 연산자는 혼동을 줄 수 있음
  * 비동기 코드에서 실행될 때
  * Loop문 안에서 실행될 때
  * 디버깅하기 어려움
* 예측가능한 코드를 작성하기 위해 전위, 후위 연산자는 지양

```JavaScript
const increment = (num) => {
  return num++;
}

const decrement = (num) => {
  return num--;
}

// 위 코드를 아래와 같이 리팩토링
const increment = (num) => {
  num = num + 1;
  return num;
}

const decrement = (num) => {
  num = num - 1;
  return num;
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

[[MDN] 연산자 우선순위](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
