# 36장. 디스트럭처링 할당

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

* 배열, 이터러블 또는 객체의 구조를 파괴하여 변수에 할당하는 것
* 필요한 값만 추출하여 변수에 할당할 때 유용



## 36.1 배열 디스트럭처링 할당

* 할당 기준은 인덱스
* 할당할 변수에 기본값 설정 가능
  * 할당할 값이 기본값에 우선
* Rest 요소 사용 가능
  * 마지막에 위치해야 함

```JavaScript
const cats  = ['siru', 'nunu', 'mango'];

// 디스트럭처링 할당
const [cat1, cat2, cat3 = 'hoho'] = cats;

// Rest요소
// pet1을 할당 후, 나머지 인덱스들의 요소를 pets에 할당(배열)
const [pet1, ...pets] = cats;
```



## 36.2 객체 디스트럭처링 할당

* 할당 기준을 프로퍼티 키
  * 순서는 의미가 없음
  * 선언된 변수 이름과 프로퍼티 키가 일치하면 할당
  * 다른 변수 명으로도 할당 가능
* Rest 프로퍼티 사용 가능

```JavaScript
const cats = {
  siru : 'siru',
  nunu: 'nunu',
  mango: 'mango',
};

// 디스트럭처링 할당
// Rest 요소
// siru를 할당 후 나머지 인덱스들의 요소를 rest에 할당
const {siru, ...rest} = cats;
```

