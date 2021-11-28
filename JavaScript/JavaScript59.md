# 실행 컨텍스트(2)

**본 내용은 10분 테코톡 하루님의 강의를 토대로 작성하였습니다.**



## 1. Outer로 JS 스코프체이닝 이해하기

### Outer

* Outer Enviroment Reference
  * 외부환경 참조
* 바깥 Lexical Enviroment를 가리킴



### 식별자 결정

* Identifier Resolution
  * 코드에서 변수나 함수의 값을 결정하는 것
* Call Stack 안에 동일한 식별자가 여러개일때 JavaScript 엔진이 Outer를 활용해서 의사결정
* Lexical Enviroment가 생성되었을 때, 바깥 Lexical Enviroment로 돌아갈 수 있는 Outer를 남김
  * 필요한 경우에, 이전 실행 컨텍스트의 환경 레코드에 저장된 식별자도 참조할 수 있게 됨
* JavaScript Engine은 원칙적으로 실행 컨텍스트의 환경 레코드를 먼저 봄
* 실행 컨텍스트의 환경 레코드에 식별자가 없는 경우 Otuer가 가리키는 바깥 Lexical Enviroment에 접근
  * 전역 실행 컨텍스트까지 접근
  * 전역 실행 컨텍스트에까지 해당 식별자를 찾지 못하면, Reference Error 발생



### 변수 섀도잉

* Variable Shadowing
* 동일한 식별자로 인해 상위 스코프에서 선언된 식별자의 값이 가려지는 현상

```JavaScript
let lamp = false;

function goTo2F() {
  let lamp = true;
  
  console.log(lamp); // true
  
}

goTo2F();
```



### 스코프 체인

* Scope Chain
* 식별자를 결정할 때 활용하는 스코프들의 연결리스트



## 2. Execution Context 정리

* 코드를 실행하는데 필요한 환경을 제공하는 객체
* 환경
  * 코드 실행에 영향을 주는 조건이나 상태
* ES3 시절에는 함수가 어디에서 호출되느냐에 따라 스코프가 달라졌었음
  * 함수가 호출될 때마다 동적으로 그에 걸맞는 스코프를 생성하고 스코프 체인을 연결해야 했음
  * 동적 스코프
* ES5 이후 식별자 결정을 위한 메커니즘이 변경
  * 실행 컨텍스트라는 하나의 덩어리, 하나의 묶음으로 관리
  * 정적 스코프
  * JavaScript Engine이 더 빠르고 효율적으로 식별자를 결정할 수 있게 됨
* 코드를 실행할 때 식별자를 더욱 효율적으로 결정하기 위한 수단

# Reference

[[10분 테코톡] 하루의 실행 컨텍스트](https://www.youtube.com/watch?v=EWfujNzSUmw)

