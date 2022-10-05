# 기초 JS, CS 상식 - 표현식과 연산자



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. 표현식

* Expressions
* 어떠한 결과 값으로 평가되는 식
* 숫자, 문자열, 논리값, 변수, 상수 ,함수 호출 등으로 조합 가능



## 2. 연산자

* 표현식은 연산자로 조합되어 새로운 표현식이 됨



### 할당 연산자

* 오른쪽 표현식을 왼쪽 피연산자 값에 할당하는 연산자
* 등호(=)
* 다른 연산자와 같이 사용하여 복합 할당 연산자로 이용

```JavaScript
// 복합 할당 연산자
let example = 0;

example += 1; // 덧셈 할당
example -= 1; // 뺄셈 할당
example *= 2; // 곱셈 할당
example /= 2; // 나눗셈 할당
example %= 3; // 나머지 할당
example <<= 4; // 비트 왼쪽 이동 할당
example >>= 4; // 비트 오른족 이동 할당
```



### 비교 연산자

* 좌측 피연산자와 우측 피연산자를 비교하는 연산자
* true 혹은 false를 반환

```JavaScript
ex1 == ex2; // 동등
ex1 != ex2; // 부등
ex1 === ex2; // 일치
ex1 !== ex2; // 불일치
// 대소 관계
ex1 > ex2;
ex1 < ex2;
ex >= ex2;
ex <= ex2;
```



### 산술 연산자

* 덧셈, 뺄셈, 곱셈, 나눗셈을 하는 연산자
* Number를 반환



### 비트 연산자

* 비트를 직접 조작하는 연산자

```JavaScript
const x = 10; // 1010
const y = 12; // 1100

x & y; // AND - 1000
x | y; // OR - 1110
x ^ y; // XOR - 110
// 보수
~x; // NOT
x << 1 // Left Shift - 10100
x >> 1 // Right Shift - 101
```



### 논리 연산자

* Boolean을 통해 참과 거짓을 검증하는 연산자

```JavaScript
x && y; // AND
x || y; // OR
!x; // NOT
```



### 삼항 연산자

* 조건에 따라 값을 선택하는 연산자
* 조건 ? 참 : 거짓



### 관계 연산자

* 객체에 속성이 있는지 확인하기 위한 연산자
* Boolean을 반환

```JavaScript
'age' in user;
```



### typeof

* 피연산자의 타입을 문자열로 반환하는 연산자



## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

