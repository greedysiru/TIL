# 14장 - 전역 변수의 문제점(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 14.2 전역 변수의 문제점

### 14.2.1 암묵적 결합

* 모든 코드가 전역 변수를 참주하고 변경할 수 있게 되는 것
* 코드의 가독성은 나빠지고 상태가 변경되기 쉬워짐



### 14.2.2 긴 생명 주기

* 메모리 리소스를 오랜 기간 소비
* 의도하지 않은 재할당이 일어날 수 있음



### 14.2.3 스코프 체인 상에서 종점에 존재

* 전역 변수는 스코프 체인 상 가장 마지막애 존재
* 전역 변수를 찾기까지의 검색 시간이 걸리게 됨



### 14.2.4 네임스페이스 오염

* 자바스크립트에서는 파일이 분리되어 있어도 하나의 전역 스코프를 공유
* 파일 간의 변수 또는 함수가 겹치면 예기치 못한 문제 발생



## 14.3 전역 변수의 사용을 억제하는 방법

* 전역변수를 지양하고 지역변수를 사용할 것



### 14.3.1 즉시 실행 함수

* 모든 코드를 즉시 실행 함수로 감싸면, 그 함수의 지역변수가 됨
* 라이브러리 등에 자주 사용

```JavaScript
(function (){
  var petName = 'siru';
}());
```



### 14.3.2 네임스페이스 객체

* 전역에 네임스페이스를 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가
* 객체를 추가해서 계층적으로 구성 가능

```JavaScript
var MYPET = {};

MYPET.name = 'siru';

MYPET.inoculationInformation = {
  FPV: true,
  FCV: true,
};
```



### 14.3.3 모듈 패턴

* 클래스를 모방하여 관련 변수, 함수를 모아 즉시 실행 함수로 만듦
* 클로저로 전역 변수 억제
* 한정적인 정보 은닉
  * private : 외부로 노출되지 않는 변수
* 객체를 반환
  * 반환되는 객체의 프로퍼티는 public

```JavaScript
var churuCounter = (function() {
  // private
  var churuAmount = 0;
  return {
    print() {
      console.log(`시루는 츄르를 현재 ${churuAmount}개 먹었다.`);
      return
    },
    eat() {
      return ++churuAmount;
    }
  }
}());

churuCounter.print(); // 시루는 츄르를 현재 0개 먹었다.
console.log(churuCounter.eat()); // 1
churuCounter.print(); // 시루는 츄르를 현재 1개 먹었다.
console.log(churuCounter.eat()); // 2
churuCounter.print(); // 시루는 츄르를 현재 2개 먹었다.
```



### 14.3.4 ES6 모듈

* 전역 변수 사용 불가
* 파일 자체의 독자적인 스코프 제공
* script 태그에 type="module" 어트리뷰트 추가
* 확장자는 mjs 권장

