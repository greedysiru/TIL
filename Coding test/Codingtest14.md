# [동빈나]이코테 2021 강의 몰아보기 (14)(2021.1.17)



**본 내용은 해당 [강의](https://www.youtube.com/watch?v=d8KPN79UAKA&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=10) 토대로 작성**





# 개발형 코딩 테스트

* **정해진 목적에 따라서 동작하는 완성된 프로그램을 개발**하는 것을 요구하는 코딩 테스트 유형
* 일부 기업은 해커톤을 통해 채용을 진행
* **해커톤(Hackathon) :** 단기간에 아이디어를 제품화하는 프로젝트 이벤트
  * 1~2일 진행
* 분야에 따라 상세 요구사항이 다르다.
  * 모바일 클라이언트 개발 : 안드로이드, iOS 앱 개발
  * 웹 서버 개발 : 스프링(Spring), 장고(Django) 등의 서버 개발 프레임워크 활용
* 분야에 상관없이 꼭 알아야 하는 개념과 도구는 학습해야 한다.
  * 서버, 클라이언트, JSON, REST, API, ...



## 서버와 클라이언트

* 클라이언트가 요청(Request)을 보내면 서버가 응답(Response)한다.

| 웹 클라이언트 |   웹 서버    |
| :-----------: | :----------: |
|      PC       | 워크스테이션 |
|    노트북     |              |
|   스마트 폰   |              |



### 1. 클라이언트(Client) = 고객

* 서버로 요청(Request)을 보내고 응답(Response)이 도착할 때까지 기다린다.
* 서버로 응답을 받아 화면에 출력한다.
  1. 웹 브라우저 : 서버로부터 받은HTML, CSS 코드를 화면에 적절한 형태로 출력
  2. 게임 앱 : 서버로부터 받은 경험치, 친구, 귓속말 정보 등을 화면에 적절한 형태로 출력



## 2. 서버(Server) = 서비스 제공자

* 클라이언트로부터 받은 요청(Request)을 처리해 응답(Response)을 전송
  * 웹 서버 : 로그인 요청을 받아 아이디와 비밀번호가 정확한지 검사하고 그 결과를 응답



## HTTP

* **Hyper Text Transfer Protocol :** 웹 상에서 데이터를 주고받기 위한 프로토콜
  * 보통은 웹 문서(HTML)를 주고 받는 데 사용
  * 모바일 앱 및 개발 등에서 특정 형식의 데이터를 주고받는 용도로도 사용
* 클라이언트는 **요청의 목적**에 따라서 적절한 HTTP 메서드를 이용해 통신을 진행
* **대표적인 HTTP 메서드**

| HTTP 메서드 | 설명                        | 사용 예시                   |
| ----------- | --------------------------- | --------------------------- |
| GET         | 특정한 데이터의 조회를 요청 | 특정 페이지 접속, 정보 검색 |
| POST        | 특정한 데이터의 생성을 요청 | 회원가입, 글쓰기            |
| PUT         | 특정한 데이터의 수정을 요청 | 회원 정보 수정              |
| DELETE      | 특정한 데이터의 삭제를 요청 | 회원 정보 삭제              |



### 파이썬 웹 요청 예제 : GET 방식

```python
import requests
target = "http://google.com"
response = requests.get(url = target)
print(response.text)            # <!doctype html><html itemscope=" "... 웹서버가 주는 값
```



## 개발형 코딩 테스트 준비하기

* 핵심 키워드 : **RESET API, JSON**



## REST

### 1. REST의 등장 배경

* HTTP는 위처럼 다양한 HTTP 메서드를 지원
  * 실제로는 서버가 각 메서드의 기본 설명을 따르지 않아도 프로그램을 개발할 수 있다.
  * 하지만 각각 다른 방식으로 개발하면 문제가 될 수 있으므로 기준이 될 아키텍처가 필요하다.



### 2. REST 개요

* **REST (Representational State Transfer)는 각 자원(Resource)에 대해서 자원의 상태에 대한 정보를 주고받는 개발 방식**
* REST의 구성 요소
  * 자원(Resource) : URI 이용
  * 행위(Verv) : HTTP 메서드 이용
  * 표현(Representations ) : 페이로드 이용

| 자원(Resource)                | 행위(Verb)                  | 표현(Representations)                          |
| ----------------------------- | --------------------------- | ---------------------------------------------- |
| 사용자                        | 회원 등록                   | 아이디는 greedysira, 비밀번호는 123456으로     |
| **패킷 정보(URI)**            | **패킷 정보(HTTP Methond)** | **패킷 정보(Payload)**                         |
| https://www.example.com/users | POST                        | {"id" : "greedsysiru" , "password" : "123456"} |



### 3. REST API란?

* **API (Application Programming Interface) :** 프로그램이 상호작용하기 위한 인터페이스를 의미
* **REST API :** REST 아키텍처를 따르는 API를 의미
* **REST API호출** : REST 방식을 따르고 있는 서버에 특정한 요청을 전송하는 것을 의미



### 4. JSON

* **JSON (JavaScript Object Notation) :** 데이터를 주고받는 데 사용하는 경량의 데이터 형식
* JSON형식의 데이터 예시

> {
>
> "id" : "greedysiru",
>
> "password" : "123456",
>
> "age" : 30,
>
> "hobby" : ["football", "programming"]
>
> }

* JSON 데이터는 **키와 값의 쌍**으로 이루어진 데이터 객체를 저장



#### JSON 객체 사용 예제

```python
import json

# 사전 자료형(dict) 데이터 선언
user = {
    "id" : "greedysiru",
    "password" : "123456",
    "age" : 30,
    "hobby" : ["football", "programming"]
}

# 파이썬 변수를 JSON 객체로 변환
json_data = json.dumps(user, indent=4) # 들여쓰기 공백 명시
print(json_data)  # json 객체 출력
```



#### JSON 객체 파일 저장 예제

```python
import json

# 사전 자료형(dict) 데이터 선언
user = {
    "id" : "greedysiru",
    "password" : "123456",
    "age" : 30,
    "hobby" : ["football", "programming"]
}

# JSON 데이터로 변환하여 파일로 저장
with open("user.json", "w", encoding="utf-8") as file:
    json_data = json.dump(user, file, indent=4)
```



### 5. REST API 연습용 서비스

* https://jsonplaceholder.typicode.com



#### REST API 호출 실습

* API 호출 경로 : https://jsonplaceholder.typicode.com/users/1
* HTTP 메서드 : GET
* 첫번째 사용자의 정보가 나온다.

```json
{
"id" : 1,
"name" : "Leanne Graham"
"username" : "Bret",
"email" : "Sincere@april.biz",
.
..
...
}
```

* 실제로는 모든 사람에게 조회 권한을 줄 수 없으므로 별도의 인증용 토큰이 필요하다.
* https://jsonplaceholder.typicode.com/users 를 입력하면, 사용자 전체의 정보가 나온다.



#### REST API를 호출하여 회원 정보를 처리하는 예제

```python
import requests

# REST API 경로에 접속하여 응답(Response) 데이터 받아오기
target = "https://jsonplaceholder.typicode.com/users"
response = requests.get(url=target)

# 응답(Response) 데이터가 JSON 형식이므로 바로 파이썬 객체로 변환
data = response.json()

# 모든 사용자(user) 정보를 확인하며 이름 정보만 삽입
name_list = []
for user in data :
    name_list.append(user['name'])
    
print(name_list) # 모든 사용자의 이름 정보가 출력
```



