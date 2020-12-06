# [생활코딩] WEB2-CSS (2020.11.30~12.1)  

**상세 내용 [블로그](https://greedysiru.tistory.com/4?category=860706)**
  
* ## CSS  
HTML의 태그 문법의 비효율과 디자인 요소의 부족으로 CSS(Cascading Style Sheets)등장
* ## CSS의 장점
  > 디자인 기능  
  > 반복작업의 효율성  
* ## CSS 문법
  1. `<head></head>` 사이에 `<style></style>`입력  
  1. `<style></style>` 사이에 입력
    ```html
    <head>
        <style>
            a{
                color:red;
            }
        </style>
    <head>
    ```  
  1. a는 선택자, color:red는 효과(선언)  
* ## 선택자의 지정  
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
* ## 선택자 우선순위  
id,class,tag  

* ## 인라인과 블록
    >인라인: 화면 전체 적용
    >블록: 태그 부변만 적용

* ## 박스 모델
![Boxmodel](/ETC/images/Boxmodel.jpg)
웹 브라우저의 소스보기 기능으로 해당하는 부분의 속성을 조절할 수 있다.

* ## 코드 줄이기
```css
h1, a {border-width:5px;border-color:red;border-style: solid}
```
선택자는 컴마로 구분, 속성은 세미콜론



# Reference
https://www.dummies.com/web-design-development/site-development/how-to-work-with-the-basic-box-model-in-css3/