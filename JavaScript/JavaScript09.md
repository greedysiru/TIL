# [노마드코더]바닐라 JS로 크롬 앱 만들기 (3)(2021.1.15 ~ 16)



**상세 내용 [블로그](https://greedysiru.tistory.com/119) 참고**



# Making My First JS APP

## 1. Making a JS Clock part One

* 현재 시간을 출력하는 코드를 작성한다.



### 시간과 관련된 코드

* **new Date( ) :**  날짜와 관련된 **객체**
  * **date**에 선언한 결과, **해당 국가의 표준시**가 입력
* **date.getDay( ) :**  요일의 수. 월요일부터 카운트해서 금요일인 5가 나왔다.
* **date.getDate( ) :** 몇 일인지 입력
* **date.getHours( ) :** 현재 시간
* **date.getMinutes( ) :** 현재 분



## 시간 출력 웹 페이지 만들기

* 페이지를 연 순간을 기점으로 시간을 출력하는 웹 페이지를 만들어 본다.
* 위 함수들을 사용

#### HTML

```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Something</title>
    <link rel="stylesheet" href="index.css">
  </head>
  <body>
    <div class="js-clock"> <!-- 클래스 선언 -->
      <h1>
        00:00 <!-- 시간 -->
      </h1>
    </div>

    <script src="clock.js"></script> <!-- clock.js와 링크 -->
  </body>
</html>
```



### JavaScript

```javascript
const clockContainer = document.querySelector(".js-clock"), // js-clock 클래스 가져오기
  clockTitle = clockContainer.querySelector("h1"); // h1에서 시간 부분 가져오기
function getTime(){
    const date =new Date(); // 객체를 date 변수로 선언
    const minutes = date.getMinutes(); // minuts에 현재 시간 분 입력
    const hours = date.getHours(); // 시간 입력
    const seconds = date.getSeconds(); // 초 입력
    clockTitle.innerText = `${hours}:${minutes}:${seconds}`; // 시:분:초 출력하기
}
function init(){
    getTime();   // 함수 실행
}
init();
```





## 2. Making a JS Clock part Two

### setInterval( )

* 위의 시계 웹 페이지는 새로고침을 해야 시간이 갱신된다.
* 아래 함수로 초 단위로 갱신할 수 있다.

> setInterval( **실행할 함수**, **실행할 시간 간격)**

* 실행할 시간 간격은 **밀리 초 단위**



### 삼항연산자

* if를 쓰지 않고 한 괄호 내에서 간단한 조건문을 작성할 수 있다.
  1. 비교 연산자를 쓴다. (조건)
  2. ?를 쓴다
  3. 백틱 사이에 참일 경우 출력할 것을 쓴다.
  4. 이어서 : 뒤에 거짓일 때 출력할 것을 쓴다.



### 웹 페이지 적용하기

* 웹 페이지에 위의 두 가지를 추가하여 실시간으로 시간이 갱신되고 10 미만의 숫자일때 빈자리에 0을 출력

```javascript
const clockContainer = document.querySelector(".js-clock"),
  clockTitle = clockContainer.querySelector("h1");
function getTime(){
    const date =new Date();
    const minutes = date.getMinutes();
    const hours = date.getHours();
    const seconds = date.getSeconds();
    clockTitle.innerText = `${hours < 10 ? `0${hours}` : hours}:${minutes < 10 ? `0${minutes}` : minutes}:${seconds < 10 ? `0${seconds}` : seconds}`; // 삼항 연산자로 10 이하일때 앞에 0 붙이기
}
function init(){
    getTime();
    setInterval(getTime, 1000); // 1초마다 시간 갱신
}
init();
```



## 3. Saving the User Name part One

### Qury selector의 종류

* **querySelector :** 찾은 첫번째 것을 가져온다.
* **querySelectorAll :** 찾은 모든 것들을 가져온다. 클래스 명에 다른 엘리먼트들을 가져와서 array로 만든다.
* **getElemenyById :** 해당 id를 가진 요소를 가져온다.



### Local storage

* Local storage는 작은 정보를 유저 컴퓨터에 저장하는 방법이다.

  >localStorage.setItem("key" , value);
  >
  >localStorage.getItem("key");

* **첫번 째 인자**에는 **key**가 **두번 째 인자**에는 **value**가 들어간다.

* **저장된 key**값을 **getItem**의 인자로 입력하면, **value** 가 나온다.

* **없는 key를 입력**하면, 존재하지 않는다는 의미인 **null이 출력**된다.

* value를 변경할 수도 있다.



### 웹 페이지 적용

* **사용자 이름을 받는 form**을 만들고 위의 기능을 추가
* Local storage를 토대로 맞는 key값이면 환영 문구를 출력
* 이 단계에선, 사용자 명은 검사하지 않고 환영 문구를 출력하는 것만 추가한다.



#### HTML

```HTML
    <form class="js-form form"> <!-- js-form과 form 클래스 선언 -->
        <input type="text" placeholder="What is you name?" /> <!--사용자 이름 입력 받기-->
    </form>
    <h4 class="js-greetings greetings"></h4> <!-- 클래스 선언 -->
    <script src="greeting.js"></script> <!-- js 링크 -->
```



#### CSS

```CSS
.form {
  display: none; /* form 숨기기 */
}
.showing {
  display: block; /* block으로 인해 다시 form은 보여짐(기본 설정) */
}
```



#### JavaScirpt

```JavaScript
const form = document.querySelector(".js-form"),       // form 가져오기
      input = form.querySelector("input"),            // input 가져오기
      greeting = document.querySelector(".js-greetings"); // h4 가져오기

const USER_LS = "currentUser",
      SHOWING_CN = "showing";
function paintGreeting(text){
  form.classList.remove(SHOWING_CN);        // 폼의 showing 클래스 삭제 즉, 안보이게 된다.
  greeting.classList.add(SHOWING_CN);       // h4의 showing 클래스 추가
  greeting.innerText = `Hello ${text}`;    // h4에 문구가 추가되어 화면에 나오게 된다.
}


function loadName(){                         // local storage와 같은 이름인지 확인
  const currentUser = localStorage.getItem(USER_LS);
  if(currentUser == null){                    // 일치하지 않을 경우

  }else {
    paintGreeting(currentUser);              // 폼 가리기 함수 실행
  }
}


function init(){
  loadName();
}

init();
```



## 4. Saving the User Name part Two

* 사용자에게 이름을 받아, **Local storage에 저장하는 기능을 추가**한다.



### prevetDefault

* **input**에서 , 데이터를 입력하고 **submit**을 하면 **default** 설정에 의해 그 데이터를 어딘가에 보낸다.
* 그 과정에서, document도 보내기 때문에 웹페이지가 새로고침한 것처럼 동작한다.
* **prevetDefault 메소드**는  이러한 동작을 막을 수 있다.



### 웹 페이지 적용하기(JavaScript 코드 추가)

```javascript
...

function saveName(text){
    localStorage.setItem(USER_LS, text); // local storage에 USER_LS(currentUSer) 저장
}

function hadleSubmit(event){
    event.preventDefault(); // document를 보내는 event를 막는다.
    const currentValue = input.value; // input에서 입력된 value를 받는다.
    paintGreeting(currentValue); // value를 받고 form을 지우고 문구에 value를 더해 출력한다.
    saveName(currentValue); // value Local storage 저장
}

function askForName(){                                      // currentUser가 null이면 이름 물어보는 함수
    form.classList.add(SHOWING_CN);                        // form을 보여주게 하기
    form.addEventListener("submit", hadleSubmit)           // submit하면 hadleSubmit 함수 처리
}

...


function loadName(){
    const currentUser = localStorage.getItem(USER_LS)         // local storage의 vlaue와 input한 이름 비교하기
    if(currentUser == null){
        askForName();                      
    }else {
        paintGreeting(currentUser);
    }
}

...
```



# Reference

https://nomadcoders.co/javascript-for-beginners/lobby