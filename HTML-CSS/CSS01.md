# [생활코딩] WEB2-CSS (2020.11.30~12.1)  

**상세 내용 [블로그](https://greedysiru.tistory.com/4?category=860706)**

## CSS  
HTML의 태그 문법의 비효율과 디자인 요소의 부족으로 CSS(Cascading Style Sheets)등장
## CSS의 장점
  > 디자인 기능  
  > 반복작업의 효율성  
## CSS 문법
  1. `<head></head>` 사이에 `<style></style>`입력  
  2. `<style></style>` 사이에 입력

    ```html
    <head>
        <style>
            a{
                color:red;
            }
        </style>
    <head>
    ```  
  3. a는 선택자, color:red는 효과(선언)  
## 선택자의 지정  
```html
<a href="링크" id="active"> 내용 </a>
```
태그의 속성 안에 `id="active"`라는 선택자를 지정할 수 있다.  
선택자의 속성 부여는 아래와 같다.
```html
#active { 
    color:red
}
```
## 선택자 우선순위  
id,class,tag  

## 인라인과 블록
    >인라인: 화면 전체 적용
    >블록: 태그 부변만 적용

## 박스 모델
![CSS1-1](./images/CSS1-1.jpg)

웹 브라우저의 소스보기 기능으로 해당하는 부분의 속성을 조절할 수 있다.

## 코드 줄이기
```css
h1, a {border-width:5px;border-color:red;border-style: solid}
```
선택자는 컴마, 속성은 세미콜론으로 줄인다.

## 그리드
```html
<head>
    <style>
        #grid{ 
            display: grid; grid-template-columns: 150px 1fr; 
            }
    </style>
</head>
 
<body>
 
<div id="grid">

그리드

<div id="article">

그리드

</div>

</div>

 
</body>
```
## 미디어 쿼리
사용자의 환경에 상호작용 가능
```css
@media(min-width:800px) {
        div{
          display:none;
        }
        }
```
`@media`뒤의 괄호는 조건 `{}`에는 출력을 쓴다.
## CSS 링크하기
확장자가 .css인 파일을 만들고 링크할 수 있다.
```html
<link rel="stylesheet" href="style.css">
```
## 명령어 정리
`<font color="red"></font>` : 폰트 색상  
`<!-- -->` : 주석  
`<style></style>` : CSS 태그  
`{color:red}` : 색상  
`{text-decoration: none;}` : 글자 효괴 지우기, -underline: 및줄  
`{border-width:5px}` : 경계선  
`*/ */` : css 주석




# Reference
https://www.dummies.com/web-design-development/site-development/how-to-work-with-the-basic-box-model-in-css3/