# [노마드코더]바닐라 JS로 크롬 앱 만들기 (1)(2021.1.11 ~ 12)



**상세 내용 [블로그](https://greedysiru.tistory.com/112) 참고**



# Introduction

* 바닐라 JavaScript로 여러 앱을 클론코딩 한다.
* 모든 언어의 공통적인 concept를 배운다.
  * 변수, 함수, 조건문 등등



# Theory

## 1. Why JS?

* 웹에 사용되는 하나뿐인 프로그래밍 언어
* Fornt-end 분야에서 사용한다.
* Interactive 한 웹 사이트를 만들 수 있다.



## 2. Super Powers of JS

* Interactive한 모든 것에 사용될 수 있다.
  * game
  * app
  * web site



## 3. JavaScript version

* ECMAScript : **specification of JavaScript**
* ES5, ES6 : version of specification
* specification이란, 웹 페이지를 어떻게 구현하라는 안내책자이다.
* 웹 브라우저는 각각의 방식으로 specification을 구현
* **Vanilla JavaScrip**t : 어떠한 libraries도 없는 순수한 JavaScript



## 4. VanillaJS

* 여러 library나 framwork를 다루기 전에, **VanillaJS를 아는 것이 중요**하다.
  * 결국에는 VanillaJS로 귀결되기 때문이다.
  * 기본 지식이 있어야 library와 framwork를 배우기도 쉽다.



## 5. Hello World with Javascript

### HTML에 JavaSciprt 연결하기

* **body 하단**에 **script 태그** 입력한다.

```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Something</title>
    <link rel="stylesheet" href="index.css">
  </head>
  <body>
    <h1>This works!</h1>
    <script src="index.js"></script>
  </body>
</html>
```



### alert

* 웹 사이트의 **경고창**을 만들 수 있다.

```javascript
alert('Im Working. Im JS. Im Beautiful. Im worth it')
```



### console.log

* **console에 문구를 출력**할 수 있다.

```javascript
console.log('Im Working. Im JS. Im Beautiful. Im worth it')
```



## 6. Variable

* 변경될 수 있는 것



### JavaScript 변수 문법

* 문법은 **한 줄**에 **하나씩** 쓴다.
* 문법이 끝나면 **;(세미콜론)**으로 마친다.
* 변수 선언시, **let**을 넣는다.
* **선언 -> 초기화 -> 사용** 
  * 선언과 초기화는 동시에 가능하다.
* 사용 예시

```JavaScript
let a = 221;
let b = a - 5;
console.log(b,a);
```



## 7. let, const, var

* 변수 선언의 세가지 방법
* **let**: 초기값을 변경 가능
* **const**: 상수. 초기값 변경 불가. 주로 사용
* var: 버그나 에러 발생의 주범이므로 사용하지 말 것



## 8. Data Types on JS

### String

* **문자열**을 의미한다.
* 선언시, **""** 사이에 써야 한다.
  * 숫자도 문자열로 선언할 수 있다.
* 사용 예시

```JavaScript
const what = "Jaemin";
```



### Boolean

* **True or False**
* 이진법 체계에서는 0과 1로 구분한다. **True는 1, False는 0**
* 사용 예시

```JavaScript
const wat = false;
```



### Number

```JavaScript
const wat = 777;
```



### Float

* Floating Number
* 사용 예시

```JavaScript
const wat = 55.1
```



## 9. Organizing Data with Arrays

### camel case 문법

* 변수명을 작성할 때, 처음 시작은 소문자로 쓴다.
* 공백 대신에 단어 첫글자를 대문자로 쓴다.
* 변수에는 ./ 같은 특수문자가 들어갈 수 없다.
* 사용 예시

```JavaScript
const daysOfWeek = "a"
```



### Array

* **여러 데이터를 하나로 묶을 수 있다.**
* **[]부호**로 감싼다.
* String, Boolean, Number, Float, 변수 등 **여러 데이터형**을 넣을 수 있다.
* **index는 0부터** 시작한다.
* 사용 예시

```JavaScript
const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "sat", "sun", true, false, 1993, 180.7];
console.log(daysOfWeek);
console.log(daysOfWeek[0]); //첫 번째 값인 Mon 출력
```



## 10. Organizing Data with Objects

* 여러 데이터를 **label을 지정하여 저장**할 수 있다.
* **{}부호**로 감싼다.
* 데이터 사이에 **,**를 쓴다.
* **Object 안의 값**은 수정할 수 있다.
* **Array와 Object는 서로 포함**할 수 있다.
* 사용 예시

```JavaScript
const siruInfo = {
  name:"Siru",
  age:4,
  gender:"female",
  isUgly:true,
  favFood: [ "churu", "snack", "fish"],
  favToy: [
    {
      name:"bongbong",
      funny: "good"
    },
    {
      name:"scratch",
      funny:"well"
    }
  ]
}

console.log(siruInfo);          //siruInfo의 전체 출력

console.log(siruInfo.gender);   //siruInfo의 gender 출력

siruInfo.gender = "male"        //siruInfo의 gedner 값 변경

console.log(siruInfo.favToy)    //siruInfo에서 object를 포함한 배열 favToy 호출

console.log(siruInfo.favToy[0].name) //siruInfo에서 favToy의 첫 번째 배열의 name에 해당하는 값 호출
```



# Reference

https://nomadcoders.co/javascript-for-beginners/lobby