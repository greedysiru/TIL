# 13장 - 스코프(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 13.2 스코프의 종류

* 전역 스코프: 코드의 가장 바깥 영역 스코프
* 지역 스코프: 블록 영역 스코프



### 13.2.1 전역과 전역 스코프

* 전역 스코프에서 선언된 전역 변수(식별자)는 어디서든지 참조할 수 있음

```JavaScript
const petName = 'siru';

function callPetName() {
  console.log(petName); // siru
}
```



### 13.2.2 지역과 지역 스코프

* 블록 몸체 내부를 말함
* 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효
* 상위 스코프에서 하위 지역 스코프를 참조할 수 없음
* 자바스크립트 엔진이 스코프 체인을 통해 참조할 변수를 검색

```JavaScript
{
const petName = 'siru';

console.log(petName); // siru
}

console.log(petName); // ReferenceError
```

