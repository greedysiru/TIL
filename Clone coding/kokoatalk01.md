# [노마드코더]코코아톡 클론코딩 (1)(2021.1.1 ~ 2)



**상세 내용 [블로그](https://greedysiru.tistory.com/89) 참고**



# Introduction

## 수업 환경

Google Chrome

Visual Studio Code

GitHub desktop



# Learning HTML

* 폴더명과 파일명은 소문자로
* **.html** 확장자 사용



## 1. HTML tag

>`<tag attrname= "atrrval">` content`</tag>`

* 올바른 위치에 올바른 태그를 사용
* 브라우저는 태그를 이해



## 2. list tag

* **ol** : ordered list

```html
<ol>
  <li>츄르</li>
  <li>간식</li>
  <li>고기</li>
</ol>
```

* **ul** : unordered list

```html
<ul>
  <li>츄르</li>
  <li>간식</li>
  <li>고기</li>
</ul>
```



## 3.  Attributes

* 속성(Attributes)은 태그의 기능을 추가
* 속성이 있어야만하는 태그도 있으며 태그마다 가지는 속성이 있다.



### a tag

```html
<a href = "http://www.google.com" target="_blank">go to the google.com</a>
```

* **a** : 다른 웹사이트로 이동
  * **href** : hyperlink reference 이동할 곳을 알려주는 속성
  * **target**
    * _self : 기본값
    * _blank : 새 창 열기



### img tag

```html
<img src="이미지 주소">
```

* 이미지 삽입 태그
* self-closing tag(자체 닫기 태그)



## 4. HTML 문서의 구조

```html
<!DOCTYPE html>       <!-- 필수 첫 라인-->
<html>                <!-- 사이에 넣는 것이 html 코드-->
  
  <head>               <!-- 페이지의 환경을 설정-->
    <title>Home - My first website.</title>
  </head>
  
  <body>               <!-- 사용자가 보는 컨텐츠-->
    <h1>
      Hello!
    </h1>
    <a href = "http://www.google.com" target="_blank">go to the google.com</a>
    <img src="img/anything.png">
  </body>
  
</html>
```

* **!DOCTYPE html** : 브라우저에게 html인 것을 선언
* **html** : 이 태그 사이에 넣는 것이 html 코드라는 것을 표시
* **head** : 페이지 환경을 설정
* **body** : 사용자에게 보여질 태그들과 content를 넣는다.



## 5. head의 모든 것

```html
...
<html lang="kr">
  <head> <!-- 페이지의 환경을 설정-->
    <title>Home - My first website.</title>
    <meta name="descripton" content="This is my website">
    <meta charset="utf-8">
    <link 
          rel="shortcut icon" 
          sizes="16x16 32x32 64x64" 
          href="https://nomadcoders.co/m.png"
          >
  </head>
  ...
```

* **meta** : 표현할 수 없는 다양한 종류의 메타데이터
  
  * charset :  **"utf-8"**을 입력
  * name, cotent  검색 엔진에게 웹 사이트의 정보를 알려 준다.
  * self-closing tag
* **html**의 lang 속성 : 검색엔진에게 주된 사용 언어를 알려준다.
* **link** : 웹 브라우저에서 탭의 아이콘 이미지 설정

  

## 6. form tag

```html
...
<form>
  <input type="file" accept=".png"/>
  <input required placeholder="Name" type='text'/>
  <input required placeholder="Last Name"  type='text'/>
  <input required placeholder="Username" type='text'/>
  <input required placeholder="password" minlength="10" type='password'/>
  <input type="submit"  value="Create Account"/>
</form>
...
```

* **form** : 입력창 구획
* **input** : 입력창 생성, 다양한 속성으로 기능을 추가
  * type : text, submit, file, password
  * placeholder : 입력창에 표시될 이름
  * required : 입력할 것을 사용자에게 표시
  * minlength : 최소 입력될 글자



### label tag

```html
<form>
  <label for="profile">profile photo</label>
  <input id="profile" type="file" accept=".png"/>
  <label for="website">website</label>
  <input id="website" type="range" />
</form>
```

* **label** : 사용자 인터페이스 항목(input)의 설명
  * for속성으로 input tag의 id를 가리킬 수 있다.



## 7. id 속성

* unique identifier(고유 식별자)

* element당 하나의 id만 가질 수 있다.

  

## 8. Semantic HTML

| Semantic tag                                           | non-Semantic tag                 |
| :----------------------------------------------------- | -------------------------------- |
| `<header>` 소개 및 탐색에 도움을 주는 content를 나타냄 | `<div>` division컨트롤 분할 요소 |
| `<footer>` 꼬리말                                      | `<span>` 짧은 text               |
| `<address>` 주소                                       |                                  |



# Reference

https://nomadcoders.co/kokoa-clone/lobby