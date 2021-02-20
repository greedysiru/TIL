# [코드잇] 인터랙티브 자바스크립트 (1) (2021.2.20)



**상세 내용 [블로그](https://greedysiru.tistory.com/217) 참고**



# 인터랙티브 자바스크립트 시작하기

## 01. 웹 서비스와 JavaScript

* 웹 서비스의 중심에서 다양한 분야에서 사용되는 프로그래밍 언어
* 웹 페이지의 여러요소들을 자유롭게 다루기 위해 등장
* HTML로 구조 -> CSS로 꾸미기 -> JavaScript로 동작하기
* **사용자의 입력값을 받아 정보를 처리**



## 02. HTML/CSS + JavaScript

* HTML/CSS는 처음의 모습에서 변화를 주기 어렵다
* JavaScript를 이용하면, 실시간으로 HTML을 변화시키거나 스타일을 수정하는 것이 가능하다.



## 03. id로 태그 선택하기

> **document.getElementById('id');**

* document: 객체
* **getElementById(): 해당 id값(파라미터)을 가진 태그 선택하는 메소드**
* 해당 태그 내부의 모든 것을 가져온다.
* id 속성은 고유한 값이므로 **필요한 태그만을 명확하게 선택**할 수 있다.
* 존재하지 않은 것을 선택하면 -> null



## 04. class로 태그 선택하기

> **document.getElementsByClassName('class');**
>
> **elements임에 주의**

* **여러 요소를 동시에 선택할 수 있다.**
* **HTMLCollection**의 형태로 가져온다.
* 하나밖에 없는 클래스를 선택해도 HTMLCollection으로 가져온다.
* 위에서부터 아래의 순서대로 가져온다.
* 존재하지 않는 클래스값을 찾게되면 빈 HTMLCollection을 가져오게 된다.



### HTMLCollection

* **유사배열 (Array -Like Object)**
* 인덱스, length를 가진다.
* splice, push와 같은 배열 메소드 사용 불가
* 대괄호 표기법, for...of문으로 각 인덱스 접근 가능



## 05. 유사 배열 (Array-Like Object)

* **배열과 유사한 객체**
* 숫자 형태의 indexing이 가능하다.
* **length 프로퍼티가 있다.**
* 배열의 기본 메소드 사용 불가
* Array.isArray(유사배열)은 false
  * isArray(): 파라미터로 전달한 값이 배열인지 아닌지 평가하여 boolean 형태의 값으로 리턴



### 주의사항

* 유사배열은 다양한 형태로 존재
* for...of문을 활용할 수 없는 경우도 있음
* 배열 기본 메소드를 직접 구현에서 사용할 수 있다.



## 06. 태그이름으로 태그 선택하기

> **document.getElementsByTagName('태그이름')**

* **문서 내의 해당 태그이름인 모든 태그를 선택**
* **HTMLCollection**을 리턴
* 파라미터에 **'*'** 을 전달하면 모든 태그를 선택



## 07. CSS 선택자로 태그 선택하기

> **document.querySelector('css selector');**

* **문서 내의 해당 css 선택자를 가져온다.**
  * id인 경우 -> #
  * class인 경우 -> .
* 클래스의 경우, 가장 첫 번째 요소만을 선택한다.



### 모든 태그 선택하기

> **document.querySelectorAll('css selector');**

* **문서 내의 해당 css 선택자를 모두 가져온다.**
* **NodeList**의 형태로 가져온다.



## 08. 이벤트와 버튼 클릭

```HTML
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>JS with Codeit</title>
</head>
<body>
  <div>
    <button id="myBtn">Click!</button>
  </div>
  <script src="index.js"></script>
</body>
</html>
```



```JavaScript
// 이벤트(Event)와 버튼 클릭
const btn = document.querySelector('#myBtn');

// 이벤트 핸들링(Event Handling)
btn.onclick = function() { // 이벤트 핸들러(Event Handler)
	console.log('Hello siru!');
};
```

* **#myBtn** 을 btn에 할당
* btn의 **onclick 프로퍼티**에 함수를 정의
* 웹 페이지에서 버튼을 클릭하면, 콘솔창에 해당 문구 출력
* Event: 웹 페이지에서 발생하는 대부분의 일(사건)
  * 버튼 클릭, 스크롤, 키보드 입력...
* Evnet Handling: JavaScript를 통해 이벤트를 다루는 일
* Evnet Handler: 구체적인 동작들을 코드로 표현



### HTML 태그에 직접 이벤트 핸들링 작성하기

```HTML
  <div>
    <button id="myBtn" onclick="console.log('Hello siru!')">Click!</button>
  </div>
```

* onclick 속성에 JavaScript 코드를 넣을 수 있다.
* 코드의 일관성, 가독성에 좋지 않으니 지양



# Reference

[코드잇 - 인터랙티브 자바스크립트](https://www.codeit.kr/courses/javascript-intermediate/topics/interactive-javascript)