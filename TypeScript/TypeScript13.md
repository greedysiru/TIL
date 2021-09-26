# 실전으로 배우는 타입스크립트 - 맵드 타입

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 맵드 타입이란?

* Mapped Type
* 기존에 정의되어 있는 타입을 새로운 타입으로 변환해주는 문법
* 자바스크립트의 map API 함수를 타입에 적용한 것과 같은 효과
  * 배열의 각 요소를 순회하여 조작할 수 있음



### 맵드 타입의 기본 문법

```TypeScript
{ [ P in K ] : T }
{ [ P in K ]? : T }
{ readonly [ P in K ] : T }
{ readonly [ P in K ] ? : T }
```



## 2. 맵드 타입 예제

```TypeScript
// 타입 별칭
type Heroes = 'Hulk' | 'Capt' | 'Thor'

// 기존 타입을 맵드 타입을 이용해서 새로운 타입으로 변환
// Heroes에 지정된 타입을 하나씩 순회하며 number 타입을 지정
type HeroAges = { [K in Heroes]: number }

const ages: HeroAges = {
  Hulk: 33,
  Capt: 100,
  Thor: 1000,
}
```







# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)