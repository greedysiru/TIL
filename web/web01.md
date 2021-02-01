# [스파르타코딩] 웹개발 종합반 항해 1기 1주차 (1)(2021.2.1)



**상세 내용 [블로그](https://greedysiru.tistory.com/155?category=875936) 참고**



# 1. 서버/클라이언트/웹의 동작 개념

1. **클라이언트(브라우저)**는 **서버**에게 웹 페이지를 **요청**한다.
2. **서버**는 웹페이지를 **전달**한다.
3. **클라이언트(브라우저)**는 **출력**



# 2. HTML, CSS 기본 내용

* **HTML**: 뼈대, 문서형태 기반, 태그문법
  * body: 페이지의 내용
  * head: 페이지의 속성 정보
* **CSS**: 꾸미기

# 3. CSS 기초

* HTML의 부모-자식 구조 : 부모 태그가 영향을 받으면 그것의 자식 태그도 영향을 받는다.

```HTML
<div> <!-- 부모 -->
  <div> <!-- 자식 1 -->
    
  </div>
  <div> <!-- 자식 2 -->
    
  </div>  
</div>
```



## CSS 사용하기

* **head**태그안에 **style**태그를 생성하여 작성한다.
* 꾸밀 요소를 선택하여 적용한다.
* 예시

```HTML
<head>
    <meta charset="UTF-8">
    <title>로그인페이</title>
    <style>
        .mytitle{
            color: tomato;
        }
    </style>
</head>
<body>
    <h1 class="mytitle">로그인 페이지</h1>
```



# 4. 자주 쓰이는 CSS 연습하기

 ## margin, padding

요쇼의 경계를 기준으로

* **padding**: 안쪽 여백
* **margin**: 바깥 여백



## 가운데 정렬

1. **width**를 설정
2. **margin : auto**

태그가 **inline**인 경우, **display: block**

# 5. 폰트, 주석, 파일분리

## 구글 웹 폰트 입히기

> https://fonts.google.com/?subset=korean

* 위 사이트에서 원하는 폰트를 가져와 웹 페이지에 적용할 수 있다.
* **link 태그**와 **font-family**를 복사하여 각각 **head**와 **style**에 붙여넣기한다.

* 예시

```HTML
<head>
    <meta charset="UTF-8">
    <title>로그인페이지</title>
    <link href="https://fonts.googleapis.com/css2?family=Jua&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Jua', sans-serif;
        }
    </style>
</head>
```



## 주석

* 코드에 대한 설명을 할 때 사용
* 브라우저 / 컴퓨터가 읽지 않는다.

> 단축키 : command + /(슬래시)



## CSS 파일 분리

* style 태그의 내용을 별도의 파일로 분리할 수 있다.
* 같은 디렉토리에 style.css와 같은 파일을 만들고 **head 태그**에 **link**한다.

* 예시

```HTML
<head>
	<link rel="stylesheet" type="text/css" href = "(css파일이름).css">
</head>
```



# 6. 부트스트랩

* 현업에서 미리 완성된 CSS를 모아둔 것
* 검증되고 좋은 디자인의 CSS들이 많이 있다.



# 7. 부트스트랩 사용하기

## 적용하는 법

1. 부트스트랩 시작 템플릿을 **head**에 붙여넣는다.

```HTML
<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
        integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js"
        integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q"
        crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js"
        integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"
        crossorigin="anonymous"></script>
</head>
```

2. 아래의 부트스트랩 컴포넌트에서 적용하고 싶은 것을 가져와 붙여넣는다.

> https://getbootstrap.com/docs/4.0/components/alerts/

```HTML
<body>
    <button type="button" class="btn btn-primary">버튼입니다.</button>
</body>
```



# Reference

**스파르타코딩 - 웹개발 종합반**