# 클린코드 자바스크립트 - 함수 다루기(void & return)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## void & return

* void: 함수에 반환이 없는 것
  * 주어진 표현식을 평가하고 undefined를 반환하는 연산자
* return: 함수가 반환하는 것
* JavaScript는 기본적으로 아무것을 return하지 않을 때 undefined를 return
* 명세를 잘 확인하여 함수가 어떤 것을 반환하는지 숙지하는 습관이 중요



### 잘못된 return을 가지는 함수

* void를 return하는 경우 retrun문 뒤에서 빼주기
  * 불필요한 return이기 때문

```JavaScript
// 아래 함수들의 return 키워드 뒤에 함수는 void를 return
// return 키워드를 빼는 것이 좋음
function handleClick() {
  return setState(false);
}

function showAlert(message) {
  return alert(message);
}

// 리팩터링한 함수들
function handleClick() {
  setState(false);
}

function showAlert(message) {
  alert(message);
}
```



### return이 항상 있는 함수

* 실질적인 값을 return해야하는 함수인 경우
  * 보통 is-, get- 과같은 prefix가 붙음

```JavaScript
function isAdult(age) {
  return age > 19;
}

function getUserName(name) {
  return `유저 ${name}`;
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

