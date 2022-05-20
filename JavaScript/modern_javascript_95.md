# 43장. Ajax(2)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 43.3 XMLHttpRequest

* 자바스크립트를 사용하여 HTTP 요청을 전송할 수 있는 객체
* Web API
* HTTP 요청 전송, HTTP 응답 수신을 위한 메세드 제공



### 43.3.1 XMLHttpRequest 객체 생성

* XMLHttpRequest 생성자 함수를 호출하여 생성
* Web API이므로 브라우저 환경에서만 정상 실행

```JavaScript
const xhr = new XMLHttpRequest();
```



### 43.3.2 HTTP 요청 전송

1. XMLHttpRequest.prototype.open 메서드로 HTTP 요청을 초기화
2. XMLHttpRequest.prototype.setRequestHeader 메서드로 HTTP 요청 헤더 값을 설정
3. XMLHttpRequest.prototye.send 메서드로 HTTP 요청을 전송

```JavaScript
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
// 1. Http Mothod, 2. 요청 url
xhr.open('GET', '/cats');

// HTTP 요청 헤더 설정
xhr.setRequestHeader('content-type', 'application/json');

// HTTP 요청 전송
xhr.send();
```



## 43.3.4 HTTP 응답 처리

* XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 함
* 서버의 응답이 클라이언트에 언제 도달하는지는 알 수 없음
* readystatechange 이벤트를 통해 요청의 현재 상태 확인
  * HTTP 요청의 현재 상태를 나타내는 readyState 프로퍼티가 변경될 때마다 발생
  * 이벤트 핸들러를 할당하여 readyState가 DONE인지 확인
* 서버의 응답이 완료되면 응답 상태가 200인지 확인하여 정상처리와 에러처리를 구분
* load 이벤트를 사용하는 경우 readyState가 DONE인지 확인하지 않아도 됨

```JavaScript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://siru.com/cats');
xhr.send();

xhr.onload = () => {
  
  if (xhr.status === 200) {
    console.log('성공');
  } else {
    console.log('실패');
  }
}
```

