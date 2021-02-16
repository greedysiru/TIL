# [코드잇] 프로그래밍과 데이터 in JavaScript (3)(2021.2.16)



**상세 내용 [블로그](https://greedysiru.tistory.com/206?category=860707) 참고**



# 자료형 심화

## 01. 다양한 숫자 표기법

### 지수 표기법

* 단위가 큰 정수, 자릿수가 많은 소수를 표현
* 알파벳 e 이용
  * e를 기준으로 왼쪽의 수에 오른쪽의 수만큼 10의 거듭제곱을 곱한다.
  * 오른쪽의 수가 음수인 경우, 그만큼 10의 거듭제곱을 나눈다.

```JavaScript
let myNumber1 = 1e9;
let myNumber2 = 16e-5;

console.log(myNumber1); // 1000000000
console.log(myNumber2); // 0.00016
```



### 16진법, 8진법, 2진법

console.log로 출력 시 10진법 표기로 출력된다.

* 16진법 (Hexadecimal)

```JavaScript
let hex1 = 0xff; // 255
let hex2 = 0xFF; // 255
```

* 8진법 (Octal)

```JavaScript
let octal = 0o377; // 255
```

* 2진법 (binary numeral system)

```JavaScript
let binary = 0b11111111; // 255
```



## 02. 숫자형 메소드

* **숫자 또한 객체이다.**



### toFixed 메소드

* 소수를 다루는 메소드
* **parameter로 숫자값을 전달하면 그만큼 소수점 아래의 자릿수를 고정한다.**
  * 반올림하여 고정
  * 부족한 자릿수는 0으로 채운다.
  * **자료형은 문자열로 바뀐다.**
  * 앞에 +를 붙이면, 숫자형으로 변환된다. (number 함수와 똑같은 결과)
* 범위는 0 ~ 100

```JavaScript
let myNumber = 0.3591;

console.log(myNumber.toFixed(3)); // 0.359
```



### toString 메소드

* **parameter로 전달받은 숫자의 진법으로 변환**
  * 자료형은 문자열로 바뀐다.
* 범위는 2 ~136

```JavaScript
let myNumber = 255;

console.log(myNumber.toString(2)); // 11111111
console.log(myNumber.toString(8)); // 377
console.log(myNumber.toString(16)); // ff
```



### 주의점

* 정수형의 숫자값에서 점 표기법으로 메소드를 사용할 때, **점을 두 개 쓴다.**
* **괄호**를 감싸주는 방법도 있다.

```JavaScript
console.log(255..toString(2));
console.log((255).toString(8));
```



## 03. Math 객체

* **다양한 연산들을 유용하게 사용**



### 절댓값 (Absolute Number)

```JavaScript
console.log(Math.abs(-10)); // 10
```



### 최댓값 (Maximum)

* 전달받은 Parameter 중에서 가장 큰 값  return

```JavaScript
console.log(Math.max(2, -1, 4, 5, 0)); // 5
```



### 최솟값 (Minimum)

```JavaScript
console.log(Math.min(2, -1, 4, 5, 0)); // -1
```



### 거듭제곱 (Exponentiation)

```JavaScript
console.log(Math.pow(2, 3)); // 8
```



### 제곱근 (Square Root)

```JavaScript
console.log(Math.sqrt(25)); // 5
```



### 반올림 (Round)

```JavaScript
console.log(Math.round(2.3)); // 2
```



### 버림과 올림 (Floor and Ceil)

```JavaScript
console.log(Math.floor(2.7)); // 2

console.log(Math.ceil(2.3)); // 3
```



### 난수 (Random)

* 0 이상 1미만의 값이 랜덤으로 return

```JavaScript
console.log(Math.random());
```



## 04. 컴퓨터의 계산 오류

### 소수계산

```JavaScript
let sum = 0.1 + 0.2;
console.log(sum);
// 0.30000000000000004 출력
```

* 컴퓨터가 10진수의 소수 표현을 2진수로 바꿀 때 무한 소수가 되는 경우가 발생
* 이것을 JavaScript가 숫자를 표현할 수 있는 범위 내에서 반올림을 한다.
* **오차 발생**



### 해결 방법

* **toFixed()** 메소드를 사용한다.

```JavaScript
let sum = 0.1 + 0.2;
console.log(+sum.toFixed(1)); // 0.3
```

* **round()** 메소드를 사용한다.

```JavaScript
let sum = 0.1 + 0.2;
console.log(Math.round(sum * 10) / 10); // 0.3
```



## 05. 문자열 심화

* 문자열 또한 객체처럼 다룰 수 있다.



### length 프로퍼티

* 문자열의 길이를 return



### 요소 접근

* 대괄호 표기법

> **string[index];**

* **charAt 메소드**

> **string.charAt(index);**



### 요소 탐색

* **indexOf 메소드**
* **lastIndexOf 메소드**



### 대소문자 변환

* **toUpperCase 메소드 : 대문자 변환**
* **toLowerCase 메소드 : 소문자 변환**



### 양 끝 공백 제거

* **trim 메소드**



### 부분 문자열 접근

* 두개의 parameter
  * 두 번째를 생략시, start 이후의 문자열을 가져온다.
  * 모두다 생략시, 문자열 전체를 가져온다.

> string.slice(start, end);



## 06. 문자열과 배열

### 비슷한 점

* length 프로퍼티를 가진다.
* 대괄호 표기법으로 각 요소 접근
* 배열과 문자열 모두에 사용되는 메소드
* **for ... of 문**



### 다른 점

* 자료형
* **배열은 mutable**
  * 요소를 수정할 수 있다.
* **문자열을 immutable**
  * 한 번 할당된 값을 수정할 수 없다.



## 07. 기본형과 참조형

* **기본형 (Primitie Type)** 
  * Number, String, Boolean, null, Undefined
  * 변수에 값을 할당
* **참조형 (Reference Type)**
  * Object, Array
  * **변수에 프로퍼티의 주소값이 할당**
  * **프로퍼티는 별도의 공간에 만들어진다.**



### 참조형 예시

```JavaScript
let x = {name: 'greedysiru'};
let y = x;

console.log(x);
console.log(y);
y.birth = 2020;
console.log(x);
console.log(y);
```

* 변수 x는 객체의 주소값이 할당되어있다.
* 변수 y에 변수 x가 가지고 있는 객체의 주소값이 할당된다.
* y에 새로운 프로퍼티를 넣으면, y가 가지고 있는 주소값의 객체에 프로퍼티가 추가된다.
* x 또한 해당 객체의 주소를 가지고 있으므로 x를 호출해도 프로퍼티가 추가된 객체가 나오게 된다.



## 08. 참조형 복사하기

### 배열

* **slice 메소드 활용**
  * parameter로 아무것도 넣지 않으면 배열을 복사하는 효과

```JavaScript
let number1 = [1, 2, 3];
let number2 = number1.slice();

number2.push(4);

console.log(number1); // [1, 2, 3]
console.log(number2); // [1, 2, 3, 4]
```



### 객체

* **Object.assign() 메소드 활용**

```JavaScript
let course1 = {
  title: 'JS 프로그래밍 기초',
  language: 'JavaScript'
};

let course2 = Object.assign({}, course1);

course2.title = '알고리즘의 정석';

console.log(course1);
console.log(course2);
```



### for ... in 문으로 복사하기

```JavaScript
function cloneObject(object){
  let temp = {};
  
  for (let key in object) {
    temp[key] = object[key];
  }
  
  return temp;
}

let course1 = {
  title: 'JS 프로그래밍 기초',
  language: 'JavaScript'
};

let course2 = cloneObject(course1);

course2.title = '알고리즘의 정석';

console.log(course1);
console.log(course2);
```

* 단, 객체나 배열 안에 중첩해서 객체나 배열이 있으면 그것들도 참조형이므로 주의



## 09. const, 변수와 상수

### const

* 스타일 가이드에서 변수 선언에 사용할 것을 권장
* 재할당이 불가능
* 코드가 동작하는 순간에는 상수로 사용되는 경우가 많다.
* 코드를 일관되게, 안전하게 작성하고자하는 취지
* 참조형인 경우, 상수는 데이터의 주소값을 가지는 것이므로 참조형 데이터 자체는 변경이 가능하다.



### 작명법

* 변수
  * 소문자로 시작
  * 두 번째 단어부터 첫 글자를 대문자로
* 상수
  * 대문자로 사용
  * 띄어쓰기는 밑줄(_)로 구분



## 10. var

* 예전의 JavaScript 변수 선언 키워드
* **let, const와 달리 중복선언이 가능**
* 복잡한 코드를 작성할 때 실수의 가능성이 커지고 치명적인 오류 발생
* **함수 스코프**
  * **함수를 기준으로만 적용**
  * **let, const는 블록 스코프**
* **끌어올림 (Hoisting)**
  * **변수의 선언문을 끌어올리는 현상**
  * **선언되기 이전에 변수에 접근이 가능**
  * let, const는 불가능
  * **함수 선언도 호이스팅이 적용**



# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)