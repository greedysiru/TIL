# [항해99 1기] [Chapter1] 웹개발 미니 프로젝트 (2) (2021.3.2)



# Bulma

* 미리 정해진 모습의 클래스를 가져다 쓰는 무료 CSS 프레임 워크
* Bulma의 클래스에 CSS 추가 가능
* 공식 문서

> https://bulma.io/documentation/



## 01. Hero 배너

* 화면 전체 너비를 채우는 배너 클래스
* 클래스를 중첩해서 색, 그래디언트, 높이를 변경 가능

```html
<section class="hero is-primary is-bold is-medium">
    <div class="hero-body">
        <div class="container">
            <h1 class="title">
                Hero title
            </h1>
            <h2 class="subtitle">
                Hero subtitle
            </h2>
        </div>
    </div>
</section>
```



## 02. Section

* body 태그 안에 넣어서 구역을 나눌 때 사용

```html
<section class="section">
    <div class="container">
        <h1 class="title">Section</h1>
        <h2 class="subtitle">
            A simple container to divide your page into <strong>sections</strong>, like the one you're
            currently reading
        </h2>
    </div>
</section>
```

