# [노마드코더]코코아톡 클론코딩 (8)(2021.1.8 ~ 9)



**상세 내용 [블로그](https://greedysiru.tistory.com/104) 참고**



# Cloning time

## 1. more.html

### More Screen part One

* chats.html을 토대로 코드 작성하기

  * **margin, padding** 페이지에 맞게 조절

  ```CSS
  .more-screen .icon-row {
    margin-top: 35px;
  }
  .more-suggestions {
    margin-top: 50px;
    border-top: var(--main-border);
    padding-top: 40px;
  }
  .more-suggestions__title {
    margin-bottom: 30px;
  }
  ```

  

* 자주 사용되는 **find-icon** 컴포넌트화 하기

  * **css/components/icon-row.css에 icon-row** 클래스명으로 정리
  * **styles.css에 import**

  ```CSS
  .icon-row {
    display: flex;
    justify-content: space-between;
  }
  .icon-row__icon {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .icon-row__icon i {
    font-size: 35px;
  }
  .icon-row span {
    margin-top: 18px;
  }
  ```



### More Screen part Two

#### 카카오 아이콘 설정

* 하단의 카카오 스토리 아이콘을 만든다.
* **css/screens/more.css**

```CSS
.more-suggestions__icons {
  display: flex;
  margin-top: 30px;
}
.more-suggestions__icon {
  margin-right: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.more-suggestions__icon-image {
  width: 60px;
  height: 60px;
  background-color: var(--yellow);
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}
.more-suggestions__icon-image i {
  font-size: 32px;
  color: whitesmoke;
}
```



## 2. settings.html

### settings.html 링크 추가하기

* **more.html**의 **cog** 그림에 **settings**로 이어지는 링크를 추가한다.

```html
<a href="settings.html">
  <i class="fas fa-cog fa-lg"></i>
</a>
```



### Settings Screen part One

* more.html 토대로 코드 작성하기
  * 삭제할것, 수정할것 처리
  * CSS코드 작성 후  **import하기**

```CSS
.settings__setting {
  padding: 20px 0;
  border-bottom: var(--main-border);
  font-size: 18px;
  display: flex;
  align-items: center;
}
.settings__setting i {
  opacity: 0.8;
  margin-right: 20px;
  font-size: 22px;
}
.settings__setting {
  display: flex;
}
.settings__setting span:first-child {
  margin-right: 20px;
}
```

* **header component 작성하기**

```CSS
.alt-header {
  display: flex;
  align-items: center;
  padding: var(--horizontal-space);
  margin: 15px 0px;
  justify-content: center;
}
.alt-header__title {
  font-size: 28px;
  font-weight: 600;
}
.alt-header__column:first-child {
  margin-right: auto;
}
.alt-header__column:last-child {
  margin-left: auto;
}
```



### Settings Screen End

#### main 리스트 column 추가

* **column을 추가**하여 요소를 더 넣을 수 있게 한다.

```html
<main class="main-screen more-screen">
        <ul class="Settings-list">
            <li class="settings__setting">
                <div class="settigs_setting-column">
                <i class="fas fa-bullhorn"></i>
                <span>Notices</span>
                </div>
                <div class="settigs_setting-column"></div>
            </li>
            <li class="settings__setting">
                <div class="settigs_setting-column">
                <i class="fas fa-flask"></i>
                <span>Kokoa Lap</span>
                </div>
            </div>
            <div class="settigs_setting-column"></div>
            </li>
            <li class="settings__setting">
                <div class="settigs_setting-column">
                <span class="holebadge--black">i</span>
                <span>Version</span>
            </div>
            <div class="settigs_setting-column">Latest Version</div>
            </li>
        </ul>
    </main>
```

* CSS 설정
  * 추가한 **column**들의 디테일을 설정한다.

```CSS
.settings__setting {
  padding: 20px 0;
  border-bottom: var(--main-border);
  font-size: 22px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.settings__setting i {
  opacity: 0.8;
  margin-right: 20px;
  font-size: 22px;
}
.settings__setting span:first-child {
  margin-right: 20px;
}
.settigs_setting-column {
  display: flex;
}
.settings__setting-column:last-child {
  opacity: 0.5;
}
```



# Reference

https://nomadcoders.co/kokoa-clone/lobby