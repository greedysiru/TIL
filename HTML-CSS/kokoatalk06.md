# [노마드코더]코코아톡 클론코딩 (6)(2021.1.7 ~ 8)



**상세 내용 [블로그](https://greedysiru.tistory.com/102) 참고**



# Cloning time

## friends.html

### Navigation bar

#### VSC 단축키

```html
nav>ul>li>*4>a
```

위 단축키를 입력하면, 아래의 html 코드가 생성

```html
<nav>
    <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
    </ul>
</nav>
```



#### html 코드 작성

* Navigation bar의 기본 html 코드를 작성

```html
    <nav class="nav">
        <ul class="nav__list">
            <li class="nav__btn">
                <a class="nav__link" href="friends.html"><i class="fas fa-user fa-lg"></i></a>
            </li>
            <li class="nav__btn">
                <a class="nav__link" href="#"><i class="far fa-comment fa-lg"></i></a>
            </li>
            <li class="nav__btn">
                <a class="nav__link" href="#"><i class="fas fa-search fa-lg"></i></a>
            </li>
            <li class="nav__btn">
                <a class="nav__link" href="#"><i class="fas fa-ellipsis-h fa-lg"></i></a>
            </li>
        </ul>
    </nav>
```



#### CSS 코드 작성

* **componetns 폴더** 아래에 **nav-bar.css를 생성**하고 CSS 코드를 입력
* **styles.css**에 꼭 **@import**  한다.

```CSS
.nav {
  background-color: #f9f9fa;
  padding: 20px 50px;
  border-top: 1px solid rgba(121, 121, 121, 0.3);
}

.nav__list {
  display: flex;
  justify-content: space-between;
}

.nav__link {
  color: #2e363e;
}
```



#### a 태그 reset

* reset.css에서 a태그를 초기화 한다.

```CSS
a {
  color: inherit;
  text-decoration: none;
}
```





#### status bar, navigation bar 고정 하기

* status bar

```CSS
.status-bar {
  position: fixed;
  top: 0;
  display: flex;
  justify-content: center;
  padding: 5px 3px;
  width: 100%;
}
```

* **position: fixed**와 **width: 100%, top: 0을 추가**한다.



* navigation bar

```CSS
.nav {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #f9f9fa;
  padding: 20px 50px;
  box-sizing: border-box;
  border-top: 1px solid rgba(121, 121, 121, 0.3);
}
```

* **position: fixed, bottom: 0, box-sizing: border-box**를 추가한다. 



#### Border Box

* CSS에 box에 **padding을 추가하면, 그 만큼 box의 크기를 늘린다.**
  * 200px의 box에 padding 50px을 추가하면, box크기는 총 250px이 된다.
* **box-sizing : border-box**를 입력하면, padding을 입력해도 **box사이즈를 유지**할 수 있다.



#### 대화 알림 버튼 만들기

* 카카오톡의 대화 알림 버튼을 구현한다.
* friends.html의 대화창 navigation 아이콘 부분에  **span태그를 추가**
  * class는 **nav__notification**으로 한다.

```html
<a class="nav__link" href="#">
  <span class="nav__notification">1</span>
  <i class="far fa-comment fa-2x"></i>
</a>
```



* **nav-bar.css**에서 **nav__notification**을 설정한다.

```CSS
.nav__link {
  color: #2e363e;
  position: relative;
}

.nav__notification {
  display: block;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: tomato;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  color: whitesmoke;
  font-weight: 600;
  position: absolute;
  left: 15px;
  bottom: 15px;
}
```

* **span태그**는 **inline**이므로 **display:block 속성을 부여**한다.
* 숫자 1이 정렬되도록 **display:flex**
*  부모요소를 기준으로 설정하기 위해, 부모요소에는 **position:relative**
* 자식요소에는 **position: absolute**



### Screen header

* Screen header는 대부분의 페이지에서 공통적으로 구현된다.



#### html 코드 작성

* friends.html에 **header** 코드를 작성한다.

```CSS
    <header class="screen-header">
        <h1 class="screen-header__title">Friends</h1>
        <div class="screen-header__icons">
            <span><i class="fas fa-search fa-lg"></i></span>
            <span><i class="fas fa-music fa-lg"></i></span>
            <span><i class="fas fa-cog fa-lg"></i></span>
        </div>
    </header>
```



#### CSS 코드 작성

* **componets/screen-header.css**에 코드를 작성한다.
* **styles.css**에 **@import** 한다.

```CSS
.screen-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 40px;
}
.screen-header__title {
  font-size: 32px;
  font-weight: 600;
}
.screen-header__icons span {
  margin-left: 25px;
}
```



#### Friend 문구 만들기

* Header 아래에 friend문구를 만든다.

```html
    <a id="friends-display-link">
        <i class="fas fa-info-circle"></i>Friends' Names Display
        <i class="fas fa-chevron-right fa-xs"></i>
    </a>
```

* **css/screens/friends.css** 를 생성하고 코드를 작성한다.

```CSS
#friends-display-link {
  text-align: center;
  display: block;
  background-color: #fafafa;
  padding: 15px 0px;
  font-size: 16px;
}
#friends-display-link i {
  color: rgba(0, 0, 0, 0.3);
  margin-right: 5px;
}
```

* **styles.css**에 **@import**한다.



### User Component 1

* 사진과 닉네임이 나오는 부분을 만든다.



#### VSC 단축키

```
.user-component*2
```

* 입력하면 해당 **class**를 가진 **div 2개**가 만들어진다.



#### html 코드 작성

```html
    <div class="user-component">
        <div class="user-component__column">
            <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" class="user-component__avatar" />
            <div class="user-component__text">
                <h4 class="user-component__title">Jaemin</h4>
                <h6 class="user-component__subtitle">My nickname is greedysiru</h6>
            </div>
        </div>
        <div class="user-component__column"></div>
    </div>
```



#### CSS 코드 작성

* **css/components/user-component.css**에 코드를 작성한다.
* **styles.css**에 **@import**하기

```CSS
.user-component,
.user-component__column:first-child {
  display: flex;
  align-items: center;
}
.user-component__avatar {
  width: 70px;
  height: 70px;
  border-radius: 27px;
  margin-right: 20px;
}
.user-component__title {
  font-weight: 600;
  font-size: 22px;
}
.user-component__subtitle {
  margin-top: 5px;
  font-size: 17px;
  color: rgba(0, 0, 0, 0.5);
}
```

* flexbox를 적용할 때, 부모 자식 요소를 잘 파악하고 적용하도록 한다.



### User Component 2

* 프로필 사진 아래에 채널 목록을 만든다.



#### html 코드 작성

```html
    <main class="friends-screen">
    <div class="user-component">
        <div class="user-component__column">
            <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" class="user-component__avatar--xl" />
            <div class="user-component__text">
                <h4 class="user-component__title">Jaemin</h4>
            <!--    <h6 class="user-component__subtitle">My nickname is greedysiru</h6> -->
            </div>
        </div>
        <div class="user-component__column"></div>
    </div>
    <div class="friedns-screen__channel">
        <div class="friedns-screen__channel-header">
             <span>Channel</span>
        </div>
             <i class="fas fa-chevron-up fa-xs"></i> 
             <div class="user-component">
                <div class="user-component__column">
                    <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" class="user-component__avatar--sm" />
                    <div class="user-component__text">
                        <h4 class="user-component__title">Channel</h4>
                    </div>
                </div>
                <div class="user-component__column">
                    <span>2</span>
                    <i class="fas fa-chevron-right fa-xs"></i>
                </div>
            </div>
        </div>
    </main>
```

* **div태그**들을 **main 태그** 안에 넣는다.



#### 변수 선언

* **margin 이나 padding을 바꿀 때, 일정한 값을 매번 입력하기 위해** 변수를 선언한다.

```CSS
  --horizontal-space: 40px;
```



#### CSS 코드 작성

* user avatar 가 제일 큰 경우의 CSS를 설정한다.

```CSS
.user-component__avatar--xl {
  width: 80px;
  height: 80px;
  border-radius: 30px;
  margin-right: 20px;
}
```



### Finishing Friends Screen

* 채널의 타이틀은 굵지 않으므로 **class명을 새로 만들어준다.**

```html
<h4 class="user-component__title user-component__title--not-bold">
  Channel
</h4>
```

* 채널 사진의 크기와 타이틀, 글자 색상을 **user-component.css**에서 설정한다.

```CSS
.user-component__avatar--sm {
  width: 60px;
  height: 60px;
  border-radius: 25px;
  margin-right: 20px;
}

.user-component__title--not-bold {
  font-weight: 400;
}

.user-component__column:last-child {
  color: rgba(0, 0, 0, 0.5);
}
```

* friends.css에서 경계선과 헤더의 설정을 한다.

```CSS
.friends-screen__channel {
  margin-top: 25px;
  border-top: 1px solid rgba(0, 0, 0, 0.2);
  padding-top: 15px;
}

.friends-screen__channel-header {
  margin-bottom: 30px;
  display: flex;
  justify-content: space-between;
  color: rgba(0, 0, 0, 0.5);
}
```



# Reference

https://nomadcoders.co/kokoa-clone/lobby