# [항해99 1기] [Chapter3-2] 주특기 심화 - 리액트 심화반 (4) (2021.3.29)



# 1. 토큰 기반 인증

* 이전의 방식은 사용자의 로그인 상태를 서버가 전부 가지고 있었다.
  * 서버의 세션에 사용자 정보를 넣고 로그인 여부를 기록, 저장
  * 서버에 부하가 크고 관리의 여러움
* 최근은 토큰 기반 인증 방법을 많이 사용



## 1.1 OAuth2.0

* 외부서비스의 인증 및 권한부여를 관리하는 프레임워크
* Open Authentication, Open Authorization



### 동작 방식

* 클라이언트와 서버 사이에 인증(로그인)을 하면 서버가 access_token을 준다.
* 클라이언트는 access_token을 이용하여 API 요청을 할 수 있다.
* 서버는 API  요청을 받고, access_toke을 가지고 권한 여부를 확인 후 결과를 클라이언트에게 보낸다.

> **유저가 구글 로그인을 하는 상황**
>
> **구글(Resource Server + Authorization server)은 유저의 정보를 가지고 있고 로그인 검증도 진행**
>
> **유저는 Resource Owner(자원 소유자)**



## 1.2 JWT(Json Wev Token)

* 토큰의 한 형식
* 데이터가 JSON 형태로 이루어짐



### 생김새

> **[header].[payload(내용)].[signature(서명)]**

* header: 토큰 타입과 암호화 방식 정보
* payload:  토큰에 담을 정보가 name: value 쌍으로 들어간다.
* signature: 서명 정보
  * secret key를 포함하여 header와 payload 정보가 암호화 되어 들어간다.



### 동작 방식

* 유저가 로그인을 시도
* 서버가 요청을 확인, secret key를 가지고 access_token을 발급
* 클라이언트에 JWT를 전달
* 클라이언트는 API 요청 시, Authorization header에 JWT를 담아 보냄
* 서버는 JWT의 서명을 확인하고 payload에서 정보를 확인하여 API 응답을 보냄



# 2. 웹 저장소

* http는 1번 요청을 한 후 응답을 받으면 연결이 해제
* access_token을 클라이언트에 어디엔가 저장을 해야한다.
* 쿠키, 세션, 로컬 스토리지 등의 방식이 있다.
* 프로젝트 성향에 맞추어 사용한다.



## 2.1 클라이언트 저장소

* 개발자 도구 -> Application 탭 -> 좌측 Storage 확인



## 2.2 쿠키

* 클라이언트 로컬에 저장된다.
* key:value 형태의 저장소
* 4kb의 용량 저장 가능



### 쿠키 만들기

```JavaScript
// key는 MY_COOKIE, value는 here
document.cookie = "MY_COOKIE=here;";
```



### 쿠키 가져오기

```JavaScript
console.log(document.cookie);
```



### 쿠키 삭제

* 만료일을 이전으로 돌려서 지운다.

```JavaScript
document.cookie = "MY_COOKIE=here; expires=new Date('2020-12-12').toUTCString()";
```



## 2.3 세션 스토리지

* key:value 형태의 저장소
* 세션 스토리지는 브라우저를 닫으면 제거된다.
* 자동 로그인, 장바구니 같은 것에는 부적절



### 추가하기

```javaScript
// key는 MY_SESSION, value는 here인 세션
sessionStorage.setItem("MY_SESSION", "here");
```



### 가져오기

* key로 호출

```javaScript
sessionStorage.getItem("MY_SESSION");
```



### 삭제하기

```JavaScript
// 하나만 삭제
sessionStorage.removeItem("MY_SESSION");

// 다 지우기는 clear()를 쓴다.
sessionStorage.clear();
```



## 2.4 로컬 스토리지

* 로컬 스토리지는 지우지 않으면 브라우저에 계속 남는다.
* 중요한 정보를 담지 않는다.
* key:value 형태의 저장소



### 추가하기

```JavaScript
// key는 MY_LOCAL, value는 here인 데이터를 저장
localStorage.setItem("MY_LOCAL", "here");
```



### 가져오기

```JavaScript
// key값으로 가져오기
localStorage.getItem("MY_LOCAL");
```



### 삭제하기

```JavaScript
// 하나만 삭제하고 싶다면, 이렇게 키를 통해 삭제
localStorage.removeItem("MY_LOCAL");

// 다 지우기는 clear()
localStorage.clear();
```





# Reference

[스파르타코딩클럽 리액트 심화반](https://spartacodingclub.kr/online/react/plus)