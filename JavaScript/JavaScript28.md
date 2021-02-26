# [코드잇] jQuery 시작하기  (2021.2.26)



**상세 내용 [블로그](https://greedysiru.tistory.com/230) 참고**



# jQuery

## 01. jQuery

* JavaScript를 간단하게 사용할 수 있게하는 라이브러리



### 적용하기

#### 1. jQuery CDN

```javascript
<script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
```



#### 2. jQuery 코드 다운로드

[jQuery 사이트](https://jquery.com/)

다운로드 후, 아래를 코드 입력

```html
<script src="파일 경로"></script>
```



### 문법

> **$('selector').attr('property', 'property value');**
>
> **$('selector').css('property', 'property value');**

* **attr**: 속성을 바꾸는 메소드
  * 첫 번째 파라미터: 속성
  * 두 번째 파라미터: 속성값
* **css**: style을 설정하는 메소드
  * 첫 번째 파라미터: 속성
  * 두 번째 파라미터: 속성값



## 02. 이벤트

* HTML 요소들에게 일어날 수 있는 일들
  * 요소를 클릭
  * 페이지 로딩이 끝남
  * 키보드를 입력
  * 마우스의 이동
* **Event Handling(이벤트 핸들링)**: 이벤트에 따른 동작이 일어나도록 코드를 작성할 수 있다.
  * 링크를 클릭하면(이벤트) 사진이 바뀐다.(이벤트 핸들링)
* **Event Handler(이벤트 핸들러)**: 이벤트 핸들링을 실행하는 함수



## 03. 이벤트 핸들링

### on

> **$('selector').on('event', eventhandler);**

* **on**: 이벤트를 이벤트 핸들러 함수에게 넘겨주는 메소드
  * 첫 번째 파라미터: event
  * 두 번째 파라미터: event handler, 괄호는 생략



## 04. 키보드 이벤트

>**$(document).on('keydown', eventhandler);**

* 키보드는 특정 요소를 선택하는 것이 아니라 문서 전체에서 일어나는 것이므로 document(문서 전체)를 쓴다.
* 그 결과 페이지 전체에 이벤트 핸들링을 등록



## 05. 여러 메소드

* **addClass()**:클래스 이름을 추가
* **removeClass()**: 클래스 삭제



# Audio 객체

* Audio 객체를 사용하여 소리를 재생할 수 있다.

## 01. 소리 재생하고 정지하기

* Audio 객체와 메소드를 사용하여 재생, 정지를 할 수 있다.

 ```javascript
var audioFile = new Audio("file location or url"); // Audio 객체 생성
audioFile.play(); // 재생
audioFile.pause(); // 정지
 ```



## 02. 사이트에 소리 입히기

```html
<!DOCTYPE html>
<html>
<head>
  <title>Audio Player</title>
  <meta charset="utf-8" />
  <link href="css/styles.css" rel="stylesheet" />
</head>
<body>

<button id="playBtn">Music Start</button> <!-- 재생 버튼 -->
<button id="stopBtn">STOP</button>        <!-- 정지 버튼 -->

<script
  src="https://code.jquery.com/jquery-3.2.1.min.js"
  integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4="
  crossorigin="anonymous"></script> <!-- 제이쿼리 가져오기 -->

<script> 
var audioFile = new Audio("https://d34x6xks9kc6p2.cloudfront.net/540997b0-a35f-4b69-86d6-b1c925c4a264/540997b0-a35f-4b69-86d6-b1c925c4a264.mp3"); // Audio 객체

function playMusic() { // 재생 버튼 함수
    audioFile.play(); 
}

function stopMusic() { // 정지 버튼 함수
    audioFile.pause();
}

$('#playBtn').on('click', playMusic);  // 이벤트 핸들러 등록
$('#stopBtn').on('click', stopMusic);
</script> 
</body>
</html>
```



## 03. 처음부터 재생하기

* 처음부터 재생하는 기능을 만들 수 있다.
* **아래의 코드를 stopMusic(); 함수에 추가한다.**

```javascript
audioFile.currentTime = 0; // 오디오 파일 재생 위치 설정
```



# 세련된 코드

## 01. 스타일 가이드

* **어떤 방식과 스타일로 코딩을 하는 게 좋을 지 정해주는 역할을 한다.**
  * 띄어쓰기와 줄바꿈
  * 변수 이름을 짓는 규칙
  * 동작은 하지만 쓰지 말아야 할 코드
  * 그 외 등등
* 스타일이 잘 갖추어진 코드는 가독성이 높고, 유지 보수 및 재사용성이 높아지며 버그를 줄일 수 있는 안정적이 코드가 된다.



## 02. 작명

* 보기에 좋아야 한다.
  * 너무 긴 이름은 지양하기
* 이해하기 쉬워야 한다.
  * ex. 불린타입의 변수는 isXxxxx 와 같이 짓는다.
* 실수를 유발하지 않아야 한다.
  * ex. isNotZero 처럼 부정적 의미의 변수 이름은 지양



## 03 . Boolean의 활용

### undefined 와 null

* **undefined**: 변수에 아무것도 할당되지 않았을 때
* **null**: 비어있는 값



### NaN

* Not a Number
* 숫자가 아닌 것을 숫자로 표현하려 할 때 반환



### Boolean으로 반환되는 것들

* 숫자

  * 0: false
  * 양수, 음수:  true

* 문자열

  * 비어있는 문자열: false
  * 문자열: true

* null, undefined, NaN

  * false

  

# Reference

[코드잇 - jQuery 시작하기](https://www.codeit.kr/courses/jquery/topics/getting-started-with-jquery)

