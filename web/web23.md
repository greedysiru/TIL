# REST API

**본 내용은 노마드 코더님의5분만에 제대로 설계하는 REST API 강의를 토대로 작성하였습니다.**



## 1. 좋은 API 설계

* URL에서는 동사를 사용하지 않기
* HTTP methods로 Interaction하기
  * CRUD 구현
* 명사화된 URL + HTTP methods를 사용
* Collection: 하나로 분류되는 정보 모음
* Uniaue Identifier: 고유식별자
* 슬래시(/)로 관계를 표현
  * 객체들의 관계 인터랙션을 표현



> **명사화된 URL과 HTTP methods를 조합하여 많은 URL을 생성하지 않고 의도를 알기 쉬운 API를 설계할 수 있음**



### HTTP methods

* GET
  * read
* POST
  * create
* PUT
  * update
* DELETE
  * delete



### Collection

* 작명에 복수를 사용하는 것
  * ex) /movies
* 그 다음에 고유 식별자(unique identifier) 사용하기
  * ex) movies/ineption



## 2. API 예시

### 영화 리스트 불러오기, 생성하기

```
GET /movies
POST /movies
```



### 특정 영화 삭제하기, 업데이트하기

* 컬렉션과 고유 식별자를 사용

```
DELETE /moveis/inseption
PUT /movies/inseption
```



### 특정 영화 정보 열람하기

```
GET /movies/inseption
```



## 3. Query Parameters

* url에 파라미터를 받아서 특정 조건의 정보를 조회할 수 있도록 함
  * 검색 기능
  * 페이지네이션
* 매번 조회 조건의 해당 URL을 새롭게 만드는 것보 개선된 방식

```
GET /movies?min_rating=9.8 // 평점이 9.8이상인 영화 조회

GET /movies?release_date=2021 // 개봉일이 2021년인 영화 조회

GET /movies?page=5 // 영화 목록의 5번째 페이지 조회
```



# Reference

[[노마드 코더] 5분만에 제대로 설계하는 REST API](https://www.youtube.com/watch?v=4DxHX95Lq2U)