# [코드잇] 프로그래밍 시작하기 in JavaScript (2021.2.12)



**상세 내용 [블로그](https://greedysiru.tistory.com/195) 참고**



# 프로그래밍 맛보기

## 01. 세미콜론

* **프로그래밍 언어의 마침표**
* 문장 끝에 사용
* JavaScript, C, C++. Java 등
* 생략하면 오류가 발생할 가능성이 있다.



## 02. 코멘트

* **주석, comment**
* **어떤 의도로 코드가 작성 되었는지 설명**
* **구현한 코드가 어떤 동작을 하는지 기록**
* 컴퓨터가 읽지 않게 한다.
* 필요한 만큼, 간결하게 사용할 것



### 예시

```Javascript
// 15를 출력하는 코드
console.log(10 + 5);
console.log(3 * 5);
/*
여러줄 주석을 쓸 수도 있다.
*/
```



## 03. 자료형 개요

### 프로그래밍이란?

* **컴퓨터로 복잡한 계산을 하는 것**



### 자료형 (Data type)

* 다양한 값들의 유형



### 숫자 (Number)

* **정수 (Integer)**
  * -8, -6, -1, 0, 5, 10 ...
* **실수 (Floating point)** : 소수점을 가지는 숫자
  * 3.14, -1.1, 1.6 ...
* 숫자형 데이터는 사칙연산이 가능



### 문자열 (String)

> "Hello"
>
> 'Codeit'

* **감싸는 따옴표는 통일한다.**
* 더하기(+)를 통해 연결이 가능



### 불린 (Boolean)

* **참(true)과 거짓(false)**
* **어떤 조건에 의한 결과값으로 사용**

> 8 > 6
>
> true
>
> 8 < 6
>
> false



## 04. 추상화 개요

* **여러 가지 사물이나 개념에서 공통되는 특성이나 속성 따위를 추출하여 파악하여 적용**
* 구체적인 정보 -> **꼭 필요한 핵심**
* **복잡한** 것들을 **목적**에 맞게 **단순화** 하는 것
* **목적**을 명확히, **불필요**한 것들은 숨기기, **핵심**만 드러내기



### 프로그래밍에서의 추상화

*  자기자신, 컴퓨터, 동료, 사용자와의 소통
* 프로그래밍의 추상화의 연속



## 05. 변수

* **값에 이름을 부여**

### 변수 선언

> let 변수명;

### 변수 초기화

> 변수명 = 값;

* **=**  : 할당 연산자
  * 오른쪽의 값을 왼쪽의 변수에 저장한다.



### 선언과 초기화 동시에 하기

```JavaScript
let coffeePrice = 3800;
```



## 06. 변수 작명

### 꼭 지켜야 하는 룰

* 첫 글자는 문자, 밑줄(_), 혹은 달러 기호($)로 시작한다.
* 둘 번째 글자부터는 숫자도 가능
* 대문자와 소문자는 구별
* 예약어(JavaScript에서 사용하는 단어)는 사용하지 않는다.
  * if, for, let 등



### 지키면 좋은 룰

* **일관성 있는 코드를 작성하기 위한 약속**
* 의미없는 이름을 사용하지 않는다.
* 너무 추상적인 이름을 사용하지 않는다.
* **들여쓰기는 space 2칸**을 사용한다.
* **camelCase 작명법**을 사용한다.

> let goodVariableName;



## 07. 함수

* 다양한 명령들을 저장



### 함수 선언

> function 함수명 (파라미터) {
>
> ​		명령;
>
> }



### 함수 호출

> 함수명 (파라미터);



## 08. 파라미터

* Parameter(매개변수)
* **함수 내에서 변수처럼 사용**



### 예시

```Javascript
function greeting(name) {
  console.log('Hi!');
  console.log(name);
}

greeting('greedysiru');
// hi!
// greedysiru 출력
```



## 09. 여러개의 파라미터

* 함수에서 여러개의 파라미터를 사용할 수 있다.
* 쉼표로 구분



### 예시

```Javascript
function printSum(num1, num2){
  console.log(num1 + num2);
};

printSum(2, 4);
// 6 출력
```



## 10. return문

* 함수의 output
* **함수의 명령을 실행 후 다시 반환한다.**



```Javascript
function getTwice(number){
  return number *2;
}

console.log(getTwice(5));
// 10 출력
```





# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)

