# 40장. 이벤트(1)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 40.1 이벤트 드리븐 프로그래밍

* 브라우저는 특정 사건이 발생하면 이를 감지하여 이벤트를 발생 시킴
  * 클릭, 키보드 입력, 마우스 이동, 드래그
* 이벤트가 발생했을 때 호출될 함수를 브라우저에게 알려 호출을 위임
  * 이벤트 핸들러 : 호출될 함수
  * 이벤트 핸들러 등록 : 이벤트가 발생했을 때 이벤트 핸들러의 호출을 위임
* Window, Document, HTMLElement 타입의 객체는 다양한 이벤트 핸들러 프로퍼티를 가지고 있음
* 이벤트 드리븐 프로그래밍 : 프로그램의 흐름을 이벤트 중심으로 제어하는 프로그래밍 방식



## 40.2 이벤트 타입

* 이벤트의 종류를 나타내는 문자열
* 약 200여 가지가 있음
* MDN Event reference에서 참고하기



## 40.3 이벤트 핸들러 등록

* 이벤트 발생 시, 브라우저 호출을 위임한 함수



### 40.3.1 이벤트 핸들러 어트리뷰트 방식

* HTML 요소의 어트리뷰트의 이벤트 핸들러 어트리뷰트에 이벤트 핸들러를 등록
  * on접두사와 이벤트 종류를 나타내는 이벤트 타입으로 이루어져 있음
* 값으로 이벤트 핸들러로 등록할 함수 호출문 등의 문을 할당
  * 함수 참조가 아님에 주의
* 이벤트 핸들러 어트리뷰트의 값은 암묵적으로 생성될 이벤트 핸들러의 함수 몸체를 의미
  * 이벤트 핸들러에 인수를 전달하기 위함
* 여러개의 문을 할당할 수 있음
* CBD(Component Based Development)방식의 React.js와 같은 라이브러리에서 이와 유사한 방식으로 이벤트 핸들러를 처리

```HTML
...
<button onclick="sayHello('안녕'); cry('야옹');">
  야옹
</button>
...
<script>
  function sayHello(str) {
    console.log(str);
  }
	function cry(str) {
    console.log(`나는 ${str}라고 울어`);
  }
</script>
```



### 40.3.2 이벤트 핸들러 프로퍼티 방식

* window 객체, Document, HTMLElement 타입의 DOM 노드 객체는 이벤트에 대응하는 이벤트 핸들러 프로퍼티를 가지고 있음
  * 프로퍼티의 키는 on 접두사와 이벤트 타입으로 이루어져 있음
* 이벤트 타킷, 이벤트 타입, 이벤트 핸들러를 지정해야 함
* DOM 노드 객체의 이벤트 핸들러 프로퍼티로 변환
* HTML과 JavaScript의 분리를 가능하게 함
* 이벤트 핸들러를 하나만 바인딩할 수 있는 것이 단점

```HTML
<script>
	const $button = document.querySelector('button');
  // $button: 이벤트 타깃
  // onclick: 이벤트 타입
  // function~ : 이벤트 핸들러
  $button.onclick = function() {
    console.log('click');
  };
</script>
```



### 40.3.3 addEventListener 방식

* DOM Level 2에서 도입
* 이벤트 타입은 on 접두사가 필요 없음
* 마지막 매개변수에 이벤트 전파 단계를 지정 가능
  * true를 지정하면 캡처링 단계에서 이벤트를 캐치
* addEventListener 방식은 이벤트 핸들러 프로퍼티에 바인딩된 이벤트 핸들러에 영향을 주지 않음
  * 두 개를 바인딩하면, 두 개 이벤트 핸들러가 호출 됨
* 참조가 동일한 이벤트 핸들러를 중복 등록하면, 하나의 이벤트 핸들러만 등록 됨

> EventTarget.addEventListener('eventType', functionName [, useCapture]);

```HTML
...
<script>
	const $button = document.querySelector('button');
  $button.addEventListener('click', function () {
    console.log('button click');
  });
</script>
```



## 40.4 이벤트 핸들러 제거

* addEventListener
  * EventTarget.prototype.removeEventListener 메서드를 사용
  * 등록한 이벤트 타입과 함께 이벤트 핸들러를 전달
* 동일한 함수여야 함
* 무명 함수의 경우 제거 불가능
* 이벤트 핸들러 프로퍼티의 경우 null을 할당하여 제

```HTML
...
<script>
	const $button = document.querySelector('button');
  
  const clickEvent = () => console.log('click!');
  
  // 이벤트 핸들러 등록
  $button.addEventListener('click', clickEvent);
  
  // 이벤트 핸들러 제거
  $button.removeEventListener('click', clickEvent);
</script>
```

