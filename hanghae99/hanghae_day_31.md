

# [항해99 1기] [Chapter3-2] 주특기 심화 - 리액트 심화반 (6) (2021.3.31)



# Firebase Authentication

* 파이어베이스에서 지원하는 인증 기능
* [공식 문서](https://firebase.google.com/docs/auth/web/manage-users?hl=ko)



## 1. 설치

```shell
yarn add firebase
```



## 2. auth 설정

* firebase.js에서 아래와같이 설정

```javascript
import firebase from "firebase/app";
import "firebase/auth";

const firebaseConfig = {
// 파이어베이스의 인증 정보
};

firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();

export { auth };
```

















# Reference

[스파르타코딩클럽 리액트 심화반](https://spartacodingclub.kr/online/react/plus)

