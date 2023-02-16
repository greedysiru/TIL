# Understanding TypeScript(17) - Unknown

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Unknown

* 어떤 타입이 들어올 지 모를 때 사용
* 사용함에 있어서 타입 체크가 강제되므로 안전
  * any는 모든 값을 허용하므로 타입 체크도 강제되지 않음
  * any보다 사용을 권장
* 미래에 어떤 타입이 들어갈지 자명해지면 타입을 지정



### 예시

```TypeScript
// 어떤 타입이 들어올 것인지 모름
let userInput: unknown;
let userName: string;

// 어떤 타입을 할당해도 Error가 발생하지 않음(any와 비슷)
userInput = 5;
userInput = "James";
// Error, 할당할 수 없음
// unknown 타입이 string임이 보장되지 않으므로
// any라면 할당 가능
userName = userInput;

if (typeof userInput === 'string') {
  // userInput이 string임이 보장되므로 할당 가능
userName = userInput;
}
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

