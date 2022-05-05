# 38장. 브라우저의 렌더링 과정(1)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 38.0 브라우저 렌더링이란

* 자바스크립트의 대표적인 런타임 환경은 웹 브라우저
* 브라우저에서 HTML, CSS과 함께 파싱하여 렌더링
  * 렌더링 : HTML, CSS로 작성된 문서를 파싱하여 브라우저에 시각적으로 출력하는 것
* 간략한 브라우저의 렌더링 과정
  * HTML, CSS, JavaScript, 이미지, 폰트 파일 등의 리소스를 서버에 요청하여 응답 받음
  * 렌더링 엔진이 HTML, CSS를 파싱하여 DOM, CSSOM을 생성하여 렌더 트리를 생성
  * 자바스크립트 엔진은 JavaScript를 파싱하여 AST(Abstract Syntax Tree)를 생성하고 바이트코드를 변환하여 실행. 이 시점에서 JavaScript는 DOM API를 통해 DOM이나 CSSOM을 변경 가능. 변경된 DOM, CSSOM은 렌더 트리로 결합
  * 렌더 트리를 기반으로 HTML 요소의 레이아웃으 계산하고 브라우저 화면에 HTML 요소를 페인팅



## 38.1 요청과 응답

* 브라우저의 핵심 기능
  * 필요한 리소스를 서버에 요청하고 응답받아 브라우저에 시각적으로 렌더링
  * 렌더링에 필요한 리소스는 모두 서버에 존재
* 주소창
  * 서버에 요청을 전송하기 위한 도구
  * URL을 입력



### 38.1.1 URI

> https://www.sirubabo.com:80/docs/search?name=siru

* scheme(protocol): https
* Host(Domain): www.sirubabo.com
* Port: 80
* Path: /docs/search
* Query(Query String): ?name-siru
* 서버는 루트 요청에 대해 암묵적으로 index.html을 응답
  * https://www.sirubabo.com === https://www.sirubabo.com/index.html
  * 다른 파일을 요청 시에는 Path에 기술하여 서버에 요청
* 자바스크립트를 통해서도 서버에 정적/동적 데이터 요청 가능
  * ajax, REST API



## 38.2 HTTP 1.1과 HTTP 2.0

* HTTP
  * 웹에서 브라우저와 서버가 통신하기 위한 프로토콜(규약)
* HTTP/1.1
  * 하나의 요청과 응답만 처리
  * 여러 개의 요청 또는 응답을 한 번에 처리 불가
  * 동시 전송이 불가능한 구조
  * 요청 리소스의 개수에 비례하여 응답 시간도 증가하는 단점
* HTTP/2
  * 다중 요청/응답 가능
  * 여러 리소스의 동시 전송이 가능함
  * HTTP/1.1보다 50% 빠름