# 20장 strict mode(2)

## 20.3 전역에 strict mode를 적용하는 것은 피하자

* 전역에 적용한 경우, 스크립트 단위로 적용
  * 다른 스크립트에 영향을 주지 않고 해당 스크립트에 한정되어 적용
* 서드 파티 라이브러리가 none-strict mode인 경우, 오류를 발생
  * 전역에 사용하는 것은 바람직하지 않음
* IIFE를 사용하여 스코프를 구분할 것



## 20.4 함수 단위로 strict mode를 적용하는 것도 피하기

* 모든 함수에 strict mode를 적용하는것은 번거로운 일
* stirct mode를 적용한 함수가 외부 컨텍스트를 참조시, 해당 컨텍스트가 strict mode가 적용되어 있지 않다면 문제가 발생할 수 있음
  * 즉, IIFE를 감싼 스크립트 단위로 활용할 것



## 20.5 strict mode가 발생시키는 에러

* 암묵적 전역
  * 선언하지 않은 변수 참조시, Reference Error 발생
* 변수, 함수, 매개변수의 삭제
  * delete 연산자로 변수, 함수, 매개변수 삭제시 SyntaxError가 발생
* 매개변수 이름의 중복
  * 중복된 매개변수 이름 사용시 SyntaxError가 발생
* with문의 사용
  * SyntaxError가 발생



## 20.6 strict mode 적용에 의한 변화

### 20.6.1 일반 함수의 this

* 일반 함수로서 호출하면 this에 undefined가 바인딩
  * 생성자 함수가 아니면 this를 사용하지 않으므로



### 20.6.2 arguments 객체

* 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않음

