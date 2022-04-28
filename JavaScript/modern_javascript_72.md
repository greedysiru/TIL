# 31장. RegExp(1)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 31.1 정규 표현식이란?

* 정규표현식: 일정한 패턴을 가진 문자열의 집한을 표현하는 형식 언어
  * 대부분의 프로그래밍 언어와 코드 에디터에 내장
  * 자바스크립트는 펄의 정규 표현식 문법을 도입(ES3)
* **패턴 매칭 기능** : 특정 패턴과 일치하는 문자열 검색 또는 치환할 수 있는 기능
  * 유효성 검사에 사용(휴대전화, 이메일, 아이디 형식, 비밀번호 형식 등)



## 31.2 정규 표현식의 생성

* 정규 표현식 리터럴
  * 패턴과 플래그로 구성
* RegExp 생성자 함수 사용하여 객체 생성
  * 변수를 사용ㅎ해 동적으로 RegExp 객체 생성 가능

```javascript
// 패턴 : cat
// 플래그 : i
const regexp = /cat/i;

new RegExp(/cat/i);
```





## 31.3 RegExp 메서드

### 31.3.1 RegExp.prototype.exec

* 인수로 전달받은 문자열에 대해 정규 표현식의 패턴 검색
* 매칭 결과 배열로 반환
  * 없는 경우 null을 반환

```JavaScript
const target = 'siru is cat';
const regExp = /cat/;

regExp.exec(target); // ['cat', index: 8, input: 'siru is cat', groups: undefined]
```



### 31.3.2 RegExp.prototype.test

* 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환

```JavaScript
const target = 'siru is cat. cat is siru';
const regExp = /cat/;

regExp.test(target); // true
```



### 31.3.3 String.prototype.match

* 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환

```JavaScript
const target = 'siru is cat. cat is siru';
const regExp = /cat/;

target.match(target); // ['siru is cat. cat is siru', index: 0, input: 'siru is cat. cat is siru', groups: undefined]
```

