# Understanding TypeScript(16) - Function Types & Callbacks

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Function Types & Callbacks

* Function Type에 callback에 대한 타입 또한 명시할 수 있음



### 예시

```TypeScript
// addAndHandle은 두 숫자와 하나의 콜백 함수를 전달 받아 로직을 실행하는 함수
// 콜백에 대한 타입 또한 명시되어 있음
// 콜백은 숫자 하나를 전달 받아 아무것도 리턴하지 않음
const addAndHandle = (n1: number, n2: number, cb: (num: number) => void) => {
  const result = n1 + n2;
  cb(result);
};

// addAndHandle 호출
// 두 숫자와 콜백을 올바르게 전달
// 콜백은 하나의 숫자를 전달받아 콘솔에 출력하는 함수
addAndHandle(10, 20, (result) => {
  console.log(result);
});

// 콜백이 void를 return하도록 type이 정의되어 있어도 특정 값을 return할 수 있음
addAndHandle(10, 20, (result) => {
  console.log(result);
  return true;
});

// addAndHandle을 올바르지 않게 호출(Error)
// 콜백 함수의 타입이 하나의 숫자만 받도록 되어있으나 두 파라미터를 받게 되는 콜백 함수를 할당하여 Error
addAndHandle(10, 20, (result, some) => {
  console.log(result);
});
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

