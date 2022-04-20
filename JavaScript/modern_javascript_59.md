# 26장. ES6 함수의 추가 기능(1)

## 26.1 함수의 구분

* ES6 이전의 모든 함수는 일반 함수 또는 생성자 함수로서 호출 가능
  * callable이면서 constructor
  * 객체에 바인딩된 함수(일반적으로 메서드라 칭했던 것)
  * 불필요한 프로토타입 객체를 생성하여 성능상에서 문제
* ES6 이후로 함수를 사용 목적에 따라 세 가지 종류로 명확히 구분
  * 일반 함수
  * 메서드
  * 화살표 함수



## 26.2 메서드

* ES6 이후로 메서드 축약 표현으로 정의된 함수를 지칭
* non-constructor
  * 생성자 함수로서 호출 불가
* 인스턴스 생성 불가
  * prototype 프로퍼티가 없고 프로토타입도 생성하지 않음
* 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 가짐
  * 수퍼클래스의 메서드를 참조 하므로 super 키워드 사용 가능

```JavaScript
const siru = {
  cry() {
    cnosole.log('야옹');
  }
}
```



## 26.3 화살표 함수

* 간략한 함수 정의
* 내부 동작 또한 간략화
* 일반 함수를 콜백 함수로 사용하였을 때, this가 전역 객체를 가리키는 문제 해결하는 대안으로 유용
* IIFE로 사용 가능



### 26.3.1 화살표 함수 정의

```JavaScript
// 함수 정의
const cry1 = () => {
  return '야옹!';
};

// 매개변수 선언
// 매개변수 한 개인 경우, 소괄호 생략 가능
const cry2 = isCat => {
	return isCat? '야옹!' : '으앙';
};

// 하나의 문인 경우 중괄호 생략 가능
const cry3 = () => '야옹!';

// 객체의 경우, 소괄호로 감싸기
const cry4 = () => ({ cryString: '야옹'});
```



### 26.3.2 화살표 함수와 일반 함수의 차이

* 화살표 함수는 non-constructor
  * prototype 프로퍼티가 없고 프로토타입도 생성하지 않음
* 중복된 매개변수 이름 선언 불가
* 함수 자체 this, arguments, super, new.target 바인딩을 갖지 않음
  * 스코프 체인을 통해 사위 스코프를 참조