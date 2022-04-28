# 28장. Number(1)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 28.1 Number 생성자 함수

* Number 객체
  * 표준 빌트인 객체
  * 생성자 함수 객체
  * Number 인스턴스 생성 가능
  * 인수 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체 생성
  * 인수를 전달하고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체 생성
  * 숫자가 아닌 값을 전달하면 숫자로 강제 변환
  * 숫자로 변환할 수 없으면 NaN을 할당한 래퍼 객체 생성



### 28.2 Number 프로퍼티

### 28.2.1 Number.EPSILON

* ES6 도입
* 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이
* 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용



### 28.2.2 Number.MAX_VALUE

* 자바스크립트에서 표현할 수 있는 가장 큰 양수 값
* Number.MAX_VALUE 보다 더 큰 숫자는 Infinity



### 28.2.3 Number.MIN_VALUE

* 자바스크립트에서 표현할 수 있는 가장 작은 양수 값
* Number.MIN_VALUE보다 작은 숫자는 0



### 28.2.4 Number.MAX_SAFE_INTEGER

* 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수 값



### 28.2.5 Number.MIN_SAFE_INTEGER

* 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값



### 28.2.6 Number.POSITVE_INFINITY

* 양의 무한대를 나타내는 숫자값



### 28.2.7 Number.NEGATIFVE_INFINITY

* 음의 무한대를 나타내는 숫자값



### 28.2.8 Number.NaN

* 숫자가 아님을 나타내는 값