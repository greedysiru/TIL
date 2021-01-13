# [노마드코더]바닐라 JS로 크롬 앱 만들기 (2)(2021.1.13)



**상세 내용 [블로그](https://greedysiru.tistory.com/114) 참고**



# Practice

## 1. Your first JS Function

### 함수

* 어떤 것을 수행하는 한 부분



### 함수 선언

* 기본적인 내장함수 말고, 원하는 기능을 할 수 있도록 함수를 선언할 수 있다.

>function 함수명(인자){
>
>​    함수 선언
>
>}



### 함수 예시

```JavaScript
function sayHello(name, number){
   console.log('hello', name, "You are", number, "years old"); 
}
sayHello("Jaemin", 15); // hello Jaemin You are 15 years old 출력
```



## 2. More Function Fun

### backtick

```JavaScript
function sayHello(name, number){
   console.log(`Hello ${name} you are ${number} years old`); 
}
```



### return

* **return은 함수를 실행하고 그 값을 되돌려 준다.**



#### return이 없는 경우

```JavaScript
function sayHello(name, number){
   console.log(`Hello ${name} you are ${number} years old`); 
}

const greetJaemin = sayHello("Jaemin", 15) //sayHello 함수를 실행하고 아무것도 반환하지 않음
console.log(greetJaemin) //undefined
```



#### return을 사용한 경우

```JavaScript
function sayHello(name, number){
   return(`Hello ${name} you are ${number} years old`); 
}

const greetJaemin = sayHello("Jaemin", 15) //sayHello 함수의 리턴값 입력
console.log(greetJaemin) //sayHello 출력
```



### Object로 함수 정의하기

```JavaScript
const calculator = {
    plus: function(a, b){
        return a + b;
    },
    minus: function(a, b){
        return a - b;
    },
    multiple: function(a, b){
        return a * b;
    },
    divide: function(a, b){
        return a / b;
    },
    power: function(a, b){
        return a ** b;
    }
}

const plus = calculator.plus(5, 5);
const minus = calculator.minus(5, 5);
const multiple = calculator.multiple(5, 5);
const divide = calculator.divide(5, 5);
const power = calculator.power(5, 5);


console.log(plus);
console.log(minus);
console.log(multiple);
console.log(divide);
console.log(power);
```



## 3. JS DOM Functions

### DOM

* **Document Object Model**
* HTML 문서를 DOM 객체로 가져온다.
* HTML 문서에 class, ID 등으로 지정해놓은 요소를 가져와서 그것을 객체의 이름으로 할 수 있다.
* 사용 예시

```JavaScript
const title = document.getElementById("title");
title.innerHTML = "Hi! From JS";
```

* **documnet.getElementById** : HTML의 title id를 가진 요소를 가져온다.
* **tiltle.innerHTML** : 가져온 title을 해당 문구로 변경



## 4. Modifying the DOM with JS

### query selector

* HTML 지정한 해당 요소를 찾아와서 변수에 정의
* 사용 예시

```JavaScript
const title = document.querySelector("#title");
title.innerHTML = "Hi! From JS";
title.style.color = "tomato";
document.title = "I own you now";
```

* **document.querySelector** : id가 title인 element를 찾아서 변수 title에 입력
* **title.style.color** : 색상 스타일을 적용
* **document.title** : html문서의 title을 변경



## 5. Events and event handlers

* **JavaScript는 event에 반응할 수 있다.**
* **event**란 **웹사이트에서 발생하는 것**들이다.
  * clikc, resize, submit, input, change, load 등
* **HTML JavaScript DOM event MDN 검색**하여 더 많은 event 조회 가능



### addEventListener

>target.addEventListener(type, listener);

* **target의 event type을 감지해서 listener에게 전달**
* 사용 예시

```javascript
const title = document.querySelector("#title"); // html의 id가 title인 요소를 변수 title에 입력

function handleResize(){                        // 입력을 받으면 문구를 출력하는 함수 handleResize 선언
    console.log("I have been resized");
}

window.addEventListener("resize", handleResize); // window가 resize되면 handleResize 함수 실행

function handleClick() {                     // 입력을 받으면 title의 색상을 바꾸는 함수 handleClick 선언
    title.style.color = "tomato";
}

title.addEventListener("click", handleClick); // title이 click되면 handleClick 함수 실행
```



## 6. If, else, and, or

### 조건문 문법

> if(condition){
>     block
> } else {
>     block
> } 



### and, or 연산자

* **&&(and)** : 둘 다 참이어야 참
* **||(or)** : 둘 중 하나가 참이어도 참



### 조건문 사용 예시

```JavaScript
const age = prompt("How old are you");

if (age >= 18 && age <= 21){                  //age가 18이상이고 21이하일때 참
    console.log('you can drink but you should not');
} else if(age > 21){                          // age가 21 초과일 때 참
    console.log('go ahead');
} else{                                      // 위 두 조건이 거짓일 경우 아래 block 실행
    console.log('too young');
}
```

* **prompt** : 사용자에게 입력 창을 띄워줌



## 7. DOM - If else - Function practice



```JavaScript
const title = document.querySelector("#title"); //html의 id=title 요소를 가져온다.

const BASE_COLOR = "rgb(52, 73, 94)";          // 기본 색상 선언
const OTHER_COLOR = "#7f8c8d";                 // 다른 색상 선언

function handleClick() {
    const currentColor = title.style.color; 
    if (currentColor === BASE_COLOR){        // 현재 색상이 기본 색상과 같으면 참
        title.style.color = OTHER_COLOR;     // title 색상을 다른 색상으로 변경
    } else {                                 // 현재 색상이 기본 색상과 다르면
        title.style.color =BASE_COLOR;       // 기본 색상으로 변경
    }
}

function init(){                            // 초기화 함수
    title.style.color = BASE_COLOR;         // 기본 색상을 title에 입력
    title.addEventListener("click", handleClick);  // title 클릭 시 handleClick 실행
}
init();                                    // 초기화 함수 실행 시키기

function handleOffline() {                  // 인터넷 연결이 끊겼을 시 콘솔에 문구 출력 함수 선언
    console.log("Disconnected");
}

window.addEventListener("offline", handleOffline); // 인터넷 연결이 끊어지면 hadleOffline 실행

function handleOnline() {                         // 인터넷 연결이 되었을 시 콘솔에 문구 출력 함수 선언
    console.log("connected");
}

window.addEventListener("online", handleOnline);  // 인터넷 연결이 되면 handleOnline 실행

```



## 8. DOM - If else - Function practice Two



### HTML 코드

```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Something</title>
    <link rel="stylesheet" href="index.css">
  </head>
  <body>
    <h1 id="title" class="btn">This works!</h1> 
    <script src="index.js"></script>
  </body>
</html>
```



### CSS 코드

```CSS
body {
  background-color: #ecf0f1;
}
h1 {
  color: #34495e;
  transition: color 0.5s ease-in-out; /* 폰트 색상이 바뀌는 경우 서서히 변화하는 효과 */
}
.btn {
  cursor: pointer;                   /* 포인터 커서 효과 */
}
.clicked {                           /* 클릭 되었을 때 색상 변경 */
  color: #7f8c8d;
}
```



### JavaScript Code 1

```JavaScript
const title = document.querySelector("#title"); // id title 가져오기

const CLICKED_CLASS = "clicked"; // 클릭여부를 확인하기 위한 변수 선언

function handleClick() {         // 폰트 색상 변경 기능을 가진 함수 선언
 const currentClass = title.className; // 현재 title의 class 명을 가지는 변수 선언
 if(currentClass !== CLICKED_CLASS){   // 현재 클래스명이 clicked가 아니면 참
     title.className = CLICKED_CLASS;  // title의 클래스 명을 clicked로 바꾼다. 그 결과 폰트 색상 변경
 } else {                              // 현재 클래스명이 clicked일 경우 클래스 명을 지운다.
     title.className = "";             // 그 결과, 처음의 폰트 색상으로 돌아온다.
 }
}

function init() {                      //초기화 함수 선언
    title.addEventListener("click", handleClick);
}
init();
```

* 위의 코드는 정상적으로 폰트의 색상을 변경한다. 
* **그러나, class 를 변경하는 과정에서 css에서 선언한 cusor : pointer 가 지워져, 포인터 효과가 사라진다.**



### JavaScript Code 2

```javascript
const title = document.querySelector("#title");

const CLICKED_CLASS = "clicked";

function handleClick() {
 const hasClass = title.classList.contains(CLICKED_CLASS); // title에 clicked가 있는지 (참/거짓)
 if(!hasClass){                                        //clicked가 없을 경우
     title.classList.add(CLICKED_CLASS);              // title의 클래스에 clicked를 추가
 } else {
     title.classList.remove(CLICKED_CLASS) = "";     //clicked가 있으면 제거
 }
}

function init() {
    title.addEventListener("click", handleClick);
}
init();
```

* **title.classList** : 해당 요소의 클래스에 접근할 수 있는 메소드이다.
  * **contains** : 해당 문자열이 있는지 참/거짓으로 출력
  * **remove** : 해당 문자열을 제거



### JavaScript Code 3

* 위의 코드를 대체할 수 있는 간단한 함수를 사용

```javascript
const title = document.querySelector("#title");

const CLICKED_CLASS = "clicked";

function handleClick() {
  title.classList.toggle(CLICKED_CLASS); // clicked가 있으면 추가 없으면 제거
}

function init() {
    title.addEventListener("click", handleClick);
}
init();
```

* **title.classList.toggle** : 클래스가 있으면 추가 없으면 제거



# Reference

https://nomadcoders.co/javascript-for-beginners/lobby