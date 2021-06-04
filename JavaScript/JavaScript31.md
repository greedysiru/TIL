# [드림코딩 by 엘리] JavaScript 기초 강의(1) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/501) 참고**

## console

```JavaScript
console.log('Hello World');
```

* **console: WEB API 중 하나**
  * Appication Programming Interface
  * Node.js , 브라우저에서 사용 가능
  * **브라우저가 제공하는 함수**



## JavaScript의 공식사이트

**developer.mozilla.org**



## async vs defer

### header 태그에 script태그를 넣은 경우

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src='main.js'></script>
</head>
<body>
</body>
</html>
```

| parsing HTML | blocked                   | parsing HTML | -> Page is ready |
| ------------ | ------------------------- | ------------ | ---------------- |
|              | fetching js / excuting js |              |                  |

* parsing HTML
  * 사용자가 HTML 파일을 다운로드 받았을 때, **브라우저가 한 줄씩 분석한다.**
  * 그 후 이해한 것을 CSS와 병합해서 **DOM 요소로 변환한다.**
  * 도중에, script 태그가 보이면, parsing HTML을 멈추고 필요한 js파일을 서버에서 다운 받아 실행한 다음 다시 parsing을 실행한다.
  * **단점**: js 파일의 크기가 크고, 인터넷이 느리다면 사용자가 웹 사이트를 보기까지 많은 시간이 소요될 것이다.
    * script를 header에 포함하는 것은 좋은 방법이 아니다.



### 대안 - body태그 마지막에 넣기

* body 태그 마지막에 script태그를 넣기

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div> 
  </div>
  <script src='main.js'></script>
</body>
</html>
```

| parsing HTML | -> page is ready | fetching js | executing js |
| ------------ | ---------------- | ----------- | ------------ |

* 브라우저가 parsing을 한 후 서버에서 js파일을 받아오고 실행하게 된다.
* 사용자가 기본적인 HTML 컨텐츠를 빨리 볼 수 있다.
* **단점**: 웹사이트가 JavaScript에 의존적인 경우, 의미있는 컨텐츠를 보기 위해 fetching, executing을 기다려야 한다.



### 대안 - async

* script태그에 async 속성 사용하기
* async는 boolean

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script async src='main.js'></script>
</head>
<body>
</body>
</html>
```

| parsing HTML | blocked      | parsing HTML | -> page is ready |
| ------------ | ------------ | ------------ | ---------------- |
| fetching js  | executing js |              |                  |

* parsing과 동시에 js파일을 병렬로 다운로드
* 다운로드를 다 받게 되면, js를 실행
* fetching이 병렬적으로 일어나므로 다운로드 시간을 절약할 수 있다.
* **단점**
  * js에서 dom요소 조작시, 원하는 요소가 정의되어 있지 않을 수 있다.(HTML parsing이 끝나지 않았으므로)
  * js 파일이 다수인 경우, 정의된 순서가 아니라 다운로드가 된 순서대로 실행한다. js가 순서 의존적이라면, 문제가 발생할 수 있음
  * 여전히 페이지를 보는데에 시간이 걸린다.



### 대안 - defer

* script 태그에 defer 속성 사용하기

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script defer src='main.js'></script>
</head>
<body>
</body>
</html>
```

| parsing HTML | -> page is ready | executing js |
| ------------ | ---------------- | ------------ |
| fetching js  |                  |              |

* js 파일을 병렬적으로 다운로드 받음
* parsing이 완전히 끝난 다음에 js 파일을 실행
* parsing을 하는 동안 필요한 js 파일들을 다운로드 받은 후, 정의된 순서대로 실행한다.
* **가장 좋은 옵션**



## use strict

* JavaScript 사용시, 제일 윗 부분에 정의
* TypeScript 사용시, 선언할 필요 없음

```JavaScript
'use strict'

console.log('Hello world');
```

* JavaScript 언어를 만들 때, 굉장히 유연하게 설계 됨

  * 때로는 위험을 야기
  * 선언되지 않은 변수의 값을 할당, 프로토 타입을 변경할 수 있음 -> 비상식적

* use strict를 선언하면 위험을 방지할 수 있음

  * ECMAScript 5에서 추가

* scrict mode에서 개발하는 것을 권장

  * 오류 방지 및 성능 개선

  

# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)

