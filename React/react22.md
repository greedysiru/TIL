# Hook의 소개

* React 16.8부터 새로 추가



## 1. Hook의 특징

* 선택적 사용
  * 코드를 다시 사용하지 않고 컴포넌트 안에서 Hook을 사용
* 이전 버전과의 호환성
* React 개념에 더 직관적인 API



## 2. 동기

### 상태 로직 재사용의 어려움

* 컴포넌트 사이에서 상태 로직 재사용의 어려움
* **render props, HOC 패턴으로 해결 가능하나, 코드의 추적이 어려워짐**
* 래퍼지옥(wrapper hell) 야기
* Hook을 사용하면, 상태 관련 로직을 추상화할 수 있음
  * 독립적인 테스트, 재사용 가능



### 복잡한 컴포넌트 로직

* 생명 주기 메서드에서 관련 없는 로직이 섞여들어가는 경우가 있음
  * componentDidMount, componentDidUpdate
* 생명주기 메서드를 기반으로 쪼개는 것 보다, Hook을 통해 서로 비슷한 것을 작은 함수 묶음으로 나누는 방법이 좋음
  * 로직 추적이 쉬어짐



### Class 컴포넌트의 문제

* Class 컴포넌트는 사람과 기계를 혼동시킴
* JavaScript에서의 this 키워드 복잡성
  * 다른 언어와는 다르게 작동
* 단, React는 Class형 컴포넌트를 제거할 계획은 없음





# Reference

[React 공식 문서](https://ko.reactjs.org/)

