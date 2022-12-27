# 클린코드 자바스크립트 - 분기 다루기(Early Return)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Ealry Return

* Ealry Return : 분기처리에서 특정 조건일 때 return 처리
* 사람이 생각하기 편하도록 코드를 정리
  * if-else, else문을 정리



### AS-IS

* 복잡한 분기처리가 포함되어 있는 코드

```JavaScript
const loginService(isLogin, user) => {
  // 1. 로그인 여부 확인
  if (!isLogin) {
    // 2.토큰 존재 여부 확인
    if (checkToken()) {
      // 3. 기가입유저 확인
      if (!user.nickName) {
        // 4-1. 가입 처리
        return registerUser(user);
      } else {
        // 4-2. 로그인 성공 처리
        refreshToken();
        return '로그인을 성공하였습니다.';
      }
    } else {
      throw new Error('토큰이 존재하지 않습니다.');
    }
}
```



### TO-BE

```JavaScript
const loginService(isLogin, user) => {
  // Early Return
  if (isLogin) {
    // 로그인이 되어있으면 함수를 종료
    return;
  }
  
  // 토큰이 없으면 에러 처리
  if (!checkToken()) {
     throw new Error('토큰이 존재하지 않습니다.');
  }
  
  // 기 닉네임이 없으면 가입 처리
  if (!user.nickName) {
    return registerUser(user);
  } 
  
  refreshToken();
  
  return '로그인 성공';
}
```







## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

