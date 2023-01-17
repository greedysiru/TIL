# 클린코드 자바스크립트 - 객체 다루기(직접 접근 지양하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 직접 접근 지양하기

* 객체의 데이터에 접근하려면 안전하게 해야 함

* 예측 가능하도록 데이터 조작을 통제해야함

* 직접 접근을 지양하기

* getter, setter를 사용하기

  

### flux의 예시

* action -> reducer -> state 변화
* **복잡한 과정을 거치는 이유는 상태 변화를 예측가능하도록 하기 위함**
* redux등



### 안전한 상태 변화 관리로의 리팩터링

```JavaScript
// 유저의 인가 상태를 관리하는 객체
const auth = {
  isLogin: false,
  isValidToken: false,
}

// 함수에서 객체로 직접 접근하여 변화시킴
// 상태 변화를 추적하기가 어려움
const login = () => {
  auth.isLogin = true;
  auth.isValidToken = true;
}

const logout = () => {
  auth.isLogin = false;
  auth.isValidToken = false;
}

// auth에 따라 UI를 렌더하는 함수
render(auth);
```

```JavaScript
const auth = {
  isLogin: false,
  isValidToken: false,
}

// 데이터를 변화시키는 레이어를 분리
const setLogin = (bool) => {
  model.isLogin = bool;
  serverAPI.log(model.isLogin);
}

const setValidToken = (bool) => {
  model.isValidToken = bool;
  serverAPI.log(model.isValidToken);
}

// 함수에서 객체로 직접 접근하여 변화시킴
// 상태 변화를 추적하기가 어려움
const login = () => {
  setLogin(true);
  setValidToken(true);
}

const logout = () => {
  setLogin(false);
  setValidToken(false);
}

// auth에 따라 UI를 렌더하는 함수
render(auth);
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

