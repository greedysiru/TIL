# TypeScript(1)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. 타입 안정성

* JavaScript는 런타임 에러를 방지해주지 않음
  * 유저가 마주칠 수 있음
  * 전혀 다른 타입끼리의 연산, 존재하지 않는 메서드의 호출, 함수 매개변수의 잘못된 전달 등을 감지하지 않음
* TypeScript는 타입 안정성을 부여하여 런타임 에러를 최소화 시킬 수 있음



## 2. TypeScript

* 강타입의 프로그래밍 언어
* JavaScript의 Super Set
* TypeScript는 JavaScript로 변환
  * 브라우저가 JavaScript 만을 이해하기 때문
  * Node는 TypeScript, JavaScript 둘 다 이해
* TypeScript에 에러가 발생(또는 감지)하면, JavaScript로 변환되지 않음
  * 타입 추론



## 3. Type System

* TypeScript는 타입을 명시적으로 정의할 수 있음
  * 또는 변수만 생성하고 넘어갈 수도 있음(타입 추론)
* 별도의 명시적 타입 정의 없이 변수에 문자열/숫자를 할당하면, 타입 추론으로 해당 변수의 타입이 지정됨

### 명시적 타입 vs. 타입 추론

* 일반적인 상황에서, 타입 추론을 활용하는 것이 좋음
  * 가독성과 생산성에서 좋음

```TypeScript
let ex1 = "string"; // 타입 추론으로 인해 ex1은 string type으로 정의
let ex2: string = "stiring"; // 명시적 타입 정의로인해 string type
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

