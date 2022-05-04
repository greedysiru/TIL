# 37장. Set과 Map(2)



**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 37.2 Map

* 키와 값의 쌍으로 이루어진 컬렉션
* 객체와 유사
  * 키로 객체를 포함한 모든 값 사용 가능
  * 이터러블



### 37.2.1 Map 객체의 생성

* Map 생성자 함수로 생성
  * 인수를 전달하지 않으면, 빈 Map 객체가 생성
  * 인수는 키와 값의 쌍으로 된 요소로 구성된 이터러블을 전달 받아야 함
* 중복된 키를 추가 하면 갚이 덮어써짐

```JavaScript
const mapForCats = new Map([['siru', 'cat'], ['mummum', 'dog']]);
console.log(mapForCats); // Map(2) {'siru' => 'cat', 'mummum' => 'dog'}
```



### 37.2.2 요소 개수 확인

* Map.prototype.size

```JavaScript
const {size} = new Map([['siru', 'cat'], ['mummum', 'dog']]);
console.log(size); // 2
```



### 37.2.3 요소 추가

* Map.prototype.set
  * 연속하여 사용 가능

```JavaScript
const mapForCats = new Map();
mapForCats.set('siru', 'cat');
console.log(mapForCats); // Map(1) {'siru' => 'cat'}
```



### 37.2.4 요소 취득

* Map.prototype.get

```JavaScript
const mapForCats = new Map();
mapForCats.set('siru', 'cat');
console.log(mapForCats.get('siru')); // cat
```



### 37.2.5 요소 존재 여부 확인

* Map.prototype.has

```JavaScript
const mapForCats = new Map();
mapForCats.set('siru', 'cat');
console.log(mapForCats.has('siru')); // true
console.log(mapForCats.has('nunu')); // false
```



### 37.2.6 요소 삭제

* Map.prototype.delete
  * 삭제 성공시 여부를 나타내는 불리언 반환

```JavaScript
const mapForCats = new Map([['siru', 'cat'], ['mummum', 'dog']]);

mapForCats.delete('mummum');
console.log(mapForCats); // Map(1) {'siru' => 'cat'}
```



### 37.2.7 요소 일괄 삭제

* Map.prototype.clear
  * undefined 반환

```JavaScript
const mapForCats = new Map([['siru', 'cat'], ['mummum', 'dog']]);

mapForCats.clear();
console.log(mapForCats); // Map(0) {}
```



### 37.2.8 요소 순회

* Map.prototype.forEach
  * 첫 번째 인수: 현재 순회 중인 요소 값
  * 두 번째 인수 : 현재 순회 중인 요소 키
  * 세 번째 인수 : 현재 순회 중인 Map 객체 자체
* Map 객체는 이터러블 이므로 아래와 같은 이터레이터인 객체 반환 메서드들을 제공
  * Map.prototype.keys : Map 객체의 요소키를 값으로 갖는 이터러블이며 이터레이터인 객체 반환
  * Map.prototype.values : Map 객체에서 요소값을 값으로 갖는 이터러블이며 이터레이터인 객체 반환
  * Map.prototype.entries: Map 객체에서 요소값을 값으로 갖는 이터러블이며 이터레이터인 객체를 반환

```JavaScript
const mapForCats = new Map([['siru', 'cat'], ['mummum', 'dog']]);

mapForCats.forEach((cat) => console.log(cat));
```

