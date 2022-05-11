# 39장. DOM(4)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 39.6 DOM 조작

* 새로운 노드르 생성하여 DOM에 추가하거나 기존 노드를 삭제 또는 교체
  * 리플로우와 리페인트가 발생하므로 성능 영향



### 39.6.1 innerHTML

* Element.prototype.innerHTML
  * setter, getter 모두 존재하는 접근자 프로퍼티
* 요소 노드의 HTML 마크업을 취득하거나 변경
  * 요소 노드의 콘텐츠 영역(시작 태그 ~ 종료 태그)에 포함된 HTML 마크업을 문자열로 반환
* 문자열 할당 시 HTML 마크업을 파싱하여 자식 노드로 DOM에 반영
  * 모든 자식 노드를 제거하고 할당한 것으로 DOM을 변경
* 사용자로부터 입력 받은 데이터를 그대로 innerHTML프로퍼티에 할당하는 것은 크로스 사이트 스크립팅 공격에 취약
  * 마크업 내에 악성 자바스크립트 코드를 파싱 과정에서 그대로 실행할 가능성이 있음
  * HTML5는 자바스크립트 코드를 실행하지 않음
  * script 요소 없이도 크로스 사이트 스크립트 공격에 취약므로 주의
  * HTML 새니티제이션: 크로스 사이트 스크립팅 공격을 예방하기 위해 잠재적 위험을 제거하는 기능
* 삽입될 위치 지정 불가
* 복잡하지 않은 요소를 새롭게 추가할 때는 유용하지만, 기존 요소를 유지하여 추가하거나 위치를 지정해야할 때는 좋지 않음



### 39.6.2 insertAdjacentHTML 메서드

* 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소 삽입
* 첫 번째 인수로 전달한 위치에 두 번째 인수로 전달한 HTML 마크업 문자열을 파싱하여 추가
* 첫 번째 인수로 올 수 있는 문자열
  * beforebegin
  * afterbegin
  * beforeend
  * afterend
* innerHTML과 마찬가지로 크로스 사이트 스크립팅 공격에 취약



### 39.6.3 노드 생성과 추가

* DOM은 노드를 생성/삽입/삭제/치환하는 메서드도 제공



#### 요소 노드 생성

* Document.prototype.createElement(tagName)
  * tagName에는 태그 이름을 문자열로 전달
* 요소 노드를 생성하여 반환
* 생성한 요소 노드를 DOM에 추가하는 처리는 별도로 필요
* 자식 노드 또한 가지고 있지 않은 상태



#### 텍스트 노드 생성

* Document.prototype.createTextNode(text)
  * text에는 텍스트 노드의 값으로 사용할 문자열을 인수로 전달
* 텍스트 노드를 생성하여 반환
* 생성된 텍스트 노드를 요소 노드에 추가하는 처리가 별도로 필요



#### 요소 노드의 자식 노드로 추가

* Node.prototype.appendChild(childNode)
  * childNode에는 인수로 전달한 노드를 호출한 노드의 마지막 자식 노드로 추가
  * 해당 메서드로 텍스트 노드를 요소 노드에 추가 가능
  * 요소 노드를 DOM에 추가 가능
* 요소 노드에 자식 노드가 하나도 없을 때, 텍스트 노드를 추가할 대는 textContent 프로퍼티를 사용하는 것이 더 효율적



### 39.6.4 복수의 노드 생성과 추가

* 생성한 복수의 노드를 DOM에 추가할 때 컨테이너 요소를 활용하여 한 번에 추가
  * DOM은 한 번만 변경하게 되어 효율적
* DocumentFragment 노드를 사용하여, DOM에 추가
  * Document.prototype.createDocumentFragment
  * DOM에 추가 되면, 자신은 제거되고 자식 노드만 DOM에 추가 됨



### 39.6.5 노드 삽입

* 마지막 노드로 추가
  * Node.prototype.appendChild
* 지정한 위치에 노드 삽입
  * Node.prototype.insertBefore(newNode, childNode)
  * 첫 번째 인수로 전달받은 도드를 두 번쨰 인수로 전달받은 노드 앞에 삽입



### 39.6.6 노드 이동

* 이미 존재하는 노드를 appendChid 또는 insertBefore 메서드를 사용하여 DOM에 다시 추가하면 현재 위치에서 노드를 제거하고 새로운 위치에 노드를 추가



### 39.6.7 노드 복사

* Node.prototype.cloneNode
* 노드의 사본을 생성하여 반환
* 인수로 true를 전달하면 깊은 복사
  * false를 전달하면 얕은 복사



### 39.6.8 노드 교체

* Node.prototype.replaceChlid(newChild, oldChild)
* 자신을 호출한 노드의 자식 노드를 다른 노드로 교체



### 39.6.9 노드 삭제

* Node.prototype.removeChild(child)
* child 매개변수에 전달한 노드를 DOM에서 삭제