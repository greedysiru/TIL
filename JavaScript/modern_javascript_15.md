# 12장 - 함수(1)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 12.1 함수란?

* 수학적 개념의 입력을 출력으로 내보내는 일련의 과정과 어느정도 비슷
  * 자바스크립트의 함수는 출력(반환값)이 없을 수도 있음
* 프로그래밍에서의 일련의 과정이란, 문으로 구현 됨
  * 코드 블록
* 매개 변수: 내부로 입력 **받는** 변수
* 인수: 내부로 입력 **하는** 변수
* 반환값: **출력**
* 함수는 함수 정의로 생성
  * 함수 선언문
  * 함수 표현식
  * 함수 생성자
* 함수 호출: 함수의 실행을 명시적으로 지시하는 것

```JavaScript
// 함수 정의
// name: 매개 변수
function callMyPet(name) {
  const message = `이리오려무나 ${name}!`
  // message: 출력(반환값)
  return message;
}

// 함수 호출
// 'siru': 인수
console.log(callMyPet('siru')); // 이리오려무나 시루!
```



## 12.2 함수를 사용하는 이유

* 재사용이 가능한 코드를 만들 수 있음
  * 효율성 증대
  * 유지보수 편의성
  * 코드의 신뢰성
* 적절한 함수 명을 붙여 코드의 의도를 분명하게 드러낼 수 있음
  * 코드 가독성 향상



## 12.3 함수 리터럴

* 함수는 객체 타입
  * 객체와 다르게 호출할 수 있음
* 함수 리터럴로 함수를 생성할 수 있음
  * function 키워드, 함수 명, 매개 변수, 코드 블록
  * 함수 리터럴로 평가되어 값을 생성하고 변수에 할당될 수 있음
* 함수 이름은 생략할 수 있음
  * 기명 함수, 무명 함수



### 함수 리터럴의 구성 요소

* 함수 이름
  * 식별자 네이밍 규칙 준수하기
  * 함수 몸체 내부에서만 참조할 수 있는 식별자
* 매개 변수
  * 매개 변수 순서에 따라 함수 호출시 지정한 인수가 순서대로 할당
  * 식별자 네이밍 규칙 준수하기
  * 함수내에서 변수 취급
* 함수 몸체
  * 호출 시 실행될 문들이 모인 실행 단위