# RESTful

**본 내용은 10분 테코톡 심바님의 강의를 토대로 작성하였습니다.**



## 1. REST

* Representational State Transfer
  * 자원의 표현에 의한 상태 전달
* 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처
* 네트워크 리소스를 정의하고 처리하는 방법을 설명하는 일련의 원칙을 기반으로하는 **아키텍처 스타일**
* 클라이언트와 서버가 데이터를 주고 받는 방식에 대해 정리한 원칙을 기반으로 함
* 로이필딩에 의해 제창
  * HTTP를 잘 활용하기 위한 원칙



## 2. 예시

```
/courses/front
/corses/back
```

* uri만 보고도 어떤 정보인지 예측할 수 있음
* 리소스를 uri에 표현해서 주고받을 정보에 대해 어느정도 예측



## 3. REST API

```
/courses/front
/courses/back
```

**위를 테이블로 표현하면**

| id   | title | body |
| ---- | ----- | ---- |
| 1    | front | ...  |
| 2    | back  | ...  |

* collection: 테이블 전체에 해당하는 부분(courses)
  * 객체들의 집합
  * 복수로 표현
* Document: 행 하나의 부분 혹은 객체(front, back)
  * 집합들 중 객체를 구분할 수 있는 값



### 주의점

* uri에는 동사를 사용하지 않음
  * 자원에 대한 행위에 대해서는 HTTP Method를 사용



## 4. HTTP Method

* Create -> POST
* Read -> GET
* Update -> PUT or PATCH
* Delete -> DELETE



### Read(조회) - GET

```
GET /courses
GET /courses/front
```

* Collection만 명시할 경우에는 전체 정보를 조회



### Create(생성) - POST

```
POST /couses/front
body { lecture: React }
```

* 어떤 것을 생성할 것인지에 대한 내용을 body에 담아 표현



### Update(수정) -  PUT

```
PUT /courses/front
body { id: 1, lecture: Vue }
```

* 어떤 것을 수정할 것인지에 대한 내용을 body에 담아 표현



### Delete(삭제) - DELETE

```
DELETE /courses/front/vue
```



# Reference

[[10분 테코톡] 심바의 RESTful](https://www.youtube.com/watch?v=NODVCBmyaXs)