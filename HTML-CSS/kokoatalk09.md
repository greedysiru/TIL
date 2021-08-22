# [노마드코더]코코아톡 클론코딩 (9)(2021.1.9 ~ 10)



**상세 내용 [블로그](https://greedysiru.tistory.com/106) 참고**



# Cloning time

## chat.html

### Chat Screen part One

* **settings.html**을 토대로 코드 작성한다.
  * 목표와 비교하며 수정, 삭제
* **html을 기반으로 필요한 CSS 코드 작성**



#### chats.html 링크

* chats.html 에서 특정 대화를 누르면 대화창이 뜨도록 구현
  * 그러므로 chats.html의 component에 아래와 같이 링크를 설정

```html
    <a href="chat.html">
    <div class="user-component">
        <div class="user-component__column">
            <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" class="user-component__avatar" />
            <div class="user-component__text">
                <h4 class="user-component__title">
                  Jaemin
              </h4>
                <h6 class="user-component__subtitle">
                  My nickname is greedysiru
              </h6>
            </div>
        </div>
        <div class="user-component__column">
            <span class="user-component__time">12:00</span>
            <div class="badge">1</div>
        </div>
    </div>
        </a>
```



#### Background color 설정

* 대화창의 배경 색상을 설정
* **css/screens/chat.css**

```CSS
.mgr {
  margin-right: 25px;
}
#chat-screen {
  background-color: #abc1d1;
}
```



### Chat Screen part Two

#### alt-header 고정시키기

* 채팅창에서 스크롤을 했을 때, **alt-haeder가 고정**
* **css/screens/caht.css**에서 코드를 입력

```CSS
#chat-screen .alt-header,
#chat-screen .status-bar {
  top: 0;
  position: fixed;
  width: 100%;
  background-color: #abc1d1;
  box-sizing: border-box;
}
```

* 이와 동시에, **상태창도 고정**
* 텍스트가 겹치면 안 되므로 **배경색상도 적용**



#### alt-header 정렬하기

* **alt-header**를 고정하면 자식 요소들이 한쪽으로 쏠린다.
* 이전에 **status-bar component**를 정렬할 때 사용한 아래와 같은 방법을 **alt-screen-haeder.css에 사용하여 정렬**

```CSS
.alt-header__column {
  width: 33%;
}
.alt-header__column:nth-child(2) {
  text-align: center;
}
.alt-header__column:last-child {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.alt-header__column span:last-child {
  margin-left: 30px;
}
```



#### timestamp 추가하기

* 채팅창 상단의 년,월,일 표기를 만든다.

```html
    <main class="main-screen main-chat">

        <div class="chat__timestamp">
            Tuesday, June 30, 2020
        </div>

    </main>
```

* CSS 설정

```CSS
.main-chat {
  margin-top: 150px;
}
```



#### z-index 설정하기

* 배경색상을 설정하면, header에 stauts bar가 가려서 보이지 않게 된다.
* **z-index**를 사용해서 **layer 순서를 설정**

```CSS
#chat-screen .alt-header {
  top: 10px;
  z-index: 1;
}
#chat-screen .status-bar {
  z-index: 2;
}
```

* **숫자가 작을 수록 낮은 layer**
* **fixed, absolute position에 사용할 수 있다.**



### Chat Screen part Three

#### timestamp CSS

* **timestamp**를 원하는 모습에 맞게 CSS로 설정

```CSS
.chat__timestamp {
  color: whitesmoke;
  background-color: #92a4b2;
  padding: 8px 15px;
  border-radius: 25px;
}
```



#### main-chat CSS

* **timestamp**를 완성했으므로 대화목록 컨텐츠를 넣기전에 **main-chat CSS를 설정**

```CSS
.main-chat {
  margin-top: 110px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
```

* 컨텐츠들이 세로로 정렬되어야 하므로 **flex-direction: column을 설정**



#### message-row 만들기

* 대화창의 메세지 컨텐츠들을 만든다.
* html 작성

```html
        <div class="message-row">
            <img src="https://tistory3.daumcdn.net/tistory/4367973/attach/059c57a4a960451fad4115308781a782" />
            <div class="massage-row__content">
                <span class="message__author">
                    Jaemin
                </span>
                <div class="messag__info">
                    <span class="message__bublle">
                        Hi!
                    </span>
                    <span class="message__time">
                        21:27
                    </span>
                </div>
            </div>
        </div>
```

* 컨텐츠들을 적절하게 **div로 분할**한다.



### Chat Screen part Four

#### message-row CSS

* message-row의 컨텐츠를 적절하게 설정한다.

```CSS
.message-row {
  width: 100%;
  display: flex;
}
.message-row img {
  width: 45px;
  height: 45px;
  border-radius: 40%;
  margin-right: 10px;
}
.message__author {
  opacity: 0.8;
  font-size: 15px;
  margin-bottom: 8px;
  display: block;
}
.message__bubble {
  background-color: white;
  padding: 10px;
  border-radius: 15px;
  border-top-left-radius: 0px;
  margin-right: 5px;
  font-size: 18px;
}
.message__info {
  display: flex;
  align-items: flex-end;
}
.message__time {
  opacity: 0.8;
  font-size: 13px;
}
```

* 카카오톡의 메세지 bubble은 별도의 이미지이다.
  * 이미지를 사용하지 않고 CSS로 비슷하게 구현한다.
  * 전체 **border-radius 를 설정**한다.
  * 좌측 상단  **border-top-left-radius: 0px 로 원하는 곳의 모서리만 설정**할 수 있다.



### Chat Screen part Five

#### 내가 보낸 메세지 추가하기

* 내가 보낸 메세지를 구현
* 전 파트에서 구현한 메세지 양식을 토대로 만든다.
  * 프로필 사진 제거, 작성자 이름 제거, 메세지 텍스트 변경

```html
        <div class="message-row message-row--own">
            <div class="massage-row__content">
                <div class="message__info">
                    <span class="message__bubble">
                        Hi nice to meet you!
                    </span>
                    <span class="message__time">
                        21:27
                    </span>
                </div>
            </div>
```



#### message-row--own

* 내가 보낸 메세지의 클래스 명을 설정한다.(**modifier**)
* CSS를 적용

```CSS
.message-row--own {
  justify-content: flex-end;
}
.message-row--own .message__bubble {
  background-color: var(--yellow);
  border-top-right-radius: 0px;
  border-top-left-radius: 15px;
  margin-right: -10px;
  margin-left: 5px;
}
```

* **말풍선의 꼬리의 방향이 반대이므로 이를 수정**



#### 컨텐츠 순서 바꾸기

* 대화 내용과 시간을 바꿔야한다.
* 2 가지의 방법이 있다.



##### order

```CSS
.message-row--own .message__time {
order: 0;
margin-right: 5px;
}
.message-row--own .message__bubble {
order: 1;
margin-right: 0px;
}
```

* 이 방법은 **flex의 자식요소**에 적용할 수 있다.
* **0이면 첫 번째에 위치**한다.



##### row-reverse

```CSS
.message-row--own .message__info {
  flex-direction: row-reverse;
}
```

* 간단하게 **flex-direction: row-reverse**를 적용



### Write Message Input

* 메세지 입력창을 만든다.

```html
    <form class="reply">
        <div class="reply__column">
            <i class="far fa-plus-square fa-lg"></i>
        </div>
        <div class="reply__column">
            <input type="text" placeholder="Write a message..." />
            <i class="far fa-smile fa-lg"></i>
            <button>
                <i class="fas fa-arrow-up fa-lg"></i>
            </button>
        </div>
    </form>
```

* CSS를 입력한다

```CSS
.reply {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: whitesmoke;
  display: flex;
  justify-content: space-between;
  padding: 5px 25px;
  box-sizing: border-box;
  align-items: center;
}
.reply .reply__column:first-child {
  width: 10%;
}
.reply .reply__column:last-child {
  width: 90%;
  position: relative;
}
.reply input {
  padding: 10px;
  width: 100%;
  border: var(--main-border);
  border-radius: 20px;
}
.reply__column:last-child > i,
.reply__column:last-child button {
  position: absolute;
  right: 0;
}
.reply__column:last-child > i {
  right: 25px;
  top: 10px;
}
.reply__column:last-child button {
  top: 3.5px;
  right: -18px;
}
.reply__column button {
  background-color: var(--yellow);
  border: none;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.reply i {
  opacity: 0.5;
}
.reply__column button i {
  opacity: 1;
}
```

* **부모요소에 width가 있어야 자식 요소에 width를 가질 수 있다.**

# Reference

https://nomadcoders.co/kokoa-clone/lobby

