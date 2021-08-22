# [노마드코더]코코아톡 클론코딩 (7)(2021.1.8)



**상세 내용 [블로그](https://greedysiru.tistory.com/103) 참고**



# Cloning time

## 1. chats.html

### Chats Screen part One

* 이제부터는 전의 html코드를 가져와서 사용하므로 빠르게 진행
* 목표로하는 페이지의 모습에 맞게 **header**와 **icon**들을 적절한 것들로 바꾼다.
  * 상단 **icon** 추가
  * 하단 **chat icon** 채워짐 효과(다른 icon으로 대체)
  * 하단 **friends icon** 비워짐 효과(다른 icon으로 대체)
  * subtitle 추가 및 프로필 삭제 등
* **margin, padding**을 조절



### Chats Screen part Two

#### badge component

* 지난 시간에 만들었던 **badge**는 이번 페이지에도 사용되므로 **component화 한다.**
* **css/components/badge.css** 에 아래처럼 **badge**의 설정을 작성

```CSS
.badge {
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
}
```

* **css/style.css**에 **import**한다.

```CSS
@import "components/badge.css";
```

* **chats.htm**l에 적용한다.

```CSS
<div class="user-component__column">
  <span class="user-component__time">12:00</span>
  <div class="badge">
   1
  </div>
</div>
```

* **firends.html**에 적용한다.(chats.html하단에도 적용)

```CSS
<a class="nav__link" href="chats.html">
  <span class="nav__notification badge">1</span>
  <i class="fas fa-comment fa-2x"></i>
</a>
```



#### badge와 time 정렬

* badge와 time을 세로로 나란히 정렬한다.
* css/components/user-component.css에서 **flex-direction: column**설정 한다.

```CSS
.user-component__column:last-child {
  color: rgba(0, 0, 0, 0.4);
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
```



#### friends.html 수정

* 위처럼 **user-component__column**에 **flex-direction:column**을 주게 되면, friends.html의 화면이 깨지게 된다.
* 설정을 적용하지 않으려면, **부모 요소에 영향을 받지 않게 하기 위해서 div태그를 씌워준다.**

```CSS
<div>
  <span>2</span>
  <i class="fas fa-chevron-right fa-xs"></i>
</div>
```



## 2. find.html

### Find Screen part One

* chats.html을 토대로 만들 페이지를 구현하기 위해 삭제, 수정



#### icon css

* **icon css**를 만든다.
* **css/screen/fing.css**에서 아래와 같이 설정한다.

```CSS
.find-icons {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid rgba(0, 0, 0, 0.3);
}
.find-icons__icon {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.find-icons__icon i {
  font-size: 35px;
}
.find-icons span {
  margin-top: 18px;
}
```

* 이후 **styles.css**에 **import**

```CSS
@import "screens/find.css";
```



### Find Screen part Two

#### 색상 설정 변수화

* 자주 쓰는 설정은 변수화를 하는 것이 좋다.
* **css/variables.css**의 **:root**에 아래를 추가

```CSS
  --gray: rgba(0, 0, 0, 0.5);
```



#### Recommended Friends 만들기

* html 코드 작성

```html
<div class="recommended-friends">
  <h6 class="recommended-friends__title">recommended Friends</h6>
  <span>You have no recommended friends.</span>
</div>
```

* CSS 코드 작성 (**css/screens/find.css**)

```CSS
.recommended-friends {
  margin: 25px 0px;
  padding: 25px 0px;
  border-top: var(--main-border);
  border-bottom: var(--main-border);
}
.recommended-friends__title {
  font-size: 14px;
  color: var(--gray);
}
.recommended-friends span {
  display: block;
  margin: 100px 0;
  text-align: center;
  font-size: 18px;
  color: var(--gray);
}
```



### Find Screen part Three

#### Open post 만들기

* html 코드 작성

```html
        <div class="open-chat">
            <div class="open-chat__header">
                <h4 class="open-chat__title">Open chat</h4>
                <span>
                    Go to Openchat Home
                    <i class="fas fa-chevron-right fa-xs"></i>
                </span>
            </div>
            <div class="open-post">
                <div class="open-post__column">
                    <h5 class="open-post__title">#BTS</h5>
                    <h6 class="open-post__hashtags">#bts#army#friedns</h6>
                    <div class="open-post__members">
                        <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" />
                        <span class="open-post__member-count">820 members</span>
                        <div class="divider"></div>
                        <span class="open-post__member-status">Active</span>
                    </div>
                </div>
                <div class="open-post__column"></div>
            </div>
        </div>
```



* CSS 코드 작성

```CSS
.open-chat__header {
  display: flex;
  justify-content: space-between;
  opacity: 0.8;
  margin-bottom: 25px;
}

.open-chat__header span {
  opacity: 0.6;
}

.open-post {
  display: flex;
}

.open-post__title {
  font-weight: 600;
  margin-bottom: 7px;
}

.open-post__hashtags {
  text-transform: uppercase;
  opacity: 0.6;
}

.open-post__members {
  margin-top: 7px;
  display: flex;
  align-items: center;
}

.open-post__members img {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  margin-right: 5px;
}

.open-post__member-count {
  opacity: 0.5;
  font-size: 14px;
}

.open-post__members .divider {
  width: 2px;
  height: 15px;
  margin: 0 5px;
  background-color: rgba(0, 0, 0, 0.2);
}

.open-post__member-status {
  color: #ffb0e0;
}
```

* **uppercase**는 해당 요소를 대문자로 만들어 준다.



### Fing Screen part Four

#### Open post 마무리하기

* 남은 column의 컨텐츠를 채운다.
* html 코드 작성

```html
                <div class="open-post__column">
                    <div class="open-post__photo">
                        <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" />
                        <div class="open-post__heart-count">
                            <i class="fas fa-heart fa-xs"></i> <span>326</span>
                        </div>
                    </div>
                </div>
```

* CSS 코드 작성

```CSS
.open-post {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.open-post__photo img {
  width: 120px;
  height: 120px;
  border-radius: 10px;
}

.open-post__photo {
  position: relative;
}

.open-post__heart-count {
  background-color: var(--gray);
  color: whitesmoke;
  padding: 5px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 12px;
}

.open-post__heart-count span {
  margin-left: 3px;
}

```

* **position**에서 **absolute는 자식 요소**, **relative는 부모요소**인 것을 잊지말자.



# Reference

https://nomadcoders.co/kokoa-clone/lobby