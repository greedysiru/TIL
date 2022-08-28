# TypeScript(4)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. Polymorphism

* 다형성
  * 다양한 구조를 가지는 것
* Generic
  * Type의 Placeholder 같은 것
* 사용할 함수의 모든 용도를 고려하여 Call signature를 정의하는 것은 비효율적



## 2. Geneirc

* Generic을 사용하여, 다형성을 구현
  * 함수의 다양한 형태를 구현
  * 작성한 코드의 타입 기준으로 바꿔줌
* <>(꺽쇠) 안에 사용할 제네릭을 명시
* 함수를 단일 타입이 아닌, 다양한 타입에서 작동하게 할 수 있음
  * 재사용성 증대
* 선언 시점이 아니라 생성 시점에 타입을 명시하여 다양한 타입을 사용할 수 있도록 하는 기법

```TypeScript
type CallAllItem = {
  <T>(arr: T[]):T
}

const callAllItem: CallAllItem = (arr) => arr[0];
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

