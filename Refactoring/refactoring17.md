# Refactoring - 기능 이동(1)

**본 내용은 마틴 파울러의 Refactoring 2판을 토대로 작성되었습니다.**



## 기능 이동

## 1. 함수 옮기기



### 설명

* **좋은 소프트웨어의 핵심은 모듈성에 있음**
* 모듈성
  * 프로그램의 기능을 수정할 때 해당 기능과 깊이 관련된 작은 요소만 이해해도 수정이 가능한 것
  * **모듈성을 높이기 위해서 서로 연관된 요소들을 묶어야 함**

* 함수 옮기기 리팩터링은 서로 연관된 요소들을 묶기위한 것



## 2. 필드 옮기기

### 설명

* **프로그램의 진짜 힘은 데이터 구조에서 나옴**
* 아귀가 맞는 데이터 끼리 묶어야 함
* 적절하지 않은 데이터 구조는 보이는 **즉시 수정**해야 함
* **클래스는 함수가 곁들여진 레코드**
  * 캡슐화 되어 있어, 데이터를 이리저리 옮기기 쉬움

* 반대로, 날 것의 레코드는 변경하기 까다로울 것
  * 클라이언트에서도 코드 수정이 필요하기 때문




## 3. 문장을 함수로 옮기기

* 반대 리팩터링 : 문장을 호출한 곳으로 옮기기



### 설명

* **중복 제거는 코드를 건강하게 관리하는 가장 효과적인 방법 중 하나**
* 특정 함수의 앞 또는 뒤에서 똑같은 코드가 호출되면 그 함수로 옮기기



## 4. 문장을 호출한 곳으로 옮기기

* 반대 리팩터링 : 문장을 함수로 옮기기



### 설명

* 추상화의 경계를 잡는 것은 어려움
* 프로젝트가 진행되면서 단순한 한 가지 일을 하던 함수가 두 가지 이상의 다른 일을 수행하게 바뀔 수가 있음
  * 함수에서 달라진 동작을 꺼내서 옮기기