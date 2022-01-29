# JavaScript - async & await

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. async & await

* JavaScript 비동기 패턴 처리 문법
* Promise보다 더 직관적으로 사용할 수 있음
  * 문법적 설탕



## 2.  사용조건

* 함수 선언문 앞에 async가 붙어야 함
* 함수 안에서 비동기 처리를 위해서 Promise를 반환하는 로직 앞에 await를 붙여야 함



## 3. 예시

```JavaScript
function getPetName() {
  return new Promise(function(resolve, reject) {
    const petName = 'siru';
    resolve(petName);
  })
}

async function fetchPetInfo() {
  // Promise를 반환하는 로직
  const petName = await getPetName();
  return petName;
}
```







# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

