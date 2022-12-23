# 클린코드 자바스크립트 - 분기 다루기(Truthy & Falsy)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 암묵적 타입 변환

* JavaScript는 동적인 언어
  * 암묵적 타입 변환이 일어남
  * 어떠한 값을 특정 조건에 따라 ture 또는 flase와 같은 boolean으로 형 변환




## 2. Truthy

* 암묵적 타입 변환이 일어났을 때 참으로 변환되는 값
* 참으로 평가되는 값



### Truthy로 평가되는 값들

```JavaScript
if (true)
if ({})
if ([])
if (42)
if ("0")
if ("false")
if (new Date())
if (-42)
if (12n)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)
```



## 3. Falsy

* 암묵적 타입 변환이 일어났을 때 거짓으로 변환되는 값
* 거짓으로 평가되는 값



### Falsy로 평가되는 값들

```JavaScript
if (false)
if (null)
if (undefined)
if (0)
if (-0)
if (0n)
if (NaN)
if ("")
```



## 3. Truthy & Falsy 응용

* Truthy & Falsy 앞에 부정 연산자(`!`)를 붙일 수 있음
* 임의의 변수에 문자열이 들어왔는지 없는지 체크할 때 Truthy & Falsy를 응용할 수 있음

```JavaScript

const callCat = (catName) => {
  // catName에 문자열이 들어오면 Turthy
  // catName에 빈문자열, null, undefined가 할당되어 있으면 Falsy
  
  // Falsy이면 아래 로직을 실행
  if (!catName) {
    return '고양이가 없어';
  }
  
  return `이리온, ${catName}`;
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

[[MDN] Truthy](https://developer.mozilla.org/ko/docs/Glossary/Truthy)

[[MDN] Falsy](https://developer.mozilla.org/ko/docs/Glossary/Falsy)
