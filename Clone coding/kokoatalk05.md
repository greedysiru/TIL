# [노마드코더]코코아톡 클론코딩 (5)(2021.1.7)



**상세 내용 [블로그](https://greedysiru.tistory.com/100) 참고**



# Cloning time

## 1. Introduction

* 카카오톡을 HTML과 CSS만으로 구현
* 백엔드는 적용하지 않는다.



## 2. index.html

* 기본적으로, 대부분의 웹 서버는 index.html을 먼저 읽어 낸다.



### 기본 구성

* VSC 환경에서, !를 입력하면 HTML 기본 서식을 바로 입력
* 클래스 명을 지을 때, 일반적인 이름보다는 다른 요소들과 구분을 짓기 위해서 아래처럼 특징적인 이름을 짓는다.

```HTML
<div class="status-bar">
  <div class="status-bar__column">
  </div>
</div>
```

* **BEM(Blcok Element Modifier)**
  * 클래스 속성만 사용한다.
  * Element : .block__element
  * Modifier : .block block--color--red



### 아이콘 삽입

* svg 형식으로 아이콘을 추가

  * 좌표로 되어있고 늘이고 줄이기가 자유롭다.

  * heroicons, Font Awesome 


```html
<body>
    <div class="status-bar">
        <div class="status-bar__column">
            <span>No Service</span>
            <i class="fas fa-wifi"></i>
            <!-- Wifi Icon -->
        </div>
        <div class="status-bar__column">
            <span>12:00</span>
        </div>
        <div class="status-bar__column">
            <span>100%</span>
            <i class="fas fa-battery-full"></i>
            <!-- Battery Icon -->
        </div>
    </div>
    <script src="https://kit.fontawesome.com/7ae4be9b50.js" crossorigin="anonymous"></script>
    <!-- fontawesome 스크립트 -->    
</body>
```



### 폼 만들기

* 배운 HTML을 토대로 회원가입 폼 만들기

```html
    <form id= "login-form">
        <input type="text" placeholder="Email or phone number" />
        <input type="password" placeholder="Password" />
        <input type="submit" value="Log In" />
        <input type="submit" value="Sign Up" />
        <a href="#">Find kokoa Account or Password</a>
    </form>
```

* fom에 id를 지정



### 상태바 CSS



#### body font 설정하기

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
```

* font-family 을 추가
* Google Fonts에서 다양한 폰트를 가져올 수 있다.
  * 원하는 폰트를 선택한다.
  *  폰트의 **url을 복사**해서 CSS 파일 상단에  **@import** 해준다.
  * **font-family를 복사**해서 적용할 곳에 **붙여넣기** 한다.
  * 

#### CSS hack

* 적용 순서
  * 상위 박스 : 
    * **justify-content: center;**
  * 내부 박스 : 
    * **width: 33%;**
  * 중앙에 위치할 박스 : 
    * **display: felx; justify-content: center;**
  * 오른쪽에 위치할 박스 :
    * **display: flex; justify-content: flex-end; align-items: center;**



### Reset CSS

* 브라우저에서 제공하는  body의 기본 margin 설정을 없앤다.
* 검색 후 파일을 복사한 뒤 **@import** 한다.
* 전체 웹 페이지의 기본 설정 CSS파일로 지정
* input의 border를 전부 지워 줄 것이므로 마지막에 아래의 코드를 추가

```CSS
input:focus {
  outline: none;
}
```





### Header CSS

* index.html 의 **header태그를 설정**

```CSS
.welcome-header {
  margin: 90px 0px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.welcome-header__title {
  margin-bottom: 20px;
  font-size: 25px;
}

.welcome-header__text {
  width: 60%;
  opacity: 0.7;
}
```

* 지정한 클래스 명을 사용해서 세부 사항들을 설정한다.
  * Chrome의 확장 프로그램 **page ruler redox**를 사용해서 샘플 이미지의 치수를 측정
* **.welcom-header__text**의 폰트 색상이 회색일 때, **opacity**를 설정하는 방법도 있다.
* **.welcom-header** 의 자식 요소가 세로로 있어야 하므로 **flex-direction: column**을 설정한다.
* **text-align : center** : 텍스트 태그들을 가운데 정렬한다.



### Login form CSS

* index.html의 **Login form을 설정**

```CSS
#login-form {
  display: flex;
  flex-direction: column;
  margin: 0px 30px;
}

#login-form input {
  border: none;
  padding: 15px 0px;
  font-size: 18px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  margin-bottom: 25px;
  transition: border-color 0.3s ease-in-out;
}

#login-form input::placeholder {
  color: rgba(0, 0, 0, 0.4);
}

#login-form input:focus {
  border-color: var(--yellow);
}
```

* 로그인 폼은 요소들이 위 아래로 나란히 있으므로 **login-form**에  **flex-direction : colomn**을 설정한다.
* margin, padding 값들을 설정한다.
* font-size, color를 설정한다.
  * 색상은 Chrome의 확장 프로그램 **colorzilla**를 사용하여 추출한다.
* **login-form input::placeholder**로 **placeholder**의 색상 지정
* form이 **focus** 되었을 때 **색상 변화**와 **transition** 설정
  * 색상 변수를 선언하기 위해, 별도의 변수 파일을 생성한다.

```CSS
:root {
  --yellow: #fae100;
}
```

* **@import** 후, **#login-form input:focus**에 **var(--yellow)**변수 선언한 색상을 적용
* 부모 요소인 **#login-form input**에 **transition** 설정



#### not

* 적용하고 싶지 않은 요소를 not으로 제외할 수 있다.

```CSS
#login-form input:not([type="submit"]) {
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  transition: border-color 0.3s ease-in-out;
}
```

* **type="submit"**은 아래의 속성을 적용하지 않게 된다.



#### Submit CSS

```CSS
#login-form input[type="submit"] {
  background-color: var(--yellow);
  cursor: pointer;
  padding: 20px 0px;
  border-radius: 5px;
}

#login-form a {
  text-align: center;
  text-decoration: none;
  color: inherit;
  font-size: 13px;
}
```

* **cursor: pointer**는 커서를 **submit 버튼**에 올렸을 때 모양을 설정한다.
* **color: inherit**은 부모 요소로부터 속성을 상속받는다는 듯이다.



### CSS 코드 정리하기

* index.html의 CSS코드를 별도의 파일로 분리한다.
  * **status-bar.css**는 **components 폴더**에 정리
  * **login.css**는 **screens 폴더**에 정리
* **styles.css**에는 **전 페이지 공통으로 가지는 설정**을 한다.
  * 전체 페이지의 배경 색, 기본 폰트 등등



### Form action, method

* action은 어떤 페이지로 data를 보낼 것인지 지정한다.

```html
 <form  action="friends.html" method="get" id= "login-form">
```

* 다음에 만들 페이지인 **friends.html**과 연결되었다.
* method는 2가지 방식 중 하나를 사용한다.
  * post : 백엔드 서버에 정보를 전송한다. 이 프로젝트에서는 할 수 없다.
  * get : 보안에 취약하다. URL에 포함되어도 상관없는 정보들을 이 방식으로 전송



# Reference

https://nomadcoders.co/kokoa-clone/lobby



