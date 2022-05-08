# 39장. DOM(2)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 39.2 요소 노드 취득

* HTML의 구조나 내용, 스타일을 동적으로 조작하기 위해서는 요소 노드를 취득해야 함
* DOM은 요소 노드를 취득할 수 있는 다양한 메서드 제공



### 39.2.1 id를 이용한 요소 노드 취득

* Document.prototype.getElementById
* 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환
* id는 문서 내에서 유일한 값이어야 함
  * 여러개가 존재하더라도, 에러가 발생하지는 않으나 첫 번째 요소만을 반환
  * 존재하지 않는 경우 null을 반환



### 39.2.2 태그 이름을 이용한 요소 노드 취득

* Document.prototype/Element.prototype.getElementsByTagName
  * Document에 정의되어 있는 메서드의 경우, DOM 전체에서 요소 노드를 탐색하여 반환
  * Element에 정의되어 있는 메서드의 경우, 특정 요소의 자손 노드 중에서 요소 노드를 탐색하여 반환
* 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 DOM 컬렉션 객체인 HTMLCollection으로 반환
  * astarisk(*)를 전달하면, 모든 요소 노드들을 취득
* HTMLCollection
  * 유사 배열 객체
  * 이터러블



### 39.2.3 class를 이용한 요소 노드 취득

* Document.prototype/Element.prototype.getElementByClassName
* 인수로 전달한 class 이름을 갖는 모든 요소 노드들을 탐색하여 반환
* HTMLCollection 객체로 반환



### 39.2.4 CSS 선택자를 이용한 요소 노드 취득

* Document.prototype/Element.prototype.querySelector
* 인수로 전달한 CSS 선택자를 만족시키는
  * 요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환
  * 요소 노드가 존재하지 않은 경우 null을 반환
  * 문법에 맞지 않는 경우 DOMExeption 에러가 발생
* astarisk(*)를 전달하면, 모든 요소 노드들을 취득
* DOM Collection 객체인 NodeList 객체 반환
  * NodeList : 유사 배열 객체이면서 이터러블
* getElementBy~ 와 같은 메서드들보다 다소 느림
  * 하지만 더 구체적인 조건으로 요소 노드를 취득할 수 있고 일관된 방식으로 요소 노드를 취득 가능



### 39.2.5 특정 요소 노드를 취득할 수 있는지 확인

* Element.prototype.matches
* 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인
  * 여부를 Boolean으로 반환



### 39.2.6 HTMLCollection과 NodeList

* 둘 다 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체
  * 유사 배열 객체이면서 이터러블
  * for..of 문으로 순회 가능
  * 스프레드 문법을 사용하여 간단히 배열로 변환 가능
* HTMLCollection은 live 객체
* NodeList는 non-live 객체
  * 경우에 따라 live 객체로 동작할 때가 있음



#### HTMLCollection

* getElementsByTagName, getElementsByClassName 메서드가 반환
* 노드 객체의 상태 변화를 실시간으로 반환하는 DOM 컬렉션 객체
  * 부작용을 발생시키는 원인이 될 수 있음
* 배열로 변환하여 사용하면, 부작용을 방지하고 유용한 배열의 고차 함수를 사용할 수 있음



### NodeList

* HTMLCollection 객체의 부작용을 해결하기 위해 querySelectorAll 메서드를 사용하는 방법이 있음
  * NodeList 객체 반환
* 실시간으로 노드 객체의 상태 변경을 반영하지 않는 객체
  * childeNodes 프로퍼티가 반환하는 NdoeList 객체는 live 객체로 동작함에 주의
* NodeList 역시 배열로 변환하여 사용하는 것을 권장

