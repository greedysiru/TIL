# [노마드코더]코코아톡 클론코딩 (10)(2021.1.10)



**상세 내용 [블로그](https://greedysiru.tistory.com/108) 참고**



# Clonning time

## 1. Splash Screen

* 로딩화면을 구현한다.
* 사라지는 효과를 넣는다.



### Splash Screen part One

* 첫 화면인 **friends.html에 구현**한다.
* 하단에 독립적인  **div**를 만든다.

```html
    <div id="splash-screen">
        <i class="fas fa-comment"></i>
    </div>
```



#### Splash Screen CSS

* 화면 전제를 채울 수 있도록 한다.

```CSS
#splash-screen {
  background-color: var(--yellow);
  position: absolute;
  height: 100vh;
  width: 100vw;
  top: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 132px;
}
```

* 모든 layer의 위로 오게 하기 위해서 **position: absolute**를 한다.



### Splash Screen part Two

#### animation 효과 넣기

* 로딩창이 사라지는 효과를 삽입한다.

```CSS
@keyframes hideSplashScreen {
  for {
    opacity: 1;
  }
  to {
    opacity: 0;
    visibility: hidden;
  }
}
#splash-screen {
  background-color: var(--yellow);
  position: absolute;
  height: 100vh;
  width: 100vw;
  top: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 132px;
  animation: hideSplashScreen 0.3s ease-in-out forwards;
  animation-delay: 2s;
}
```

* **forwards** : Animation의 마지막 속성을 유지한다.
* **visibility : hidden** 은 Animation이 끝나면 마우스에 걸리지 않게 screen을 빼준다.
* **animation-delay** : 딜레이 후에 Animation을 실행한다.



## 2. Navigation Animation

* Navigation에 다채로운 효과를 부여한다.

```CSS
@keyframes appearBtnAnimation {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
    transform: none;
  }
}
.nav__btn {
  transform: translateY(50px);
  opacity: 0;
  animation: appearBtnAnimation 0.5s ease-in-out forwards;
}
.nav__btn:nth-child(2) {
  animation-delay: 0.3s;
}
.nav__btn:nth-child(3) {
  animation-delay: 0.5s;
}
.nav__btn:last-child {
  animation-delay: 0.8s;
}
```

* 각 요소에 **animation-delay**를 주어서, 차례대로 나타나도록 한다.



## 3. More Animations

### 설정 cog 돌아가기 효과

* 톱니바퀴에 마우스 커서를 올렸을 때 돌아가는 효과를 삽입
* **css/components/screen-header.css**

```CSS
@keyframes rotateCog {
  from {
    transform: none;
  }
  to {
    transform: rotateZ(360deg);
  }
}
.screen-header__icons .fa-cog:hover {
  animation: rotateCog 2s linear infinite;
}
```



### heart 박동 효과 추가

* heart에 커서를 올렷을 때 박동 효과 추가
* **css/screens/find.css**

```CSS
@keyframes heartBeat {
  0% {
    color: whitesmoke;
    transform: none;
  }
  50% {
    color: tomato;
    transform: scale(1.5);
  }
  100% {
    color: whitesmoke;
    transform: none;
  }
}
.open-post__heart-count:hover i {
  will-change: transform;
  animation: heartBeat 1s linear infinite;
}
```

* **will-change** : 브라우저에게 바뀌는 것을 말해준다. **Animation을 안정화 한다.**



## 4. Animating Chats Screen

* 채팅창에 다양한 효과를 삽입한다.
* **css/screens/chat.css**

```CSS
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    transform: none;
    opacity: 1;
  }
}
.main-chat {
  margin-top: 180px;
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeIn 0.8s linear;
}
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
  transition: transform all 0.3s ease-in-out;
}
.reply input {
  padding: 10px;
  width: 100%;
  border: var(--main-border);
  border-radius: 20px;
  transition: all 0.3s ease-in-out;
}
.reply:focus-within .reply__column:first-child,
.reply:focus-within .fa-smile,
.reply:focus-within button {
  transition: opacity 0.3s ease-in-out;
  opacity: 0;
}
.reply:focus-within .reply__column:first-child,
.reply:focus-within .fa-smile,
.reply:focus-within button {
  opacity: 0;
}
.reply input:focus {
  width: 92vw;
  transform: translateX(-13%) translateY(-80px);
}
.reply:focus-within {
  transform: translateY(80px);
}
```

* **focus-within** : state selector
  *  내부에 **focus 되어 있는 요소**가 있는지 알 수 있다.



## 5. No Mobile Media Query

* 스크린이 일정 크기 이상으로 늘어났을 때, **Media Query를 사용해서 안내문구를 출력**하도록 한다.
* **모든 페이지 html에 아래와 같이 div를 추가한다.**

```html
    <div id="no-mobile">
        <span>Your screen is too big ㅠㅠ</span>
    </div>
```

* **Media Query**를 입력한다.**(css/components/no-mobile.css)**

```CSS
#no-mobile {
  position: absolute;
  z-index: 99;
  height: 100vh;
  width: 100vw;
  background-color: var(--yellow);
  display: flex;
  top: 0;
  justify-content: center;
  align-items: center;
  font-size: 32px;
}
@media screen and (max-width: 645px) {
  #no-mobile {
    display: none;
  }
}
```



# Reference

https://nomadcoders.co/kokoa-clone/lobby