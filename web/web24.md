

# Web 요청 & 응답과정

**본 내용은 10분 테코톡 삭정님의 강의를 토대로 작성하였습니다.**



## 1. Internet

### Internet이란?

* **컴퓨터 네트워크**들을 서로 연결 지어주는 **범지구적 네트워크**
  * Inter + Network = 컴퓨터 네트워크들의 네트워크



### 컴퓨터 네트워크의 종류

* Local Area Network(LAN)
  * **근거리 통신망**, 구내 정보 통신망은 네트워크 매체를 이용하여 집, 사무실, 학교 등의 건물과 같은 가까운 지역을 한데 묶는 컴퓨터 네트워크
* MAN(Metropolitan Area Network)
* WAN(wide Area Network)



### Internet의 의의

* 이렇게 구축된 **인터넷**이라는 거대한 네트워크 위에서 **다양한 서비스**들이 동작
* Web또한 인터넷 위에서 동작하는 서비스들 중 하나
* 인터넷이 있어야 Web이 존재



## 2. Web(World Wide Web)

### Web이란?

* 팀 버너스리가 CERN에서 최초로 개발
  * Information Management: A Proposal
  * 인터넷과 HyperText를 활용하여 서로 다른 컴퓨터에서의 다른 정보 교환의 문제점을 해결하려 함
* 웹의 존재 이유는 **정보 (자원)의 공유**
* **수많은 요청과 응답 사이클의 연속**으로 이루어짐



### 서버 & 클라이언트

* 서버(Server)
  * 정보, 자원, 서비스를 **제공**하는 측. 요청을 받고 응답하는 측
  * 웹서버
* 클라이언트(Client)
  * 클라이언트는 정보, 자원, 서비스를 **사용**하는 측. 요청을 보내는 측
  * 웹 브라우저



## 3. HTTP

###  HTTP (HyperText Trasfer Protocal)

* 웹 요청과 응답에 관한 클라이언트와 서버사이의 규약(약속)
* HTTPS
  * HTTP에서 보안을 강화



### HTTP의 비연결성
* 비연결성 (Connectionless)
* 클라이언트의 요청에 대해 서버가 응답을 마치면 연결을 **끊음**
* 다음 요청은 새로운 연결을 통해 이루어짐
* 단점
  * 매번 모든 요청에 대해서 새로운 연결/해제 과정을 거치므로 **네트워크 비용**측면에서 **비효율적**
* 보완책
  * HTTP/1.1 Keep-Alive
  * 서버와 클라이언트 사이에서 통신이 없어도 **지정된 시간동안 연결**을 유지



### HTTP의 무상태성

* 무상태성(Stateless)
* 서버와 클라이언트는 **하나의 요청이 진행되는 동안만 서로를 인지**
* 단점
  * 클라이언트 인증(로그인)이 필요한 서비스에서 불편함
* 보완책
  * 쿠키, 세션, 토큰 (OAuth, JWT) - 상태를 기억하기 위한 기능들



### HTTP Status Code (응답 코드, 상태 코드)

* 클라이언트의 요청에 대해서 서버는 **요청에 대한 처리 상태**를 **숫자 코드**로 반환
* 1xx: (정보) 요청을 받았으며 프로세스를 계속함
* 2xx: (성공) 요청을성공적으로 받았으며 인식해서 처리
* 3xx: (리다이렉션) 요청 완료를 위해 추가 작업 조치가 필요
* 4xx: (클라이언트 에러) 요청의 문법이 잘못되었거나 요청을 처리할 수 없음
* 5xx: (서버 에러) 서버가 명백이 유효한 요청에 대해 충족을 실패



### HTTP Method (verbs)

* 클라이언트가 요청을 보낼 때 해당 요청의 **목적**이 뭔지 HTTP Method를 통해 명시
* GET - 서버의 리소스를 조회하고자 할 때 (READ)
* POST - 서버에 리소스를 생성하고자 할 때 (CREATE)
* PUT - 서버의 리소스를 수정할 때 (UPDATE)
* DELETE - 서버의 리소스를 삭제할 때 (DELETE)
* HEAD - GET과 동일하나, 서버에서 Body를 빼고 HEAD로만 응답 (리소스 확인의 용도)
* PATCH - 리소스의 부분만을 수정할 때
* OPTIONS - 지원 가능한 메서드 종류를 알아볼 때
* TRACE - 리소스 경로를 따라 메세지 loop-back 테스트를 실행
* CONNECT - 리소스로 식별되는 서버로의 터널을 맺을때



## 4. 웹 요청과 응답과정

### URL

* Uniform Resource Locator
* 네트워크상 자원의 위치(주소)

| https:// | www.               | exampleurl.         | com              | /info     | /aboutus.html |
| -------- | ------------------ | ------------------- | ---------------- | --------- | ------------- |
| protocol | third-level Domain | second-level domain | top-level domain | directory | file          |
|          | subdomain name     | domain name         | domain name      |           | page          |
|          | host name          | host name           | host name        | path      | path          |



### 요청을 서버로 전송 (HTTP Request)

* accept: 어떤 타입의 응답 컨텐츠를 수용할 수 있는지
* user-agent: 어떤 운영체제 어떤 브라우저인지
* cookie:  상태 기억을 위한 정보
* payload: POST, PUT 같은 HTTP 요청을 보낼 때 포함되는 데이터(JSON)



### 서버가 클라이언트로부터 요청을 받고 처리

* Request Headers 확인
  * 요청에 대한 정보 (URI, Method ...) + 클라이언트에 대한 정보 (accept, user-agent, cookie ...)
* 요청에 상응하는 로직 수행
  * 이후 응답 생성



### 서버가 클라이언트에게 응답 (HTTP Response)

* 응답을 Response Body에 담아 보냄



###  클라이언트 (웹 브라우저)가 응답을 받은 후 필요한 리소스들을 추가 요청 & 응답 받기

* CSS, JavaScript 등등
* 렌더링

# Reference

[[10분 테코톡] 삭정의 Web 요청 & 응답과정](https://www.youtube.com/watch?v=0jV7xOUcKog&t=188s)