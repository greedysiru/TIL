# [프로그래머스] Hello, JavaScript: 자바스크립트 입문 (1) (2021.1.28)



**상세 내용 [블로그](https://greedysiru.tistory.com/146) 참고**



# Part 1. 시작하기

## 1. 실습환경 만들기

* 사용 에디터 : sublimetext
* 브라우저 : chrome

### JavaScript

* HTML, CSS와 함께 client side 웹 프로그램을 작성할 수 있다.
* 별도의 개발환경이 필요 없다.
* 웹 브라우저에서 실행할 수 있다.
* 기존 언어들보다 상대적으로 문법이 쉽다.
* 웹에 interactive한 기능을 줄 수 있다.



### alert

* 특정 메시지를 브라우저 경고창에 출력한다.

>alert("출력할 문구");



### HTML과 연결하기

```HTML
<html>
	<head>
		<meta charset="utf-8">
		<script src="lecture01.js"></script>
	</head>
	<body>
		this is basic HTML page
	</body>
</html>
```

* **head 태그**에 **script태그**로 연결



## 2. Developer Console 사용하기

* **Developer Console(개발자 도구)**
  * 브라우저에서 제공하는 개발들을 위한 도구
  * HTML, CSS, JavaScript의 소스코드를 볼 수 있다.
  * console탭을 사용할 수 있다.
  * console에서 직접 명령어를 실행 하여 바로 확인할 수 있다.



### console.log 명령어

* 괄호 안의 메시지를 console에 출력
* 괄호 안에 여러개의 메시지를 콤마(,)로 구분하여 활용할 수 있다.

>console.log("출력할 문구");
>
>console.log("시루", "님 안녕하세요.")



### JavaScript 프로그램 실행순서

* 위에서 아래로 **순차적으로** 실행된다.



# Part2.  변수

## 1. 변수 선언과 초기화

### 변수

* 임의의 값을 저장하여 읽을 수 있는 공간
* **선언**: 변수를 사용할 것이라고 알려주는 것
* **초기화**: 선언한 변수에 처음으로 값을 지정하는 것

> var 변수;
>
> 변수 = value;
>
> var 변수1, 변수2;
>
> var 변수1 = 1, 변수2 = 2, 변수3 = 3;



## 2. 변수의 활용

* 변수의 이름을 사용하면, 변수에 저장된 값을 사용할 수 있다.

```JavaScript
var var 1 = "1", var2 = "2", var3 = "3";

console.log(var1);
alert(var2);
prompt(var3);
```



### prompt() 명령어

* 지정한 메시지를 사용자에게 보여주고 문자열을 입력받는다.
* 사용자가 입력한 값을 변수에 저장할 수 있다.

> var name = prompt("이름을 입력하세요.");



# Part3. 자료형

## 1. 기본 자료형

### 자료형

* 변수에 저장할 수 있는 값의 종류
  * **number Type**: 숫자
  * **string Type**: 문자열
  * **boolean Type**: 참 / 거짓



### typeof() 명령어

* 괄호 안의 변수의 자료형을 알려준다.

```JavaScript
var a = 100, b = 3.14;
var c ="안녕하세요", d = "a";
var e = true, f = false;

console.log(a, typeof(a)); // 100, "number"
console.log(c, typeof(c)); // 안녕하세요 string
console.log(e, typeof(e)); // true "boolean"
```



## 2. Number

* 숫자 자료형
* 64bit로 실수와 정수 모두 표현
* 지수표기법도 사용 가능하다.

> var a = 100;
>
> var b = 3.14;
>
> var c = 1e-3;

* NaN : Not-A-Number
* Infinity: 1/0과 같은 경우



### parseInt, parseFloat 명령어

* **prompt**처럼 데이터를 입력받는 경우, 숫자를 입력받아도 문자열로 인식된다.
* **parseInt, parseFloat**는 괄호 안에 있는 **문자열의 앞에서부터 Number를 인식**한다.
  * 앞이 문자로 시작하는 경우, 인식하지 못한다.
* parsInt는 정수, parseFloat는 실수

```JavaScript
var height = prompt("키를 입력해 주세요");
console.log( height, typeof(height)); // 180.7입니다. string

var height_int = parseInt(height);
console.log(height_int, typeof(height_int)); // 180 "number"

var height_float = parseFloat(height);
console.log(height_float, typeof(height_float)); // 180.7 "number"
```



## 3. String

* 따옴표('), 큰따옴표(")로 감싸서 문자열 표현
  * 따옴표, 큰따옴표는 짝을 맞춰서 사용해야한다.
  * 따옴표 안의 문자열에서는 큰 따옴표를 사용할 수 있고 큰 따옴표 문자열 안에서는 따옴표를 사용할 수 있다.
* escape character를 활용하면 문자열 안에서 따옴표와 큰따옴표를 사용할 수 있다.
  * 역슬래시(\\)를 사용한다.
  * 역슬래시를 두번 쓰면 역슬래시 자체를 사용할 수 있다.
* 줄바꿈 : \n



## 4. Object

* 단순 자료형보다 더 복잡한 자료를 표현할 수 있다.



### 객체 생성

* 중괄호{}로 정의
* **객체는 속성(property)의 집합**
  * 각 속성은 이름과 값(value)로 이루어진다.
  * 속성이름: 값 의 형태로 속성 정의
  * 속성은 모든 자료형이 가능하다
  * 객체 안에 객체가 들어올 수도 있다.

> var obj = { name: value };



### 객체 속성 접근

* 객체 이름 뒤에 점(.)을 사용하여 속성 이름에 접근
* 객체 이름 뒤에 대괄호([])안에 속성 이름을 문자열로 접근
* 변수에 접근하여 변경하는 것처럼 객체의 속성도 변경할 수 있다.

```JavaScript
var man = {name: "greedysiru", age: 20, height: 180};
man.name;   // "greedy siru"
man["age"]; // 20
man.height = 181; // 객체의 속성 변경
```



## 5. undefined와 null

### undefined

* 어떤 **변수나 객체의 속성이 정의되지 않을 때** 나타난다.
  * 선언만 한 상태의 변수의 타입이나 값
  * 객체의 정의되지 않은 속성의 타입이나 값



### null

* 개발자가 명시적으로 아무것도 없는 비**어있는 상태를 나타낼 때 사용**
  * typeof의 결과는 object이며 값은 null



# Part4. 연산자와 함수

## 1. 산술연산자

* Arithematic operator



### 이항연산자(binary operator)

* 두 개의 피연산자(A, B)를 가지는 연산자.
* 피연산자는 변수나 숫자가 될 수 있다.
* \+ 더하기
* \- 빼기
* \* 곱하기
* / 나누기
* % 나머지



### 단항연산자(unary operator)

* 하나의 피연산자를 가지는 연산자
* -A : 변수 A에 -1을 곱한다.
* 증감 연산자 (++, --) : 표현식 안에서 **변수**의 값을 증가하거나 감소시킬 수 있다.
  * 연산자를 변수의 앞에 또는 뒤에 적용한 것에 따라서 차이가 있다.

```JavaScript
var a;

a = 1;
console.log(++a); // 2
conosle.log(a);  // 2

a = 1;
console.log(a++); // 1
console.log(a);   // 2
```



### Math 관련 명령어

* **Math.pow(A, b)**:A의 B승을 구한다.
* **Math.sqrt(A)**: A의 제곱근을 구한다.
* **Math.random()**: 0~1 사이의 난수를 생성



## 2. 함수

### 함수의 정의

* 호출에 의해 여러번 실행될 수 있는 코드 블럭
* 반복되는 코드 감소
* 코드의 개발 및 수정 용이

> function 함수이름 (파라미터1, 파라미터2){
>
> 실행할 코드
>
> return 반환값;
>
> }

* 파라미터 : 함수의 정의 부분에 있는 변수
  * 여러개의 경우 콤마(,)로 구분
  * 파라미터가 없어도 된다.
  * 함수안에서 **변수**로 사용
* return 구문: 함수의 출력으로 보낼 값
  * return을 만나면 함수는 **즉시 종료된다.**
  * 함수를 호출한 표현식은 **반환값**으로 대치



### 함수의 호출

> 함수명(인자, ...)



## 3. 관계연산자와 논리연산자

### 관계연산자

* Relational operator
* 두 표현식(A, B)의 관계를 비교하는 이항연산자.
* boolean타입의 true, false로 출력

| > , <       | 클 때, 작을 때                   |
| ----------- | -------------------------------- |
| **>= , <=** | **같거나 클 때, 작거나 같을 때** |
| **==**      | **같을 때**                      |
| **!=**      | **같지 않을 때**                 |



### 논리연산자

* Logical operator
* 두 boolean 피 연산자에 대해 연산하는 연산자

| AND(&&)      | 두 피연산자가 모두 true일 때 true                    |
| ------------ | ---------------------------------------------------- |
| **OR(\|\|)** | **두 피연산자 중 하나라도 true일 때 true**           |
| **NOT(!)**   | **피 연산자의 boolean을 반대로 변환하는 단항연산자** |



## 4. 연산자 우선순위

1. **++, --**
2. **!**
3. ***, /, %**
4. **+, -**
5. **<, <=, >, >=**
6. **==, !=**
7. **&&**
8. **||**



### 괄호

* 우선순위 명시
* 코드의 가독성
* 연산자 우선순위 실수 방지



# Part5. String

 ## 1. String 이어 붙이기

### .length

* 문자열의 길이를 알아낸다.

> str.length



### .concat

* 문자열을 붙일 수 있다.

> str1.concat(str2)

* 더하기(+) 연산자로도 가능하다.

> str1 + str2



### 예시

```JavaScript
var str = "Hello";
var str2 = " World";

str.length; // 5
str["length"]; // 5

str.concat(str2); // "Hello World"

var str3 = str.concat(str2); // str3에 "Hello World" 저장

str.concat(str2).concat("!"); // "Hello World!"
"Hello".conat(" World").concat("!"); // "Hello World!"

"Hello".length // 5

str + str2; // "Hello World"

"Pi is" + 3.14 // "Pi is 3.14"

3.14 + "is Pi" // "3.14 is Pi"
```



## 2. String 다루기

### 특정 위치의 문자열 알아내기

* **.charAt**
  * 첫 문자 : **str.charAt(0)**
  * 마지막 문자 : **str.charAt(str.length-1)**
* **대괄호([])**
  * 첫 문자 : **str[0]**
  * 마지막 문자 :  **str[str.length-1]**



### 부분문자열 구하기

* **.substring(a, b)**: a에서 b까지의 부분 문자열 반환
  * b 생략시 a부터 마지막까지 문자열 반환
* **.substr(a, length):**a에서 길이만큼의 부분 문자열 반환
  * length 생략시, a에서 마지막까지의 문자열 반환
  * a가 음수인 경우, str.length - a로 동작



### 문자열 검색하기

* **indexOf(str):** str이 처음으로 나오는 index 반환
* **lastindexOf(str)**: str이 마지막으로 나오는 index 반환



# Reference

https://programmers.co.kr/learn/courses/3