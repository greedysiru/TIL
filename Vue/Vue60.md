# Vue.js - 에러 핸들링

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. try, catch

* try, catch 문은 실행할 코드문을 표시하고 예외가 발생할 경우의 응답을 처리
* api 호출 시 오류 발생할 때 주로 사용
  * ex) 로그인 실패, 회원가입 실패, 데이터 불러오기 실패

```JavaScript
try {
  // 실행할 코드문
} catch(error) {
  // 예외가 발생할 경우의 코드문
}
```



## 2. 에러 핸들링

* try, catch 문을 활용하여 api 호출 시의 에러 핸들링에 응용
* try 문 안에는 비지니스 로직
* catch 문 안에는 에러 핸들링 로직
* 에러가 발생했을 때 명시적으로 사용자에게 피드백을 주는 것이 좋음
* 버그 개선을 위해서도 에러 핸들링은 필수

```JavaScript
try {
  // 비지니스 로직
  const userData = {
    username: this.username,
    password: this.password,
  };
  // loginUser는 서버로 userData를 넘겨 로그인을 요청하는 함수
  const { data } = await loginUser(userData);
  this.logMessage = `${data.user.username} 님 환영합니다.`;
  this.initForm();
} catch (error) {
  // 에러 핸들링 코드
  // 로그인을 실패했을 때 이 코드를 실행
  this.logMessage = error.response.data;
}
```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

