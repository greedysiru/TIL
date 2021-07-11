# Web Server vs WAS

**본 내용은 10분 테코톡 알리님의 강의를 토대로 작성하였습니다.**



## 1. Web Server

### Web Server란?

* **웹 브라우저(클라이언트)**로부터 **HTTP 요청**을 받아, HTML 문서와 같은 **정적 컨텐츠**를 제공하는 프로그램
* 정적 컨텐츠
  * 요청 인자 값에 상관없이 달라지지 않는 컨텐츠(HTML, CSS, image...)
  * 어느 사용자 요청이든 항상 동일한 컨텐츠



### Web Server의 기능

* 클라이언트로부터 **HTTP 요청**을 받을 수 있다.
* 정적 컨텐츠 요청 시
  * 정적 컨텐츠를 제공
* 동적 컨텐츠 요청 시
  * Web Application Serv er(WAS)로 전달하여 WAS가 처리한 결과를 클라이언트에 전달



## 2. Web Application Server

### Web Application Server란?

* **DB 조회**나 다양한 로직 처리를 요구하는 **동적인 컨텐츠를 제공**하기 위해 만들어진 프로그램
* 동적 컨텐츠
  * 요청 인자값에 따라 달라지는 컨텐츠
  * 사용자에 따라 달라질 수 있다.



### WAS의 기능

* 클라이언트로부터 **HTTP요청**을 받을 수 있다. (Web Server가 내장)
* 요청에 맞는 정적 컨텐츠 제공
* DB조회나 다양한 로직 처리를 통해 동적 컨텐츠를 제공



## 3.Web Server와 WAS를 같이 사용하는 것의 장점

* 책임 분할을 통한 서버 부하 방지
  * 정적 컨텐츠는 Web Server, 동적 컨텐츠는 WAS가 담당
* 여러대의 **로드밸런싱**
  * WAS가 처리해야 하는 요청을 여러 WAS가 나누어서 처리
* 여러대의 WAS **Health Check**
  * 서버에 주기적으로 HTTP 요청을 보내 서버의 상태 확인
  * 특정 url 요청에 200 응답이 오는지
* **보안**
  * **리버스 프록시**를 통해 실제 서버를 외부에 노출하지 않을 수 있다.

> **WAS만으로도 서비스는 가능하다. 하지만, 서비스 확정성, 안정성을 고려하면 앞 단에 Web server를 두는 것이 유리하다.**

# Reference

[[10분 테코톡] 알리의 Web Server vs WAS](https://www.youtube.com/watch?v=mcnJcjbfjrs&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=12)