# [코드잇] jQuery 활용하기 (1) (2021.2.26)



**상세 내용 [블로그](https://greedysiru.tistory.com/232?category=860707) 참고**



# jQuery I

## 01. DOM pt.1

* **문서 객체 모델(Document Object Model, DOM)**
* 브라우저가 HTML 문서를 정리하여 **객체**로 만들고 보여준다.
* 태그의 **부모 - 자식 관계**로 객체가 만들어짐



## 02. DOM pt.2

* **Document**: 최상위 객체
  * DOM 트리에 접근을 가능하게 한다.
  * 메소드를 이용하여 객체 접근



## 03. jQuery 사용해보기

> **$('selector').method();**

* **dot(.)**을 기준으로 두 부분으로 나눌 수 있다.
* **selector**: 요소를 **선택**하는 부분
  * **CSS의 선택자**
  * 태그 명
  * 가상 클래스와 같은 복잡한 선택자도 가능
* **method**: 요소에 대해 **동작**하는 부분



## 04. jQuery 내부 살펴보기

* jQuery는 **JavaScript의 라이브러리**이다.
  * 여러가지의 함수와 변수가 정의되어 있는 자바스크립트 파일
* **$**: 함수 이름
  * 리턴하는 값: **jQuery 객체**
* jQuery 객체
  * 배열 비슷한 것
  * DOM 관련 **함수**들을 사용할 수 있다.



## 05. jQuery의 동작

### 클래스 관련

* **.addClass()**: 클래스 추가
* .**removeClass()**: 클래스 제거
* **.toggleClass()**: 파라미터와 같은 클래스가 있으면 제거, 없으면 추가
* **.hasClass()**: 파리미터와 같은 클래스가 있으면 true, 없으면 false 리턴



### 속성 관련

* **.attr()**: 파라미터와 같은 속성 받아오기
  * 첫 번째 파라미터: 속성명
  * 두 번째 파라미터: 속성값 지정
* **.text()**: 텍스트 받아오기
  * 파라미터 입력 시: 텍스트 지정하기
* **.html()**: HTML 텍스트 지정하기



### 스타일 관련

* **.css()**: CSS 설정 부여
  * 첫 번째 파라미터: css 속성
  * 두 번째 파라미터: css 속성값
  * 파라미터 하나만 입력 시, 해당 속성 값을 가져온다.



## 06. 요소 추가하기

### 형제 요소 추가하기

> **$('selector').after('element');**
>
> **$('selector').before('element');**

* **.after()**: 해당 선택자 뒤에 요소를 추가한다.
* **.before()**: 해당 선택자 앞에 요소를 추가한다.



### 자식 요소 추가하기

> **$('selector').append('element');**
>
> **$('selector').prepend('element');**

* **.append()** : 마지막 자식으로 요소를 추가한다.
* **.prepend()**: 첫 번째 자식으로 요소를 추가한다.



## 07. 따옴표 주의사항

* 따옴표 안에 따옴표의 종류가 겹치지 않도록 주의한다.
  * 겹치는 종류의 따옴표를 안과 밖에 중복해서 사용하면, 오류가 발생한다.
  * 써야하는 경우, 백슬래시를 사용하면 된다.

```javascript
$('ul li:first-child').before('<li class="item">어떤 요소</li>');
// 정상적으로 작동
$('ul li:first-child').before('<li class=\'item\'>어떤 요소</li>');
// 정상적으로 작동
```



## 08. 요소 이동과 삭제

### 요소 이동

> **$('selector').before('elementToMove');**
>
> **$('selector').after('elementToMove');**
>
> **$('selector').append('elementToMove');**
>
> **$('selector').prepend('elementToMove');**

* 원래 있는 요소를 메소드에 따라 원하는 위치로 이동할 수 있다.
* **elementToMove**: 옮길 요소. 클래스나 아이디가 올 수도 있다.



### 요소 삭제

> **$('selector').remove();**



## 09. 더 선택하기

* jQuery에서 제공하는 선택 방법



### filter

* 괄호 안의 조건으로 선택된 요소를 한번 더 **걸러준다.**

```javascript
$('button').filter('.color-3').text('SELECTED!');
// 모든 button 태그 중에 color-3이라는 클래스를 가지고 있는 요소만 추려내서 text를 바꾼다.
```



### not

*  선택된 요소 중에서 조건에 해당되는 것을 **제외한다.**

```javascript
$('button').not('.color-3').text('SELECTED!');
// 모든 button 태그 중에 color-3이라는 클래스를 가지고 있는 요소를 제외하고 text를 바꾼다.
```



### eq

* 선택된 요소들 중에서 **n번째 요소** 하나만 골라낸다.
* 0부터 시작한다.

```javascript
$('button').eq(1).text('SELECTED!');
// 모든 button 태그 중에 두 번째 요소만 골라서 text를 바꾼다.
```



### parent

* **부모 요소**를 찾아준다.

```javascript
$('button').parent().css('background-color', 'black');
// button의 부모요소를 찾아서 css를 적용한다.
```



###  children

* **자녀 요소**를 모두 고른다.
* 파라미터를 전달하면, filter역할도 함께 한다.

```javascript
$('body').children().css('background-color', 'black');
// body의 모든 자녀 요소를 찾아서 css를 적용한다.
```



### find

* 파라미터로 전달받은 조건에 맞는 자신 아래의 자녀 요소들을 모두 찾아낸다.

```javascript
$('#box-1').find('.color-2').css('background-color', 'black');
// box-1의 자녀 요소 중 color-2가 있는 요소의 css를 적용
```



### siblings

* 선택된 요소의 **이웃 요소**들을 골라준다.

```javascript
$('#btn-1').siblings().text('SELECTED!');
// btn-1의 모든 이웃 요소의 text를 변경
```

# Reference

[코드잇 - jQuery 활용하기](https://www.codeit.kr/courses/jquery/topics/making-use-of-jquery)

