# 26장. ES6 함수의 추가 기능(3)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 26.4 Rest 파라미터

### 26.4.1 기본 문법

* 매개변수 이름 앞에 세개의 점을 붙여서 표현
* Rest 파라미터는 함수에 전달된 목록을 배열로 전달 받음
* 일반 파라미터와 혼용 가능
* 반드시 마지막 파라미터여야 함
* 단 하나만 선언 가능

```JavaScript
function eatChuru(...churus) {
  console.log(churus); // ['참치맛', '닭고기맛', '연어맛']
}
```



### 26.4.2 Rest 파라미터와 arguments 객체

* arguments는 유사 배열 객체
  * 순회 가능
  * 함수 내부에서 지역변수처럼 사용
  * call, apply 메서드를 사용해 배열로 변환해야 함
* Rest 파라미터는 배열로 변환하지 않아도 됨



## 26.5 매개변수 기본값

* 자바스크립트 엔진이 매개변수의 개수와 인수의 개수를 체크하지 않음
* 전달되지 않은 매개변수로 인한 오류를 방지하여 기본값을 할당할 필요가 있음
* ES6에서 도입된 매개변수 기본값 사용할 것
  * 전달하지 않았을 때 또는 undefined일 때 유효
* Rest 파라미터에는 기본값 지정 불가능
* arguments 객체에 영향 없음

```JavaScript
function eatChuru(churu1, churu2) {
  churu1 = churu1 || '참치맛';
  churu2 = churu2 || '닭고기맛';
  console.log(churu1, churu2);
}

// ES6 매개변수 기본값
function eatChuru(churu1 = '참치맛', churu2 = '닭고기맛') {
  consoel.log(churu1, churu2);
}
```

