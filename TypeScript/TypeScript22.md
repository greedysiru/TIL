# TypeScript(3)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. Call Signatures

* 함수의 타입
  * 어떤 타입을 받고 어떤 타입을 반환하는지 명시할 수 있음

```TypeScript
type Sum = (a: number, b: number) => number;

const sum: Sum => (a, b) => a + b;
```



## 2. Overloading

* 함수가 여러개의 Call Signatures를 가지고 있을 때 발생시킴
* 외부 라이브러리에서 자주 보이는 형태
* 다양한 방식으로 호출할 수 있는 함수를 지정할 수 있음

```TypeScript
// merge type은 문자열들을 받았을 때는 문자열 합성을, 숫자들을 받았을 때는 숫자 합을 return
type Merge = {
  (a: number, b: number) : number
  (a: string, b: string) : string
}

const merge: Merge = (a, b) => {
  if (typeof a === "string" && typeof a === "string") {
    return `${a}${b}`;
  } else {
    return a + b;
  }
}
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

