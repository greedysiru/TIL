# REST API (2021.3.14)

## 01. API란?

* Application Programming Interface
* 사용자가 기능을 활용할 수 있도록 하는 제어장치
  * 리모콘, 자판기의 버튼, 키보드와 마우스
* 기기와 인간의 소통창구



### 소프트웨어의 측면에서

* 제어 정보를 볼 수 있도록 하는 것
* 브라우저는 web API를 통해서 자바스크립트로부터 특정한 동작을 지시받는다.
* 윈도우는 개발자들이 시스템이나 하드웨어에 대한 세세한 지식 없이도 프로그램을 개발할 수 있다.
  * 지정된 명령어로 윈도우에서 동작을 수행하도록 소프트웨어를 짤 수 있는 windows API를 제공한다.

## 02. REST API란?

* **REST API란 HTTP 요청을 보낼 때 어떤 URI, method를 사용해야 할지 개발자 사이에 지켜지는 약속**
* 기존의 SOAP 형식을 대체
* 각 요청이 어떤 동작이나 정보를 위한 것인지 요청 모습 자체에서 추론이 가능하다.
  * 보내는 주소(URI)만으로도 뭘 원하는 요청인지를 파악 가능
* CRUD(Create, Read, Update, Delete)에 따라서 메소드를 구분하여 사용한다.
* URI는 동사가 아닌 명사로 이루어진다.



### 메소드와  CRUD

*  POST, PUT, PATCH에는 BODY가 있어서 정보를 안전하게 많이 보낼 수 있다.
  * URI를 짜고 요청을 작성한 뒤 BODY에 정보를 작성하고 실어 보낸다.
* POST하나로도 CRUD가 가능하지만 요청의 의도를 파악할 수 없다.
* GET
  * Read
  * 조회하는데 사용
* POST
  * Create
  * 새로운 정보를 추가할 때
* PUT
  * 정보를 통째로 갈아 끼울 때
* PATCH
  * 정보를 특정 방식으로 변경할 때



# Reference

[얄팍한 코딩사전 - REST API](https://www.youtube.com/watch?v=iOueE9AXDQQ)