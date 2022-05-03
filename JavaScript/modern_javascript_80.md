# 37장. Set과 Map(1)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 37.1 Set

* 중복되지 않는 유일한 값들의 집합
* 배열과 유사
  * 중복 x
  * 순서 x
  * 인덱스 x
* 수학적 집합의 특성과 일치
* 교집합, 합집합, 차집합, 여집합 등을 구현 가능



### 37.1.1 Set 객체의 생성

* Set 생성자 함수로 생성
  * 인수를 전달하지 않으면 빈 Set 객체가 생성
* 활용하여 중복된 요소 제거 가능

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji', 'siru'];

const setForCats = new Set(cats);
console.log(setForCats); // Set(4) {'siru', 'nunu', 'mango', 'meonji'}

const uniqForCats = [...setForCats];
console.log(uniqForCats); // ['siru', 'nunu', 'mango', 'meonji']

// 중복된 요소가 제거된 배열로 변환 가능

const setForSiru = new Set('siru');
console.log(setForSiru); // Set(4) {'s', 'i', 'r', 'u'}
```



### 37.1.2 요소 개수 확인

* size 프로퍼티로 개수 확인 가능
* getter 함수만 존재하는 접근자 프로퍼티
  * 다른 숫자를 할당하여 개수 변경 불가

```JavaScript
const {size} = new Set([1, 2, 2, 2]);
console.log(size); // 2
```



### 37.1.3 요소 추가

* Set.prototype.add
  * 연속 호출 가능
* 중복된 요소 추가는 허용되지 않음
  * 에러가 발생하지 않고 무시

```JavaScript
const setForCats = new Set();
setForCats.add('siru').add('nunu');

console.log(setForCats); // Set(2) {'siru', 'nunu'}
```



### 37.1.4 요소 존재 여부 확인

* Set.prototype.has
  * 특정 요소의 존재 여부를 나타내는 불리언 값 반환

```JavaScript
const setForCats = new Set(['siru', 'nunu', 'mango']);

console.log(setForCats.has('siru')) // true
console.log(setForCats.has('meonji')) // false
```



### 37.1.5 요소 삭제

* Set.prototype.delete

```JavaScript
const setForCats = new Set(['siru', 'nunu', 'mango']);

setForCats.delete('mango');
console.log(setForCats); // Set(2) {'siru', 'nunu'}
```



### 37.1.6 요소 일괄 삭제

* Set.prototype.clear
  * undefined 반환

```JavaScript
const setForCats = new Set(['siru', 'nunu', 'mango']);

setForCats.clear();
console.log(setForCats); // Set(0) {size: 0}
```



### 37.1.7 요소 순회

* Set.prototype.forEach
  * 첫 번째 인수: 현재 순회 중인 요소값
  * 두 번째 인수: 현재 순회 중인 요소값
  * 세 번째 인수: 현재 순회 중인 Set 객체 자체
  * 첫 번째 인수 === 두 번째 인수
  * Array.prototype.forEach 메서드와 인터페스 통일하기 위함

```JavaScript
const setForCats = new Set(['siru', 'nunu', 'mango', 'meonji']);

setForCats.forEach((cat) => console.log(cat));
```