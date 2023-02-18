# Understanding TypeScript(18) - never

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## never

* 함수가 반환할 수 있는 타입
  * 아무것도 return하지 않는 다는 의미
  * void는 엄밀히 undefined를 return



### 예시

```TypeScript
// 에러를 발생시키는 함수
// Error를 throw하면 그 무엇도 return하지 않으므로 never type
const generateError = (message: string, code: number): never => {
  throw { message, errorCode: code };
};

// 결과를 할당하여도 에러가 발생하여 할당 자체가 되지 않음(never)
const result = generateError("에러 발생", 500);
// 실행 자체가 되지 않는 코드
console.log(result);

```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

