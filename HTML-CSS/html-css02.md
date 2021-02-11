# [코드잇] HTML/CSS 시작하기 (2)(2021.2.11)



**상세 내용 [블로그](https://greedysiru.tistory.com/194?category=860702) 참고**

# 텍스트 스타일링

## 01. 텍스트 색

### 색 이름

* **CSS에서 정한 색 이름**
  * tomato, whitesmoke, aqua 등
* 140개의 색이 대부분 브라우저에서 지원



### RGB 값

* **빨강(Red), 초록(Green), 파랑(Blue)의 조화로 표현된 색 값**

```CSS
h1 {
  color : rgb(83, 237, 65);
}
```



### HEX 값 (16진법)

* RGB값을 16진법으로 표현

```CSS
h1 {
  color : #53ED41;
}
```



## 02. 몇 가지 텍스트 스타일링

### font-weight

* **폰트 굵기를 설정**
* 100, 200, 300, 400, 500, 600, 700, 800, 900이 있다.
  * font-weight: normal == font-weight: 400
  * font-weight: bold == font-weight: 700
* 브라우저나 폰트에따라서, 지원하는 폰트 굵기 값이 다르다.



### text-decoration

* **underline** : 밑줄
* **overline** : 윗줄
* **line-through** : 가운데 줄
* **none** : 효과 없애기
  * 주로 **a태그**의 효과를 없애는데 사용

```HTML
<style>
  a {
    text-decoration: none;
  }
</style>
<body>
  <a href="사이트 주소" >사이트 이동</a>  
</body>
```



## 03. 가운데 정렬

* **inline display**인 경우, **text-align: center**를 적용하여도 정렬이 안된다.
* **div태그**로 감싼 뒤, class를 지정하여 정렬한다.



## 04. 폰트 크기

### 절대적(Absolute)인 방법

* **px**
* **pt** : px의 1.33배 크다

### 상대적(Relative)인 방법

* **%** : 부모 요소의 폰트크기를 기준으로 한다.
* **em** : 1em == 100%



## 05. line-height

* **줄 간격을 조절할 수 있다.**
* **content area**
  * **실제 내용이 들어가 있는 영역**
  * font-family와 font-size에 따라서 정해진다.
  * line-height는 영향을 주지 못한다.
* 즉, l**ine-height**는 **각 줄이 실질적으로 차지하는 공간만을 정한다.**



## 06. 폰트 종류

### Serif

* **바깥이 구부러진 형태**
* Times
* Times New Roman
* 궁서체



### Sans-Serif

* **깔끔한 디자인**
* Arial
* 굴림체



### Monospace

* **모든 글자 폭이 똑같다.**
* 프로그래밍용 폰트로 많이 사용
* Courier
* Courier New



### Cursive

* **필기체**
* Comic Sans MS
* Monotype Corsiva



### Fantasy

* **특이한 형태의 폰트들**
* Impact
* Haettenschweiler



## 07. 폰트 적용

> 선택자 {
>
> ​		font-family : 적용할 폰트1, 적용할 폰트2, 폰트의 종류;
>
> }

* 사용자의 설치된 폰트여야 적용된다.
* **적용할 폰트 1**이 없으면, **적용할 폰트 2를 찾는다.**
* **적용할 폰트 2**가 없으면, **지정된 폰트의 종류 중에서 하나를 적용**한다.
  * 폰트의 종류 : Serif, Sans-Serif 등



## 08. 구글 폰트

* **사용자에게 폰트파일을 제공**
* 구글이 제공하는 폰트를 사용할 수 있다.
* **head태그에 사이트에서 제공되는 link를 적용하면 된다.**



### 예시

```HTML
<head>
  <link href="https://fonts.googleapis.com/css?family=Barrio|Roboto" rel="stylesheet">
</head>
<style>
  h1 {
    font-family: 'Roboto', sans-serif;
  }
  h2 {
    font-family: 'Barrio', cursive;
  }
</style>
```



## 09. 폰트 파일 사용하기

* 가지고있는 폰트 파일을 CSS로 불러올 수 있다.

> @font-face {
>
> ​		src: url("파일 경로");
>
> ​		font-family: "폰트 이름"
>
> }

* 가져온 폰트를 **font-family**로 이름을 지정할 수 있다.



## 10. span 태그

* **요소를 묶을 수 있다.**
* 특정 테스트를 스타일링하고 싶을 때 사용

# Reference

[코드잇 - HTML/CSS 시작하기](https://www.codeit.kr/courses/web-publishing/topics/getting-started-with-html-css)