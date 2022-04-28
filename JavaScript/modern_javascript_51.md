# 24장 클로저(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 24.4 클로저의 활용

* 상태를 안전하게 변경하고 유지하기 위해 사용
  * 상태를 은닉
  * 특정 함수에서만 상태 변경 허용
* 가변 데이터를 피하고 불변성을 지향하는 함수형 프로그래밍에서 적극 사용 됨



### 예시

```JavaScript
const counter = (function(){
  // 즉시 실행 함수
  // 클로저를 반환하여 식별자 counter에 할당
  
  let num = 0;
  
  // 이 함수의 생명 주기가 끝나도 렉시컬 환경을 기억함
  return {
    increase() {
      return ++num;
    }
    
    decrease() {
      return --num;
    }
  }
}());
```



### 함수형 프로그래밍에서의 예시

```JavaScript
// 고차함수
// 함수를 인수를 전달받아 클로저 생성
function makeCounter(aux) {
  let counter = 0;
  
  // 클로저 생성하여 반환
  return funciton() {
    counter = aux(counter);
    return coutner;
  }
}

// 고차함수에 넘길 함수들
function increase(n) {
  return ++n;
}

function decrease(n) {
  return ++n;
}
```

