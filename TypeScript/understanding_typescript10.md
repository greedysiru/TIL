# Understanding TypeScript(10) - The "any" Type

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## The "any" Type

### any

* 가장 유연한 타입
* 어떤 타입이든 해당하는 타입
* 사용을 지양
  * Vanila JavaScript를 사용하는 것과 다름이 없음

```TypeScript
// any 타입이 지정된 변수는 어떤 타입이든 할당할 수 있음
let anything: any = '';
anything = 1;
anything = 'Hi';
anything = {
  hey: 'do not use any type'
};
anything = ['bad'];
```




# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

