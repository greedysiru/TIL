# 40장. 이벤트(3)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 40.8 DOM 요소의 기본 동작 조작

### 40.8.1 DOM 요소의 기본 동작 중단

* DOM 요소는 기본 동작이 있음
* preventDefault 메서드는 이 기본 동작을 중단 시킴



### 40.8.2 이벤트 전파 방직

* stopPropagation 메서드는 이벤트 전파를 중지시킴



## 40.9 이벤트 핸들러 내부의 this

* 이벤트 핸들러 어트리뷰트 방식의 이벤트 핸들러의 this는 전역 객체 window를 가리킴
* 이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식의 이벤트 핸들러 내부의 this는 이벤트를 바인딩한 DOM 요소를 가리킴
  * 이벤트 객체의 currentTarget 프로퍼티와 같음
  * 화살표 함수로 정의한 이벤트 핸들러의 내부 this는 상위 스코프의 this를 가짐
* 클래스 내부에 정의한 이벤트 핸들러의 경우 this가 인스턴스를 가리키지 않음에 주의
  * bind 메서드를 사용해 this를 전달하여 인스턴스를 가리키도록 해야 함
* 클래스 필드로 정의한 이벤트 핸들러는 this가 인스턴스를 가리키게 됨



## 40.10 이벤트 핸들러에 인수 전달

* 이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식의 경우 함수 호출이 브라우저가 하기 때문에 인수를 전달할 수 없음
  * 이벤트 핸들러 내부에서 함수를 호출하여 인수를 전달
  * 또는 이벤트 핸들러를 반환하는 함수를 호출하며 인수를 전달



## 40.10 커스텀 이벤트

### 40.11.1 커스텀 이벤트 생성

* 커스텀 이벤트 : 개발자의 의도로 생성된 이벤트
* 생성된 커스텀 이벤트 객체는 버블링 되지 않고 preventDefault 메서드로 취소할 수 없음
  * bubbles, cancelable 프로퍼티 값을 true로 설정하여 버블링이 일어나고 취소가 가능하도록 할 수 있음
* 커스텀 이벤트 객체를 생성하고 이벤트 핸들러 등록은 addEventListener 방식으로 이벤트 핸들러를 등록해야 함
  * 이벤트 핸들러 어트리뷰트/프로퍼티에 커스텀 이벤트가 존재하지 않기 때문

```JavaScript
const myEvent = new CustomEvent('myEvent'), {
  bubbles: true,
  cancelable: true,
};

console.log(myEvent.type); // myEvent
```



### 40.11.2 커스텀 이벤트 디스패치

* 생성한 커스텀 이벤트를 dispatchEvent 메서드로 디스패치 할 수 있음
* dispatch 매서드는 이벤트 핸들러를 동기 처리 방식으로 호출

```html
<html>
  <button class="btn">커스텀 이벤트 버튼</button>
</html>
<script>
	const $button = document.querySelector('.btn');
  
  // 커스텀 이벤트 생성
  const myEvent = new CustomEvent('myEvent', {
    detail: {message: '안녕'} // 이벤트 발생시 전달할 정보
  })
  
  // 버튼에 커스텀 이벤트 핸들러 등록
  // 커스텀 이벤트를 디스패치하기 전에 이벤트 핸들러를 등록해야 함
  $button.addEventListener('myEvent', e => {
    console.log(e.detail.message);
  })
  
  // 커스텀 이벤트 디스패치
  $button.dispatchEvent(myEvent);
</script>
```

