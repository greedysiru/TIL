# 실행 컨텍스트(1)

**본 내용은 10분 테코톡 하루님의 강의를 토대로 작성하였습니다.**



## 1. 실행 컨텍스트란

* Execution Context
* JavaScript 스펙을 위한 메커니즘
* JavaScript를 실행시키면 JavaScript Engine은 Call Stack이라는 통에 Global Execution Context를 담음
  * Global Execution Contextd에는 Record와 Outer가 담겨 있음
* 임의의 함수 A를 호출하면 함수 A의 Execution Context를 생성해서 Call stack에 담음
  * 이또한 Record와 Outer가 담겨 있음
* Call Stack에서는 가장 최근에 추가된 Execution Context만 활성화 됨
* 함수 A가 종료되면 함수 A의 Execution Context는 사라짐
* 전역에 있는 코드가 마지막 라인까지 모두 실행되면, Global Execution Context도 사라짐



## 2. Record로 JavaScript 호이스팅 이해하기

### Hoisting

* var 키워드를 사용한 변수 선언 전에 변수를 호출하여도 호이스팅으로 인해 오류가 발생하지 않음
* Hoisting
  * 호이스팅
  * 선언문이 마치 최상단에 끌어올려진 듯한 현상
  * JavaScript Engine이 먼저 전체 코드를 스캔하면서 변수 같은 정보를 Execution Context의 **Record**에 기록

```JavaScript
// Global
console.log(TVChannel); // undefined

var TVChannel = "Netflix";

console.log(TVChannel); // Netflix
```



### Record

* 정식 명칭은 **Environment Record**(환경 레코드)라고 함
* 식별자와 식별자에 바인딩된 값을 기록하는 객체



### Variable Hoisting

* 변수 호이스팅
* **생성 단계**: Execution Context를 생성하고 선언문만 실행해서 Enviroment Record에 기록
  * JavaScript Engine은 코드를 실행하면 우선 Global Execution Context 한 칸을 생성해서 Call Stack에 넣음
  * 그 후, 전체 코드를 스캔하면서 선언할 것이 있는지 찾아보고 있으면 먼저 선언을 함
  * 선언하는 과정에는 생성해둔 Execution Context 안에 있는 Enviroment Record에 새로운 식별자를 기록
  * var 키워드의 경우 undefined로 값을 초기화 해 둠
* **실행 단계**: 선언문 외 나머지 코드를 순차적으로 실행, Eviroment Record를 참조하거나 업데이트
  * 변수가 사용이 되면, 해당 변수에 바인딩된 값을 JavaScript Engine이 현재 활성화된 Execution Context의 Enviroment Record 내에서 찾음
  * var의 경우 변수 값이 할당이 된 시점에서 업데이트



### const, let

* JavaScript Engine이 식별자를 기록하지만 값을 초기화하지는 않음
* 선언문 이전에 변수를 참조하려고 하면, Reference Error가 발생
* **Temporal Dead Zone**(일시적 사각지대)
  * let 또는 const으로 선언했을 때, 선언 이전에 식별자를 참조할 수 없는 구역
* **Declaration**(선언): 메모리 공간을 확보하고 식별자와 연결
* **Initialization**(초기화): 할당문 직전까지는 초기화를 하지 않음



### var

* **var 키워드는 선언과 초기화가 동시에 이루어짐**
* **Declaration**(선언): 메모리 공간을 확보하고 식별자와 연결
* **Initialization**(초기화): 식별자에 암묵적으로 undefined 값 바인딩



### Function Hoisitng

* 함수 호이스팅
* **Function Expression**(함수 표현식): JavaScript 에서는 함수를 변수에다가 담을 수 있음
  * 변수 호이스팅과 동일하게 동작
* var 키워드로 선언된 변수에 함수를 담아 선언문 이전에 실행하려고 하면, Enviroment Record에 기록된 변수의 값은 undefined 임
  * undefined라는 자료형은 실행할 수 없음, 그러므로 Type Error가 발생
* const 키워드의 경우 Reference Error 발생
* **Function Declaration**(함수 선언문): function 키워드로 함수를 선언하는 방식
  * JavaScript Engine이 함수의 선언과 동시에 완성된 함수 객체를 생성해서 Enviroment Record에 기록
  * 선언 전에도 함수를 사용할 수 있음
  * 사용을 지양하는 것이 좋음

```JavaScript
// Global
study1(); // Type Error

var study1 = () => {
  ...
};
  
study2(); // Reference Error
  
const study2 = () => {
  ...
};
  
  
study3();  // Error 없이 실행
  
function study3() {
  ...
};
```



# Reference

[[10분 테코톡] 하루의 실행 컨텍스트](https://www.youtube.com/watch?v=EWfujNzSUmw)

