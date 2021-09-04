

# GraphQL, Apollo

**본 내용은 인프런 얄팍한코딩님의 얄팍한 GraphQL과 Apollo 강의를 토대로 작성하였습니다.**



## 1. REST API란?

* 소프트웨어간 정보를 주고받는 방식

  * GraphQL 이전부터 사용
  * 용도에 따라 적합한 것 사용하기

* IT 서비스 대다수는 여러 소프트웨어 주체간의 소통으로 이루어짐

  * 소프웨어 간의 데이터를 주고받는 형식이 필요

* **URI형식(어떤 정보를) X 요청 방식(어떻게 할 것인가)**

  | 요청 형식 | 용도          |
  | --------- | ------------- |
  | GET       | 정보 받아오기 |
  | POST      | 정보 입력하기 |
  | PUT/PATCH | 정보 수정하기 |
  | DELETE    | 정보 삭제하기 |



### REST API의 한계

* Overfetching
  * 원하지 않는 데이터까지 받아온다.
  * 낭비되는 데이터의 양이 증가
  * 네트워크의 비용과 시간이 증가
* Underfetching
  * 특정 정보에 의존적인 정보에 접근하기 위해서 여러번 요청을 해야 한다.
* **최소한의 요청으로 원하는 정보만 받아올 수 있는 방법이 필요**



## 2. GraphQL

* 필요한 정보들만 선택하여 받아올 수 있음
  * Overfetching 문제 해결
  * 데이터 전송량 감소
* 여러 계층의 정보들을 한 번에 받아올 수 있음
  * Underfetching 문제 해결
  * 요청 횟수 감소
* 하나의 endpoiont에서 모든 요청을 처리
  * 하나의 URI에서 POST로 모든 요청 가능



### 예시

* 서버로부터 teams 정보의 일부분만 받아오기
  * manager, office

```
query {
  teams {
    manager
    office
  }
}
```



* 서버로부터 해당 팀 멤버들의 정보들 받아오기

```
query {
  team(id: 1) {
    manager
    office
    members {
      first_name
      last_name
    }
  }
}
```



## 3. Apollo

* GraphQL은 명세, 형식일 뿐
* GraphQL을 구현할 솔루션 필요
  * 백엔드에서 정보를 제공 및 처리
  * 프론트엔드에서 요청 전송
  * GraphQL.js, GraphQL Yoga, AWS Amplify, Relay...



### Apollo GraphQL

* 백엔드와 프론트엔드 모두 제공
* 간편하고 쉬운 설정
* 풍성한 기능들 제공
* Apollo Server를 활용하여 백엔드 서버 제작
* Apollo Client와 React를 활용한 프론트엔드 웹 제작



# Reference

[얄팍한 GraphQL과 Apollo](https://www.inflearn.com/course/얄팍한-graphql-apollo/dashboard)