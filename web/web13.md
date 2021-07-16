# CORS

**본 내용은 10분 테코톡 코나스님의 강의를 토대로 작성하였습니다.**



## 1. 동일 출처 정책(SOP: Same-Origin Policy)

* 어떤 출처(origin)에서 불러온 문서나 스크립트가 **다른 출처**에서 가져온 리소스와 상호작용하는 것을 제한하는 중요한 보안 방식
* **출처가 같다는 것은 두 URL의 프로토콜, 호스트, 포트 세 개가 모두 같다는 것**



## 2. 크로스 도메인(Cross Domain) 이슈

* SOP 때문에 자바스크립트 (XMLHttpRequest)로 다른 웹 페이지에 접근할 때 같은 출처(Same Orign)의 페이지에만 접근 가능
* SOP를 우회해서 서로 다른 도메인 간에 통신을 할 수 있게 해줄 무언가 필요
* 개발자들이 만든 해결책
  * JSONP
  * Reverse Proxy
  * Flash Socket



## 3. CORS의 등장

* 크로스 도메인 이슈를 해결하는 표준의 필요성 대두
* W3C에서 권장사항으로 CORS 사양 발표
* 현재 활발하게 유지 관리되는 사양은 WHATWG의 Fetch Living Standard



### CORS란

* Cross-Origin Resource Sharing
* 웹 브라우저에서 외부 도메인 서버와 통신하기 위한 방식을 표준화한 스펙
* 서버와 클라이언트가 **정해진 헤더를 통해 서로 요청이나 응답에 반응할지 결정하는 방식**



## 4. CORS의 동작 방식

* 간단한 요청(Simple Requests)
* 사전 요청(Prefligt Requests)
* 인증을 이용하는 요청(Credential Requests)



### 간단한 요청(Simple Requests)

* 기존 데이터에 사이드 이펙트를 일으키지 않는 요청
* CORS **사전 요청**을 발생시키지 않는 요청
* 조건
  * GET, HEAD, POST 중 한가지 방식을 사용
  * Custiom Header가 존재하지 않음
  * POST일 경우, Content-Type이 아래 셋 중 하나를 만족
    * application/x-www-from-urlencoded
    * multipart/form-data
    * text/plain



### 사전 요청(Preflight Requests)

* 본 요청을 보내기 전에 사전 요청을 보내 서버가 이에 응답이 가능한지 확인하는 방법
* 사전 요청을 보내는 경우
  * GET, HEAD, POST 이외의 요청
  * POST 요청일 경우 Content-Type 이 application/x-www-form-urlencoded, multipart/form-data, text/plain이 아닐 때
  * 커스텀 헤더가 포함된 경우
* 과정
  * 동일한 URI에 OPTIONS method로 요청(Preflight)
  * 요청에 대해 서버에서는 허용되는 method, 허용하는 헤더, 쿠키 허용 여부를 응ㄷ갑
  * 요청의 응다빙 요청을 허용하는 조건이라면 본 요청을 보냄



### 인증을 이용한 요청

* XHR은 기본적으로 요청을 보낼 때 쿠키를 전송하지 않음
* 요청에 쿠키를 포함하고 싶다면, XMLHttpRequest 객체의 withCredentials 프로퍼티 값을 ture로 설정
* 서버 측도 Access-Control-Allow-Credentials 응답 헤더를 true로 설정

# Reference

[[10분 테코톡] 코나스의 CORS](https://www.youtube.com/watch?v=_sLjXviYivM&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=103)