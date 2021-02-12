# [코드잇] 프로그래밍 핵심 개념 in JavaScript (2)(2021.2.13)



**상세 내용 [블로그](https://greedysiru.tistory.com/200?category=860707) 참고**

# 추상화

## 01. 할당 연산자 (Assignment operators)

* **등호(=) : 할당 연산자, 오른쪽의 피연산자를 왼쪽의 피연산자에 할당한다.**
  * 할당 연산자의 오른쪽부터 처리
  * 처리된 값을 왼쪽의 피연산자에 할당



### 예시

```JavaScript
let x = 5;
x = x - 2;
console.log(x); // 3 출력
```



## 02. 복합 할당 연산자 (Compound assignment operators)

```JavaScript
// 두 줄씩 같은 표현
x = x + 1;
x += 1;

x = x + 2;
x += 2;

x = x * 2;
x *= 2;

x = x - 3;
x -= 3;

x = x / 2;
x /= 2;

x = x % 7;
x %= 7;
```



### 증가(increment), 감소(decrement) 연산자

```JavaScript
// 세 줄씩 같은 표현
x = x + 1;
x += 1;
x++;

x = x - 1;
x -= 1;
x--;
```



## 03. 함수의 실행 순서

* 기본적으로 위에서 아래로 한 줄씩, 왼쪽에서 오른쪽으로 실행한다.
* 함수의 선언후, 호출 된다면 그 때 함수 내부의 코드가 실행된다.



### 예시

```JavaScript
function square(x) {
  return x * x;
}

console.log('함수 호출 전');
console.log(square(3) + square(4));
console.log('함수 호출 후');

//함수 호출 전
//25
//함수 호출 후
```



## 04. return문 제대로 이해하기

* **함수에서 어떤 값을 되돌려주는 output의 역할**
* **함수의 실행을 중단**



### 예시

```JavaScript
function square(x) {
  console.log('return 전');
  return x * x; // 함수 실행 중단
  console.log('return 후'); // Daed Code
}

console.log('함수 호출 전');
console.log(square(3));
console.log('함수 호출 후');

// 함수 호출 전
// retrun 전
// 9
// 함수 호출 후
```

* Dead Code : 실행되지 않는 코드
  * 작성하지 않도록 한다.



## 05. return과 console.log의 차이

* **return은 함수를 실행 후 어떤 값을 되돌려준다.**
* **console.log는 console에 어떤 값을 출력해 주는 함수**



## 06. 옵셔널 파라미터

* **선택적으로 파라미터를 전달 할 수있다.**



### 예시

```Javascript
function introduce(name, age, city = '서울'){ // 옵셔널 파라미터
  console.log(`나는 ${name}이라고 해.`);
  console.log(`나이는 ${age}이야.`);
  console.log(`사는 도시는 ${city}이야.`);
}

introduce('코드잇', 4, '인천'); // 값을 모두 입력한 경우
console.log('');
introduce('greedysiru', 4) // 파라미터 값을 생략한 경우
// 나는 코드잇이라고 해.
// 나이는 4이야.
// 사는 도시는 인천이야.

// 나는 greedysiru라고 해.
// 나이는 4이야.
// 사는 도시는 서울이야.
```

* 옵셔널 파라미터를 생략하면, 함수 선언에서 설정한 기본값을 사용한다.
* 옵셔널 파라미터는 **가장 뒷 자리에 선언**해야 한다.



## 07. 변수의 scope

* **변수의 범위, 영역**
  * **변수는 유요한 범위**가 있어, 범위를 벗어나면 오류가 발생한다.



### 블록문 (Block Statement) 안에서 선언된 변수

* JavaScript에서 **중괄호( { } )**로 감싸진 부분을 **블록문**이라 한다.

```JavaScript
function myFunction() { // 블록문
  let x = 3; // 지역변수
  console.log(x);
}

myFunction(); // 3
console.log(x); // 오류
```

* **지역변수, 로컬변수 : 블록문 안에서 선언된 변수**
  * **블록문 내**에서만 사용할 수 있다.
  * **블록문 내에서 변수 사용시, 가장 먼저 로컬 변수를 찾아 사용한다.**
  * 그 다음에는 글로벌 변수를 찾는다.



### 전역 변수

* **전역변수, 글로벌 변수 : 블록문 밖에서 선언된 변수**
  * 어느곳에서나 사용할 수 있다

```JavaScript
let x = 3; // 전역변수
function myFunction() { // 블록문
  console.log(x);
}

myFunction(); // 3
console.log(x); // 3
```



## 08. 상수 (constant)

* **변하지 않는 항상 일정한 값**
* 선언시 값을 같이 입력
* 수정할 일이 없는 값을 다룰 때 사용
  * ex. 원주율

> const PI = 3.14



### 상수 작명법

* **알파벳을 대문자, 두 개이상의 단어를 밑줄로 구분한다.**
* 상수와 변수를 구분하기 위함

> myNumber -> MY_NUMBER



# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)