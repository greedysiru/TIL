# [코드잇] 인터랙티브 자바스크립트 (4) (2021.2.24)



**상세 내용 [블로그](https://greedysiru.tistory.com/226) 참고**



# 다양한 이벤트 알아보기

## 01. 마우스 버튼 이벤트

### MouseEvent.button

* **0**: 마우스 왼쪽 버튼
* **1**: 마우스 휠
* **2**: 마우스 오른쪽 버튼
* **3**: X1 (일반적으로 브라우저 뒤로 가기 버튼)
* **4**: X2 (일반적으로 브라우저 앞으로 가기 버튼)
* 노트북의 경우: **0, 2**만 있음
* **마우스 이동과 관련된 이벤트에서는 이 값이 0이다.**



### MouseEvent.type

* **click**: 마우스 왼쪽 버튼
* **contextmenu**: 마우스 오른쪽 버튼
* **dbclick**: 동일한 위치에서 빠르게 두번 click할 때
* **mousedown**: 마우스 버튼을 누른 순간
* **mouseup**: 마우스 버튼을 눌렀다 뗀 순간
* 한 동작에 두 개 이상의 이벤트가 발생할 수 있다.
  * 더블클릭의 경우
  * mousedown -> mouseup -> click -> mousedown -> mouseup -> click -> dbclick
  * 예상치 못한 동작이 발생할 수 있으니 주의
* 마우스 오른쪽 버튼은 이벤트 발생순서가 운영체제별로 달라질 수 있다.
  * 윈도우: mousedown -> mouseup -> contextmenu
  * 맥: mousedown -> context menu (-> mouseup : 오른쪽 클릭 preventDefault()로 없앴을 때)



## 02. 마우스 이동 이벤트 I

* 마우스가 이동할 때 발생하는 이벤트에는 위치와 관련된 이벤트 객체의 프로퍼티들이 자주 활용



### 위치와 관련된 이벤트 프로퍼티

* **MouseEvent.clientX, clientY**
  * **화면에 표시되는 창 기준** 마우스 포인터 위치
  * **클라이언트 영역**: 이벤트가 발생한 순간에 브라우저가 콘텐츠를 표시할 수 있는 영역
  * 항상 보여지는 좌측 상단의 모서리의 위치: (0, 0)
* **MouseEvent.pageX, pageY**
  * **웹 문서 전체 기준** 마우스 포인터 위치
  * 스크롤로 인해서 보이지 않게된 화면의 영역가지 포함해서 측정
* **MouseEvent.offsetX, offsetY**
  * 이벤트가 발생한 **요소 기준** 마우스 포인터 위치
  * 요소의 좌측 상단의 모서리 위치: (0, 0)
* **MouseEvent.screenX, screenY**
  * **마우스 포인터**의 모니터 화면 영역에서의 위치
* 특정한 위치에 도달했을 때 동작이 일어나도록 할 수 있다.
* 연속적으로 발생한 이벤트 위치값을 계산하여 마우스의 이동경로를 파악할 수 있다.



## 03. 마우스 이동 이벤트 II

### MouseEvent.type

* **mousemove**: 마우스 포인터가 이동할 때
* **mouseover**: 마우스 포인터가 요소 밖에서 안으로 이동할 때
* **mouseout**: 마우스 포인터가 요소 안에서 밖으로 이동할 때
* **relatedTarget**: 이벤트가 발생하기 직전(또는 직후)에 마우스가 위치해 있던 요소
  * 이를 응용하여 마우스의 요소간 이동경로를 파악할 수 있다.
* **mouseenter**: 마우스 포인터가 요소 바깥에서 안쪽으로 들어갈 때
  * 버블링이 일어나지 않는다.
  * 자식 요소의 영역을 계산하지 않는다.
* **mouseleave**: 마우스 포인터가 요소 안쪽에서 바깥으로 나갈 때
  * 버블링이 일어나지 않는다.
  * 자식 요소의 영역을 계산하지 않는다.



### MouseEvent.relatedTarget

* **mouseenter, mouseleave, mouseover, mouseout** 이벤트에 존재하는 프로퍼티
* **이벤트가 발생하기 직전(또는 직후)에 마우스가 위치해 있던 요소를 담고 있다.**



## 04. 키보드 이벤트

### KeyboardEvent.type

* **keydown**: 키보드 버튼을 누른 순간
  * 기능적인 키에서도 발생한다.
  * 연속 입력을 감지한다.
* **keypress**: 키보드 버튼을 누른 순간
  * 출력값이 변하는 키에서만 발생
  * 연속 입력을 감지하지 못한다.
  * 영어 외 언어를 감지하지 못한다.
  * 웹 표준에서 권장하지 않는다.
* **keyup**: 키보드 버튼을 눌렀다 뗀 순간



### KeyboardEvent 프로퍼티

* **.key**: 이벤트가 발생한 버튼의 값
  * 대소문자를 구분한다.
  * 오른쪽, 왼쪽 shift 같은 경우는 구분하지 않는다.
* **.code**: 이벤트가 발생한 버튼의 키보드에서 물리적인 위치
  * 대소문자를 구분하지 않는다.
  * 오른쪽, 왼쪽 shift 같은 경우는 구분한다.



## 05. input 태그 다루기

* input태그는 다양한 type을 가진다.
  * 입력의 역할을 한다.
  * 사용자의 키보드, 마우스 동작에 반응
* text, password, button, checkbox ...



### 포커스 이벤트

*  **input태그가 사용자의 동작에 반응할 준비가 된 상태**
* **focusin**: 요소에 포커스가 되었을 때
* **focusout**: 요소에 포커스가 빠져나갈 때
* **focus**: 요소에 포커스가 되었을 때 (버블링 x)
* **blur**: 요소에 포커스가 빠져나갈 때 (버블링 x)



### focus, blur

*  버블링을 하지 않기 때문에 이벤트 위임을 활용할 수 없다.
* **구체적으로 input 태그를 가리켜야 이벤드 핸들러를 사용할 수 있다.**



### 입력 이벤트

* **input**: 사용자가 입력을 할 때
  * 기능키에서는 이벤트가 발생하지 않는다.
* **change**: 요소의 값이 변했을 때
  * **입력이 시작되기 전 값과 완료 되었을 때 값 사이에 차이가 있을 때 발생**
  * focusout 직전에 값이 변했을 때 발생
  * 입력 후 엔터키를 누를 때도 발생
* **select**: 입력 양식의 하나가 선택되는 순간
* **submit**: 폼을 전송하는 순간



## 06. 스크롤 이벤트

* **브라우저를 대변하는 window에 이벤트 핸들러를 등록**
* window 객체의 프로퍼티 활용
  * **scrollY**: 스크롤이 발생했을 때 웹문서의 제일 위쪽에서부터 몇 픽셀을 스크롤 했는지 알 수 있다. 



### 예시

```javascript
// Scroll 이벤트
let lastScrollY = 0;

function onSroll() {
  const nav = document.querySelector('#nav');
  const toTop = document.querySelector('#to-top');
  const STANDARD = 30;
  
  if (window.scrollY > STANDARD) { // 스크롤이 30px을 넘었을 때
    nav.classList.add('shadow');
    toTop.classList.add('show');
  } else { // 스크롤이 30px을 넘지 않을 때
    nav.classList.remove('shadow');
    toTop.classList.remove('show');
  } 

	if (window.scrollY > lastScrollY) { // 스크롤 방향이 아랫쪽 일 때
    nav.classList.add('lift-up');
  } else { // 스크롤 방향이 윗쪽 일 때
    nav.classList.remove('lift-up');
  }

  lastScrollY = window.scrollY;
}

window.addEventListener('scroll', onSroll);
```



# Reference

[코드잇 - 인터랙티브 자바스크립트](https://www.codeit.kr/courses/javascript-intermediate/topics/interactive-javascript)