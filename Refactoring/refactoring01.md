# Refactoring - 첫 번째 예시(1)

**본 내용은 마틴 파울러의 Refactoring 2판을 토대로 작성되었습니다.**



## 들어가기 전에

### 저자 마틴 파울러는?

* ThoughtWorks의 수석 과학자
* 제어 역전(Inversion of Control)과 의존성 주입(Dependency Injection)용어를 대중화시킨 장본인



### 리팩토링이란?

* 코드를 이해하기 쉽고 수정하기 편하게 만드는 것
* 겉으로 드러나는 코드의 기능은 바꾸지 않으면서 내부 구조를 개선하는 방식으로 소프트웨어 시스템을 수정하는 과정
* 버그가 생길 가능성을 최소로 줄이면서 코드를 정리하는 정제된 방법
* 코드를 작성하고 난 뒤에 설계를 개선하는 것



### 코딩 후 설계 개선?

> **잘못된 설계, 엉망인 설계 -> 체계적으로 설계된 코드**

* 예전의 소프트웨어 개발 방법은 설계부터 하고 코드를 작성하는 식
* 리팩토링은 이를 반대로 함
* 처음부터 완벽한 설계를 갖추기보다는 개발을 진행하면서 지속적으로 설계
* **새로운 요구사항은 한 부대씩 몰려온다.**



## 리팩터링: 첫 번째 예시

### 시스템의 설계가 나쁘면

* 수정하기 어려움
* 원하는 동작을 수행하도록 하기 위해 수정해야할 부분을 찾고, 기존 코드와 잘 맞물려 작동하게 할 방법을 강구하기 어려움
* 수정을 하여도 버그가 생길 가능성이 높아짐



### 프로그램이 새로운 기능을 추가하기에 편한 구조가 아니라면?

* 먼저 기능을 추가하기 쉬운 형태로 리팩터링
* 코드를 여러 함수와 프로그램 요소로 재구성
* 중복코드를 최소화
  * 오래 사용할 프로그램이라면 중복 코드는 골칫거리가 됨



### 테스트 코드

* **리팩터링의 첫 단계**
* 리팩터링할 코드 영역을 꼼꼼하게 검사해줄 테스트 코드부터 마련
  * JavaScript - jest
* 버그 검출기 역할
* 원하는 내용을 소스 코드와 테스트 코드 양쪽에 적어 두면 중복 검사로 실수 가능성을 크게 줄일 수 있음
* 작은 단위의 리팩토링을 진행하고 컴파일 -> 테스트해서 실수를 확인하기



### 함수 추출하기

* 전체 동작을 각각의 부분으로 나눌 수 있는 지점 찾기
* 코드 조각을 별도의 **함수로 추출하기**
* 추출한 함수에는 그 코드가 하는 일을 설명하는 이름을 지어주기



### 리팩터링 원칙

* 간단한 수정이라도 리팩터링 후에는 항상 테스트하는 습관을 들이기
* 오류가 생기더라도, 변경 폭이 작아 살펴볼 범위도 좁아서 문제를 찾고 해결하기가 수월
* **조금씩 변경하고 매번 테스트하는 것은 리팩터링 절차의 핵심**



### 적절한 변수 이름

* JavaScript와 같은 동적 타입 언어를 사용할 때는 타입이 드러나도록 작성하면 도움이 됨
  * 매개변수 이름에 접두어로 타입 이름을 적음
* 매개변수의 역할이 뚜렷하지 않을 때는 부정 관사(a/an)을 붙임
* 좋은 코드라면, 하는 일이 명확하게 드러나야 하며 이때 변수 이름은 큰 역할을 함