# 32장. String

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

* 원시 타입인 문자열을 다룰 때 유용한 프로퍼티와 메서드 제공

## 32.1 String 생성자 함수

* new 연산자와 함께 호출하여 String 인스턴스 생성 가능
* 인수 전달하지 않고 호출하면, [[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체 생성
* 인수를 전달하면, [[StringData]] 내부 슬롯에 문자열을 할당한 String 래퍼 객체 생성
* String 래퍼 객체는 유사 배열 객체, 이터러블
  * length 프로퍼티, 인덱스를 가짐
* new 없이 인수를 전달하면, 문자열을 반환



## 32.2 length 프로퍼티

* 접근시, 문자 개수 반환



## 32.3 String 메서드

* 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않음
  * 언제나 새로운 문자열을 반환
* String 래퍼 객체도 읽기 전용 객체로 제공



### 메서드 정리

* String.prototype.indexOf: 인수로 전달 받은 문자열을 검색하여 첫 번째 인덱스 반환
  * 두번 째 인수로 검색을 시작할 인수 전달 가능
* String.prototype.search: 정규 표현식과 매치하는 문자열 검색하여 인덱스 반환
  * 검색 실패시, -1 반환
* String.prototype.includes: 인수로 전달받은 문자열의 포함 유무를 반환
* String.prototype.startWith: 인수로 전달받은 문자열로 시작하는지 확인하여 그 결과를 반환
* String.prototype.endsWith: 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 반환
* String.prototype.charAt: 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환
* String.prototype.substring: 첫 번째 인수로 전달받은 인덱스 ~ 두 번째 인수로 전달받은 인덱스 전까지의 부분 문자열 반환
* String.prototype.slice: substring 메서드와 동일하게 동작, 음수를 전달 가능
* String.prototype.toUpperCase: 대상 문자열 모두 대문자로 변환
* String.prototpye.toLowerCase: 대상 문자열 모두 소문자로 변환
* String.prototype.trim: 앞뒤 공백 문자를 제거하여 반환
* String.prototype.replace: 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 두 번째 인수로 전달한 문자열로 치환하여 반환
  * 치환 함수 전달 가능
* String.prototype.split: 첫 번째 인수로 전달한 문자열 또는 정규표현식을 검색하여 문자열을 구분하여 배열로 반환



