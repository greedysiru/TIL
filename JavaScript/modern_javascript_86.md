# 39장. DOM(3)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 39.3 노드 탐색

* 요소 노드 취득 후 부모, 형제, 자식 노드 등을 탐색
* Node.prototype
  * parentNode
  * previousSibling
  * firstChild
  * childeNodes
  * 모두 읽기 전용 접근자 프로퍼티이므로 값을 할당할 수 없음
* Element.prototype
  * previousElementSibling
  * nextElementSibling
  * childeren



### 39.3.1 공백 텍스트 노드

* 공백 텍스트 노드 : HTML 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백 문자는 텍스트 노드 생성
* 노드 탐색 시, 공백 텍스트 노드에 주의



### 39.3.2 자식 노드 탐색

* Node.prototype.childNodes
  * 자식 노드를 모두 탐색
  * NodeList에 담아 반환
  * 텍스트 노드 포함
* Element.prototype.children
  * 자식 노드 모두 탐색
  * HTMLCollection에 담아 반환
  * 텍스트 노드 미포함
* Node.prototype.firstChild
  * 첫 번째 자식 노드 반환
  * 텍스트 노드 포함
* Node.prototype.lastChild
  * 마지막 자식 노드 반환
  * 텍스트 노드 포함
* Element.prototype.firstElementChild
  * 첫 번째 자식 요소 노드 반환
* Element.prototype.lastElementChild
  * 마지막 자식 요소 노드 반환



### 39.3.3 자식 노드 존재 확인

* Node.prototype.hasChildNodes
  * 자식 노드가 존재하면 true 반환



### 39.3.4 부모 노드 탐색

* Node.prototype.parentNode
* 부모 노드가 텍스트 노드인 경우는 없음
  * 텍스트 노드는 리프 노드이므로



### 39.3.5 형제 노드 탐색

* 부모가 같은 형제 노드를 탐색
* 어트리뷰트 노드는 반환되지 않음
* Node.prototype.previousSibling
  * 이전 형제 노드 반환
  * 텍스트 노드 포함
* Node.prototype.nextSibling
  * 다음 형제 노드 반환
  * 텍스트 노드 포함
* Element.prototype.previousElementSibling
  * 이전 형제 요소 노드 반환
* Element.prototype.nextElementSibling
  * 다음 형제 요소 노드 반환



## 39.4 노드 정보 취득

* Node.prototype.nodeType
  * 노드 타입을 나타내는 상수 반환
  * 노드 타입 상수는 Node에 정의
  * Node.ELEMENT_NODE: 요소 노드 타입을 나타나는 1
  * Node.TEXT_NODE: 텍스트 노드 타입을 나타내는 3
  * Node.DOCUMENT_NODE: 문서 노드 타입을 나타내는 9
* Node.prototype.nodeName
  * 노드의 이름을 문자열로 반환
  * 요소 노드 : 태그 명을 대문자 문자열로 반환
  * 텍스트 노드 : #text를 반환
  * 문서 노드 : #document를 반환



## 39.5 요소 노드의 텍스트 조작

### 39.5.1 nodeValue

* Node.prototype.nodeValue
* setter, getter 모드 존재하는 접근자 프로퍼티
* 노드 객체의 값 반환
* 노드 객체의 값은 텍스트 노드의 텍스트
* 문서 노드, 요소 노드의 nodeValue를 참조하면 null 반환



### 39.5.2 textContent

* Node.prototype.textContent
* setter, getter 모두 존재하는 접근자 프로퍼티
* 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 취득 및 변경
* 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내의 텍스트 모두 반환
* 문자열 할당 시, 모든 자식 노드가 할당한 문자열로 텍스트 추가 됨
* inneText 프로퍼티와 유사
  * CSS 순종적이어서 CSS를 고려해야 하므로 느림