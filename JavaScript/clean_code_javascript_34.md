# 클린코드 자바스크립트 - 배열 다루기(Continue & Break)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Continue & Break

* 특정 문의 흐름을 제어
* continue: 아래의 실행 흐름을 진행하지 않고 반복문의 다음 단계를 실행
* break: 반복문을 종료

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji', 'nago'];

// continue
for (let i = 0; i < cats.length; i++) {
  const cat = cats[i];
  
  // cat이 nunu일 경우, 아래의 실행 흐름을 진행하지 않고 다음 루프를 진행
  if (cat === 'nunu') {
    continue;
  }
  
  console.log(cat); // siru mango meonji nago
}

for (let i = 0; i < cats.length; i++) {
  const cat = cats[i];
  
  // cat이 nunu일 경우, 반복문 자체를 중단
  if (cat === 'nunu') {
    break;
  }
  
  console.log(cat); // siru
}
```



### 고차함수에서

* forEach, map, reduce, filter와 같은 배열 고차함수에서는 동작하지는 않음
  * Syntax Error 발생
  * try, catch 구문 사용하여 특정 조건에 에러를 던지기
  * 또는 for, for of, for in 문으로 대체
* every, some, find, findIndex의 경우 조기에 반복을 종료할 수 있음



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

