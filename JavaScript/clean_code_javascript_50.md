# 클린코드 자바스크립트 - 함수 다루기(Callback Function)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Callback Function

* **함수의 실행권을 다른 함수에 위임**
* eventListener
* 활용하여, 로직을 추상화하고 분리할 수 있음



### 예시

```JavaScript
// 회원가입 로직
function register() {
  const isConfirm = confirm('회원가입에 성공했습니다.');
  
  if (isConfirm) {
    redirectUserInfoPage();
  }
}

// 로그인 로직
function login() {
  const isConfirm = confirm('로그인에 성공했습니다.');
  
  if (isConfirm) {
    redirectIndexPage();
  }
}

// 위 로직들을 콜백함수를 활용하여 리팩터링
function confirmModal(message, cbFunc) {
  // 전달 받은 메시지를 확인하고
  const isConfirm = confirm(message);
  
  // 전달받은 함수를 실행
  if (isConfirm && cbFunc) {
    cbFunc();
  }
}
```



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

