# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (8) (2021.3.23)

# 1. 서버와 서버리스

* 웹은 응답과 요청으로 이뤄진다.
  * 클라이언트가 서버에 요청, 서버가 클라이언트에게 응답
* 서버가 하는일
  * 데이터 관리
  * 분산처리
  * 웹 애플리케이션
* **서버리스**
  * 서버를 신경 쓸 필요가 없다.
  * 누군가 구축한 서버의 일부분을 빌려 쓸 수 있다.



# 2. Firebase

* BaaS
  * Backend as a Service
  * 백엔드와 관련된 것을 빌릴 수 있는 서비스
* [Firebase](https://firebase.google.com/?hl=ko)



## 2.1 Firebase  설정

* 사이트에서 프로젝트 만들기 버튼 클릭
* 프로젝트 이름을 정하고 약관 동의
* 프로젝트 애널리틱스 설정
* 나라 선택



## 2.2 FireStore

* realtime-database 제공
* 실시간 데이터 추가, 삭제
* 리액트의 react-firebase 패키지와 연동
* spark 요금제: 무료
* Collection: 문서의 집합
* Document: JSON 형식으로 데이터 저장



## 2.3 FireStore 설정

* 생성된 프로젝트 클릭
* Cloud Firestore 추가
* 데이터베이스 만들기 클릭
* 보안규칙 설정
  * test 모드로해야 localhost에서 firestore 데이터 요청 가능
* Cloud Firestore 위치 설정



# 3. 리액트에 Firebase 연동하기

* 패키지 설치

```shell
yarn add firebase
```



## 3.1 config 가져오기

### src 폴더 하위에 firebase.js 파일 생성

```react
//firebase.js
import firebase from "firebase/app";
import "firebase/firestore";

const firebaseConfig = {
    // firebase 설정과 관련된 개인 정보
};

// firebaseConfig 정보로 firebase 시작
firebase.initializeApp(firebaseConfig);

// firebase의 firestore 인스턴스를 변수에 저장
const firestore = firebase.firestore();

// 필요한 곳에서 사용할 수 있도록 내보내기
export { firestore };
```



### firebase SDK 추가

* firebase 대시보드에서 웹 버튼 클릭
* 앱 이름을 적고, sdk 추가영역의 텍스트의 firbaseConfig를 복사하기
* firebase.js의 해당 위치에 붙여넣기



### App.js에서 firestore 가져오기

```shell
import {firestore} from "./firebase";
```



# 4. FireStore 데이터 다루기

## 4.1 데이터 추가하기

* 콜렉션을 찾아 add

```react
collection.add({text: "코딩하기"})
```



## 4.2 데이터 수정하기

* 콜렉션을 찾아 도큐먼트 id로 set

```react
collection.doc("id").update({text: "코딩하기"})
```



## 4.3 데이터 삭제하기

* 콜렉션을 찾아 도큐먼트 id로 delete

```react
collection.doc("id").delete([도큐먼트 ID]);
```





# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

[Firebase](https://firebase.google.com/?hl=ko)