# [코드잇] 반응형 웹 퍼블리싱 (2021.2.19)



**상세 내용 [블로그](https://greedysiru.tistory.com/214) 참고**



# 반응형 웹

* Responsive Web Design
* **브라우저 사이즈에 맞춰서 레이아웃이 바뀌는 것**
* 모바일, 태블릿 버전을 만들지 않아도 된다.



## media query

```CSS
/* 기본 폰트 크기*/
h1 {
  font-size: 24px;
}

p {
  font-size: 16px;
}

/* 브라우저의 가로길이가 768px을 넘어갈 때 */
@media (min-width: 768px) {
  h1 {
    font-size: 36px;
  }  
  p {
    font-size: 24px;
  }  
}

/* 브라우저의 가로길이가 992px을 넘어갈 때 */
@media (min-width: 992px) {
  h1 {
    font-size: 48px;
  }
  p {
    font-size: 32px;
  }
}
```

* **@media**를 이용하여 브라우저 화면 크기에 따른 설정을 할 수 있다.



# 부트스트랩

## 01. 부트스트랩 소개

* **무료로 제공되는 HTML, CSS, JavaScript 프론트 엔드 프레임워크**
* 부트스트랩 CSS, JavaScript 코드를 붙여넣기하여 적용한다.

> https://getbootstrap.com/



## 02. 부트스트랩 그리드

### 기본 구성원

1. 컨테이너 (container)
2. 행 (row)
3. 열 (column)



### 기본 규칙

1. 행은 컨테이너 안에 넣는다.
2. 열은 행안에 넣는다. 열만이 행의 직속 자식이 될 수 있다.
3. 콘텐츠는 열 안에 넣는다.

위 규칙을 지키면, 의도한 레이아웃을 만들 수 있다.



### 기본 사용법

* 부트스트랩 그리드는 한 줄에 기본적으로 12칸의 열 (column)이 있다.
  * 한 줄을 정확히 3등분 -> 네 칸을 차지하는 열 세 개를 사용 (class = "col-4")
  * 한 줄을 정확히 2등분 -> 여섯 칸을 차지하는 열 두 개를 사용 (class= "col-6")
* 12칸을 넘는 경우, 새로운 줄로 넘어간다.



#### 예시

```HTML
<body>
  <div class="container">
    <div class="row">
      <!-- 정확히 3등분 -->
      <div class="col-4 first">first</div>
      <div class="col-4 second">second</div>
      <div class="col-4 third">third</div>
    </div>

    <div class="row">
      <!-- 정확히 2등분 -->
      <div class="col-6 first">first</div>
      <div class="col-6 second">second</div>
    </div>

    <div class="row">
      <!-- 1대 5 비율 -->
      <div class="col-2 first">first</div>
      <div class="col-10 second">second</div>
    </div>

    <div class="row">
      <!-- 1대 2대 1 비율 -->
      <div class="col-3 first">first</div>
      <div class="col-6 second">second</div>
      <div class="col-3 third">third</div>
    </div>
  </div>
</body>
```



### 중첩

* 8칸으로 나누고 싶은 경우
  * col-6 두 개를 사용
  * 그 안에서 col-3으로 각각 4등분
* 중첩을 하기 위해서는 열 안에 새로운 행을 써야한다.



### 예시

```HTML
<body>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <div class="row"> <!-- 중첩을 위한 새로운 행 -->
          <div class="col-3 first">1</div>
          <div class="col-3 second">2</div>
          <div class="col-3 third">3</div>
          <div class="col-3 fourth">4</div>
        </div>
      </div>

      <div class="col-6">
        <div class="row"> <!-- 중첩을 위한 새로운 행 -->
          <div class="col-3 first">5</div>
          <div class="col-3 second">6</div>
          <div class="col-3 third">7</div>
          <div class="col-3 fourth">8</div>
        </div>
      </div>
    </div>
  </div>
</body>
```



## 03. 부트스트랩 반응형 그리드

### 부트스트랩에서 정의한 구간

1. **Extra Small (<576px)**: 모바일
2. **Small(>= 576px):** 모바일
3. **Medium (>= 768px):** 태블릿
4. **Large (>= 992px):** 데스크탑
5. **Extra Large (>= 1200px):** 와이드 데스크탑



### 컨테이너 (Container)

* 가운데 정렬이 되어 있고, 그리드의 행들을 감싸주는 역할
* **class="container"**
  * 구간별로 그리드에 고정된 width를 설정
* **class="container-fluid"**
  * 그리드는 항상  width: 100%



#### **class="container"**

* 구간별로 그리드에 고정된 가로값을 설정할 경우 사용
* 예상 가능한 레이아웃

```CSS
.container {
  width: 100%; /* extra small */
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

/* small */
@media (min-width: 576px) {
  .container {
    max-width: 540px;
  }
}

/* medium */
@media (min-width: 768px) {
  .container {
    max-width: 720px;
  }
}

/* large */
@media (min-width: 992px) {
  .container {
    max-width: 960px;
  }
}

/* extra large */
@media (min-width: 1200px) {
  .container {
    max-width: 1140px;
  }
}
```



### 열 (column)

* 반응형 구간별로 열이 차지하는 칸의 개수도 다르게 할 수 있다.



#### 예시 1

* 구간별로 모두 설정

```HTML
<div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2">
```



#### 예시 2

* 특정 구간만 설정

```HTML
<div class="col-12 col-lg-3">
```

large부터 3칸 차지



# Reference

[코드잇 - HTML/CSS 시작하기](https://www.codeit.kr/courses/web-publishing)