# 27장. 배열(4)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 27.9 배열 고차 함수

### 27.9.4 Array.prototype.filter

* 모든 요소를 순회하며, 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열 반환
  * 특정 요소만 추출
* filter 메서드가 생성하여 반환한 새로운 배열의 length는 원본 배열의 length보다 같거나 작음
* 원본 배열은 변경되지 않음

```JavaScript
const pats = [
  {name: 'siru', isCat: true, isDog: false},
  {name: 'dangdangi', isCat: false, isDog: true},
  {name: 'nunu', isCat: true, isDog: false},
  {name: 'nari', isCat: false, isDog: true},
];

// pats 배열에서 isCat이 true 즉, 고양이인 경우만 추출
const onlyCats = pats.filter(pat => pat.isCat);
/*
[
  { name: 'siru', isCat: true, isDog: false },
  { name: 'nunu', isCat: true, isDog: false }
]
*/
```



### 27.9.5 Array.prototype.reduce

* 자신을 호출한 배열의 모든 요소를 순회하며 전달 받은 콜백 함수 반복 호출
  * 콜백함수의 반환 값을 다음 순회 시에 첫 번째 인수로 전달 받아 하나의 결과값을 만들어 반환
* 첫 번째 인수 : 콜백 함수
* 두 번째 인수 : 초기값
  * 기본값은 0이나, 전달하는 것이 안전
* 콜백 함수에는 4개의 인수를 전달
  * 이전 반환 값
  * 배열의 요소값
  * 인덱스
  * 배열 자체

```JavaScript
// 모든 고양이들의 나이 합을 구하기
const cats = [
  {name: 'siru', age: 7},
  {name: 'nunu', age: 6},
  {name: 'mango', age: 4},
  {name: 'meonji', age: 3},
];

const ageForSum = cats.reduce((acc, cur) => acc + cur.age, 0); // 20
```



### 27.9.6 Array.prototype.some

* 콜백 함수의 반환값이 단 한번이라도 참이면 true, 모두 거짓이면 false
* 콜백함수에서 정의한 조건을 만족하는 요소가 1개 이상 존재하면 불리언 타입으로 변환

```JavaScript
const pats = [
  {name: 'siru', isCat: true, isDog: false},
  {name: 'dangdangi', isCat: false, isDog: true},
  {name: 'nunu', isCat: true, isDog: false},
  {name: 'nari', isCat: false, isDog: true},
];

// pats 배열에서 isCat이 하나라도 true 즉, 하나라도 고양이인지 확인
pats.some(pat => pat.isCat); // true
```



### 27.9.7 Array.prototype.every

* 콜백함수에서 정의한 조건을 호출한 배열에서 모두 만족하는 지 검사
  * 단, 호출한 배열이 빈 배열이면 언제나 true를 반환

```JavaScript
const pats = [
  {name: 'siru', isCat: true, isDog: false},
  {name: 'dangdangi', isCat: false, isDog: true},
  {name: 'nunu', isCat: true, isDog: false},
  {name: 'nari', isCat: false, isDog: true},
];

// pats 배열에서 isCat이 모두 true 즉, 모두 고양이인지 확인
pats.every(pat => pat.isCat); // false
```



### 27.9.8 Array.prototype.find

* 콜백 함수를 만족하는 첫 번째 요소 반환
* 존재하지 않으면 undefined를 반환

```JavaScript
const pats = [
  {name: 'siru', isCat: true, isDog: false, isMine: true},
  {name: 'dangdangi', isCat: false, isDog: true, isMine: false},
  {name: 'nunu', isCat: true, isDog: false, isMine: false},
  {name: 'nari', isCat: false, isDog: true, isMine: false},
]

pats.find(pat => pat.isMine); // {name: 'siru', isCat: true, isDog: false, isMine: true}
```



### 27.9.9 Array.prototype.findIndex

* 콜백 함수를 만족하는 첫 번째 인덱스 반환
* 만족하는 요소가 없으면 -1을 반환

```JavaScript
const pats = [
  {name: 'siru', isCat: true, isDog: false, isMine: true},
  {name: 'dangdangi', isCat: false, isDog: true, isMine: false},
  {name: 'nunu', isCat: true, isDog: false, isMine: false},
  {name: 'nari', isCat: false, isDog: true, isMine: false},
]

pats.findIndex(pat => pat.isMine); // 0
```



### 27.9.10 Array.prototype.flatMap

* ES10에서 도입
* map 메서드를 통해 생성된 새로운 배열 평탄화
* 1단계만 평탄화 가능

```JavaScript
const sirubabo = ['siru', 'babo'];

sirubabo.flatMap(x => x.split(''));
/*
['s', 'i', 'r', 'u', 'b', 'a', 'b', 'o' ]
*/
```

