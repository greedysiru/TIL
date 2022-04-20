# 26장. ES6 함수의 추가 기능(2)

## 26.3 화살표 함수

### 26.3.3 this

* 화살표 함수가 일반 함수와 구별되는 가장 큰 특징
* 일반함수에서
  * this 바인딩은 함수의 호출방식에 따라 동적으로 결정
  * 일반 함수로서 호출되는 모든 함수의 내부 this는 전역 객체
  * strict mode에서는 undefined
  * 콜백 함수로 사용되는 일반 함수에서 문제를 일으킴
* 화살표 함수는
  * 함수 자체의 this를 가지지 않음
  * 상위 스코프의 this를 그대로 참조(Lexical This)
  * 화살표 함수의 this가 함수의 정의된 위치에따라 결정
  * call, bind 메서드를 사용해도 this 교체 불가
* 메서드를 화살표 함수로 정의하는 것은 피할 것
  * 상위 스코프의 this를 가리키게 됨
* 프로토타입 객체의 프로퍼티에 화살표 함수 정의하는 것은 피할 것



### 26.3.4 super

* 화살표 함수는 함수 자체의 super 바인딩을 가지지 않음
  * 상위 스코프의 super참조



### 26.3.5 arguments

* 화살표 함수는 함수 자체의 arguments 바인딩을 가지지 않음
  * 상위 스코프의 arguments를 참조
* 화살표 함수로 가변 인자 함수 구현 시에는 Rest 파라미터 사용