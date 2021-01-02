# [노마드코더]코코아톡 클론코딩 (1)(2021.1.1 ~ 2)



**본 내용은 해당 [강의](https://nomadcoders.co/kokoa-clone/lobby) 토대로 작성**



# Introduction

## 수업 환경

Google Chrome

Visual Studio Code

GitHub desktop



## 1. 웹사이트

크롬 브라우저에서 아래처럼 브라우저의 소스코드를 볼 수 있다.

> [Chrome] View(보기) - Developer(개발자 정보) - View Source(소스 보기)

### 무엇이 웹 사이트를 만들까?

* text 파일이다.
* 텍스트 파일 -> 브라우저 -> 이해해서 사용자에게 출력
* 브라우저가 코드를 이해해서 구현
* 어떤 종류의 텍스트를 어디에 쓰냐가 관건
* 3가지 종류의 텍스트(언어)가 있다.



## 2. HTML

**HyperText Markup Language**

* 브라우저에게 content가 무엇인지 알려준다
  * 타이틀, 링크, 리스트 등등
  * 어떻게 구성되어있는지
* Markup == Content



## 3. CSS

**Cascading Style Sheets**

* 브러우저에게 content가 어떻게 보여야하는지 알려준다.
  * 공백, 이미지, 링크의 효과 등
  * HTML과 같이 써야한다.
* 디자인과 스타일을 위한 언어

즉, HTML은 뼈대이고 CSS는 뼈대를 토대로 붙은 근육이라고 할 수 있다. CSS가 없다면 웹사이트는 썰렁하게 content만 나열된 텍스트처럼 보일 것 이다.



## 4. JavaScript

* 브라우저에게 Interactivity한 기능을 추가한다.
  * 애니메이션 효과 등
* 웹 프로그래밍 언어

단순한 웹 사이트는 HTML과 CSS로 충분하다. 하지만, 웹 사이트가 동적이며 상호작용하는 기능을 가지기 위해서는 JavaScirpt가 필요하다. 



## 5. 요약

각 세 가지 언어의 기능을 요약 하자면 다음과 같다.

> Contet를 위한 HTML (뼈대)
>
> Design을 위한 CSS(근육)
>
> Interactivity를 위한 JS(뇌)

하지만, 이 단계의 강의에선 JS를 많이 쓰지 않고 뼈(HTML)와 근육(CSS)만으로 보기 좋은 웹 사이트를 만들어 볼 것이다.



# Learning HTML

* 폴더명과 파일명은 소문자로
* **.html** 확장자 사용
* HTML을 잘 못 사용했더라도 브라우저는 언제나 컨텐츠를 보여줄 뿐 오류를 알려주지 않는다.
  * 개발자는 원인을 단번에 알기 어렵다



## 1. HTML tag

HTML은 tag문법을 사용한다.

><tag attrname= "atrrval"> content</tag>

* 올바른 위치에 올바른 태그를 사용하면 브라우저에 적용된다.
* 브라우저는 태그를 이해한다.
* 태그는 수도 없이 많다. 필요할 때마다 찾으면 되니, 원리만 이해하자.
  * mdn키워드(모질라)로 궁금한 태그를 검색하면 상세하게 나온다.
* 닫는 태그를 누락하면, 페이지 전체에 태그가 적용되어 버린다.
* 존재하지 않는 태그를 사용하더라도, 웹 브라우저는 content를 보여준다.
* 태그의 속성이 있다.
  * 필수적인 속성이 있을 수 있다.
  * 태그의 기능을 추가할 수 있다.



## 2. 리스트 tag

tag문법으로 순서있는 리스트와 순서없는 리스트를 만들 수 있다.

* **<ol></ol>** : ordered list

```html
<ol>
  <li>츄르</li>
  <li>간식</li>
  <li>고기</li>
</ol>
```

* **<ul></ul>** : unordered list

```html
<ul>
  <li>츄르</li>
  <li>간식</li>
  <li>고기</li>
</ul>
```



## 3.  Attributes

* 속성(Attributes)은 태그의 기능을 추가한다.
* 속성이 있어야만하는 태그도 있으며 태그마다 가지는 속성이 있다.
* 없는 속성은 브라우저가 알아보지 못한다.
* 공통 사용 속성도 있다.



### a tag

```html
<a href = "http://www.google.com" target="_blank">go to the google.com</a>
```

* **<a></a>** : 다른 웹사이트로 이동
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
* 이미지 주소에 인터넷의 링크나 local의 파일 주소를 올릴 수 있다.
  * 이미지의 경로를 주의할 것



## 4. HTML 문서의 구조

HTML으로 웹 페이지의 코드를 작성할 때, 따라야 하는 문서의 구조 규칙이 있다.

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

* **<!DOCTYPE html>** : 브라우저에게 text파일이 아니라 html인 것을 선언
* **<html>** : 이 태그 사이에 넣는 것이 html 코드라는 것을 표시
* **<head>** : 페이지 환경을 설정
  * 텍스트를 작성하면 안 된다. CSS 나 JavaScript와 오류를 낼 수 있다.
  * 이 위치의 태그들은 화면에 안 보인다.
* **<body>** : 사용자에게 보여질 태그들과 content를 넣는다.



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

* **<meta>** : 표현할 수 없는 다양한 종류의 메타데이터를 나타낸다. 메타는 부가적인 정보라는 뜻이다.
  * charset : text를 어떻게 보여줄지 말해준다. 한글이 있는 경우, **"utf-8"**을 입력해야 깨지지 않는다.
  * name, cotent 등의 속성을 사용해서, 검색 엔진에게 웹 사이트의 정보를 알려 준다.
  * self-closing tag
* **<html>**의 lang 속성 : 검색엔진에게 주된 사용 언어를 알려준다.
* **<link>** : 웹 브라우저에서 탭의 아이콘 이미지 설정
* **<head>** 태그는 웹 사이트가 무엇인지에 대한 설정과 정보를 웹 브라우저와 검색엔진에게 이해할 수 있도록 정리해준다.



## 6. form tag

form tag로 입력창을 만들 수 있다.

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

* **<form>** : 입력창을 만든다는 구획을 나타낸다.
* **<input>** : 입력창 생성, 다양한 속성으로 기능을 추가할 수 있다.
  * type : text, submit, file, password 등 다양한 속성을 주어 입력받을 형식 정할 수 있다.
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

* **<label>** : 사용자 인터페이스 항목(input)의 설명
  * for속성으로 input tag의 id를 가리킬 수 있다.



## 7. id 속성

* **<body>** 안에 있는 어느 tag에나 넣을 수 있는 속성
* unique identifier(고유 식별자)
* element당 하나의 id만 가질 수 있다.
* CSS가 가르키면서 디자인 할 수 있도록 한다.



## 8. Semantic HTML

HTML에서 지저분한 content를 정리하기 위해, `<div>` 태그를 사용해서 분할 할 수 있다. 그러나, `<div>`는 직관적으로 의미가 파악되기 어렵다. 반면, `<header>`는 같은 기능을 하지만, 좀 더 직관적으로 의미를 파악할 수 있다. 이렇게, 보기만 해도 그 의미를 짐작할 수 있는 것을 **semantic**이라고 한다.

| Semantic tag                                             | non-Semantic tag                   |
| :------------------------------------------------------- | ---------------------------------- |
| **<header>** 소개 및 탐색에 도움을 주는 content를 나타냄 | **<div>** division컨트롤 분할 요소 |
| **<footer>** 꼬리말                                      | **<span>** 짧은 text               |
| **<address>** 주소                                       |                                    |

* 이해하기 쉬운 html을 만들기 위해선, 같은 기능을 하더라도  Semanitc tag를 사용한다.



## 9. 요약

* HTML : 뼈대
  * tag를 브라우저가 이해하도록 작성
  * tag 열고 닫기에 유의
  * attribute
    * 큰 따옴표로 입력하기
    * 모든 tag가 가질 수 있는 속성이 있고 일부만 가지는 속성도 있다.
  * **<head>** 
    * 웹 사이트 설정을 담당하는 보이지 않는 tag들이 있는 곳
  * tag는 외울 필요가 없다. 필요할 때 검색하자.
  * Semantic tag로 작성하자
* CSS : 근육
* JavaScript : 뇌



## 느낀점

유튜브에서 항상 즐겨보던 노마드 코더의 니코선생님의 강의를 처음 들어보았다. HTML을 다시 복습해봤는데, 간단명료하고 필요한 것만 가르쳐주셔서 좋았다. 사이트와 커뮤니티도 잘 되어있어서 강의 마다 댓글을 보며 되뇌이는 것도 큰 도움이 되었다. CSS도 이어서 파이팅!!