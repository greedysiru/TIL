# 39장. DOM(5)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 39.7 어트리뷰트

### 39.7.1 어트리뷰트 노드와 attributes 프로퍼티

* HTML 요소는 여러 개의 어트리뷰트(속성)를 가질 수 있음
* 특정 HTML 요소에만 한정적으로 사용 가능한 어트리뷰트도 있음
  * input 요소에만 사용 가능한 type, value, checked 어트리뷰트
* HTML 문서가 파싱될 때 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드와 연결
* 어트리뷰트 노드의 참조는 NamedNodeMap 객체에 담겨서 요소 노드의 attributes 프로퍼티에 저장
* Element.prototype.attribues 프로퍼티로 취득 가능
  * getter만 존재하는 읽기 전용 접근자 프로퍼티
  * NamedNodeMap 객체를 반환



### 39.7.2 HTML 어트리뷰트 조작

* Element.prototype.getAttribute/setAttribute 메서드를 사용하면 HTML 어트리뷰트 값을 취득 또는 변경 가능
* Element.prototype.hasAttribute: HTML 요소에 어트리뷰트 존재 유무 확인
* Element.prototype.removeAttribute: HTML 어트리뷰트 삭제



### 39.7.3 HTML 어트리뷰트 vs. DOM 프로퍼티

* 요소 노드 객체에는 HTML 어트리뷰트에 대응하는 프로퍼티 존재
* DOM 프로퍼티는 setter, getter 모두 존재하는 접근자 프로퍼티
* HTML 어트리뷰트의 역할
  * HTML 요소의 초기 상태를 저장
  * 변하지 않음
* DOM 프로퍼티
  * 요소 노드의 최신 상태 관리
* HTML 어트리뷰트와 DOM 프로퍼티는 1:1으로 대응
  * 언제나 대응하는 것은 아님
* HTML 어트리뷰트는 언제나 문자열
  * DOM 프로퍼티는 무낮열이 아닐 수도 있음



### 39.7.4 data 어트리뷰트와 dataset 프로퍼티

* HTML 요소에 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터 교환 가능
* data- 접두사 다음에 임의의 이름 붙이기
* Element.dataset 프로퍼티로 취득
  * data 어트리뷰트 정보를 제공하는 DOMStringMap 객체 반환



## 39.8 스타일

### 39.8.1 인라인 스타일 조작

* HTMLElement.prototype.style
  * getter, setter 모두 존재하는 접근자 프로퍼티
  * 인라인 스타일을 취득하거나 추가 또는 변경
  * CSSStyleDeclaration 타입의 객체 반환
* CSSStyleDeclaration
  * CSS 프로퍼티에 대응하는 프로퍼티 가지고 있음
  * 값을 할당하면 CSS 프로퍼티가 인라인 스타일로 HTML 요소에 추가 또는 반영
  * 카멜케이스를 따름



### 39.8.2 클래스 조작

* class 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티를 사용

  

#### className

* setter, getter 모두 존재하는 접근자 프로퍼티
* HTML 요소의 class 어트리뷰트 값을 취득 또는 변경
* 문자열을 반환하므로 여러 개의 클래스를 다루기 불편



#### classList

* class 어트리뷰트의 정보를 담은 DOMToketList 객체를 반환
* 컬랙션 객체, 유사 배열 객체이면서 이터러블
* 다양한 메서드 제공
* add: 인수로 전달한 1개 이상의 문자열을 calss 어트리뷰트 값으로 추가
* remove: 인수로 전달한 1개 이상의 문자열과 일치하는 클래스를 삭제
* contains: 인수로 전달한 문자열과 일치하는 클래스가 포함되어 있는지 확인
* replace: 첫 번째 인수로 전달한 문자열을 두 번째 인수로 전달한 문자열로 클래스 변경
* toggle: 일치하는 클래스가 있으면 제거하고 존재하지 않으면 추가