# [코드잇] jQuery 활용하기 (2) (2021.2.27)



**상세 내용 [블로그](https://greedysiru.tistory.com/233) 참고**



# 이벤트

## 01. 이벤트 객체 파라미터

```javascript
$('document').on('keydown', keyboardInput); // 이벤트 등록
function keyboardInput(e){
  console.log(e.key);
}
```

* 위와 같이 이벤트 등록 시, 이벤트 핸들러 함수를 호출하는 코드가 자바스크립트 내부에 이미 구현되어 있다.
* 함수 선언 시, 파라미터를 넣는 것만으로 이벤트 객체의 전달이 가능하다.



## 02. $(document).ready 와 익명함수

### ready 이벤트

* script 태그를 body 마지막 부분에 쓰는 이유
  * 코드는 위에서 아래로 읽히는데 모든 DOM 객체가 준비가 되야 하므로
* script 태그를 head 태그에 넣는 경우
  * **$(document).ready(function)**
  * document에 ready 이벤트를 등록한다.
  * 페이지 로딩이 끝나고 나서 함수를 실행한다.



### 익명함수

* 딱 한번 사용할 코드의 함수명을 생략할 수 있다.
* 이벤트 핸들링을 할 때 자주 사용

```javascript
$(document).ready(function() {
  console.log('hi');
})
```



# jQuery II

## 01. 요소 숨기기, 보여주기

### 숨기기

* 해당 요소를 숨길 수 있다.
  * display: none으로 설정

> **$('selector').hide();**



### 사라지게 하기

* 서서히 사라지는 효과를 넣는다.

> **$('selector').fadeOut(value);**

* value: 시간(ms)의 값을 넣는다.



### 보여주기

* 해당 요소를 보여줄 수 있다.

> **$('selector').show();**



### 나타나게 하기

* 서서히 나타나는 효과를 넣는다.

> **$('selector').fadeIn(value);**



## 02. 스크롤 I

* 스크롤을 이용한 기능을 만들 수 있다.



### scrollTop()

> **$(window).scrollTop();**

* 현재 창의 top의 위치를 리턴
* 파라미터를 입력시 해당 위치로 이동
  * 0을 입력하면, 웹 페이지의 최상단



### scroll event

> **$(window).on('scroll', eventhandler);**

* 스크롤 이벤트를 다룰 수 있다.



### 예시

```javascript
$(window).on('scroll', function(){
  $('.top').css('opacity', 1 - $(window).scrollTop() / $('.top').height());
})
```

* 클래스 top의 투명도를 바꾸는 이벤트 핸들러
* height(): 선택된 요소의 높이를 가져온다.
* 처음의 scrollTop은 0 이므로 opacity는 1이다.
* 스크롤을 할 수록 scrollTop이 커지므로 opacity가 작아진다
  * 스크롤을 할 수록 요소가 투명해지는 효과가 생긴다.



## 03. 스크롤 II

### animate()

> **$('selector').animate({scrollTop: y}, time);**

* **animate()**: 애니메이션 효과를 줄 수 있다.
* **{scrollTop:y}**: y위치로 스크롤 이동
* **time**: 이동하는데에 걸리는 시간



### 예시

```javascript
$('.go-to-top').on('click'. function(){
  $('html, body').animate({scrollTop: 0}, 500);
})
```

* .go-to-top이라는 요소를 누를 시, 맨위로 올라가는데 0.5 초의 애니메이션으로 이동



## 04. each

> **$('selector').each(function(){**
>
>   **block**
>
> **})**

* **유사배열의 각 요소에 대해서 함수를 실행**
* 조건문과 조합하여 원하는 요소에만 효과를 줄 수 있다.



## 05. 제이쿼리 애니메이션

### CSS 적용하기

```javascript
$("div").animate({left: '250px'});
```

* div태그가 left: 250px만큼 이동



### 여러 CSS 동시에 적용하기

```javascript
$("div").animate({left: '250px', opacity: '0.5'});
```

* div태그가 left: 250px 만큼 이동하면서 동시에 opacity: 0.5 가 적용



### 여러 CSS 순서대로 적용하기

```javascript
$("div").animate({left: '250px'});
$("div").animate({opacity: '0.5'});
```

* 작성한 순서대로 순차 적용



### CSS 반복 적용하기

```javascript
$("div").animate({left: '+=250px'});
```

* 코드가 실행될 때마다 div 태그가 left: 250px 만큼 계속해서 이동



### CSS 적용속도 조절하기

```javascript
$("div").animate({left: '250px'}, 1000);
```

* div태그가 left: 250px만큼  1000ms 동안 이동(1초)
* 세 번째 파라미터에 숫자뿐만 아니라 slow, fast로도 사용 가능



### 애니메이션 이펙트 적용하기

 ```javascript
$("div").animate({left: '250px'}, 1000, 'easeOutElastic');
 ```

* div태그가 left: 250px만큼 1초 동안 이동하되, easeOutElastic 효과가 적용
* **Easing**: 애니메이션 이펙트들
  * linear, swing, easeInBounce 등이 있음
  * Easing을 사용하기 위해서 아래의 jQueryUI 코드도 추가해야함.
  *  [링크](https://code.jquery.com/ui/)



# Reference

[코드잇 - jQuery 활용하기](https://www.codeit.kr/courses/jquery/topics/making-use-of-jquery)

