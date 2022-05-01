# 35장. 스프레드 문법

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



* 하나로 뭉쳐 있는 여러 값들의 집합을 펼침
* Array, String, Map, Set, DOM Collection, arguments와 같은 이터러블에 한정되어 사용 가능
* 스프레드 문법의 결과는 값이 아니므로 값으로 사용할 수 없음
  * 변수에 할당 불가능



## 35.1 함수 호출문의 인수 목록에서 사용하는 경우

* 배열과 같은 이터러블을 펼쳐서 개별적인 값들의 목록을 만듦

```JavaScript
const numbers = [10, 2, 3, 8, 7, 77];

const maxNumber = Math.max(...numbers);

console.log(maxNumber); // 77
```



## 35.2 배열 리터럴 내부에서 사용하는 경우

### 35.2.1 concat

```JavaScript
// concat 메서드
const cats = ['siru', 'nunu'].concat(['mango', 'meonji']);
console.log(cats); // ['siru', 'nunu', 'mango', 'meonji']

// 스프레드 문법
const casts = [...['siru', 'nunu'], ...['mango', 'meonji']];
console.log(cats); // ['siru', 'nunu', 'mango', 'meonji']
```



### 35.2.2 splice

```Javascript
const cats1 = ['siru', 'nunu'];
const cats2 = ['mango', 'meonji'];

// splice 메서드
cats1.splice(1, 0, cats2); // ['siru', ['mango', 'meonji'], 'nunu']

// 스프레드 문법
casts1.splice(1, 0, ...cats2); // ['siru', 'mango', 'meonji', 'nunu']
```



### 35.2.3 배열 복사

```JavaScript
const casts = ['siru', 'nunu', 'mango', 'meonji'];
const copyForCats = [...cats];

console.log(copyForCats); // ['siru', 'nunu', 'mango', 'meonji']
console.log(cats === copyForCats); // false
```



### 35.2.4 이터러블을 배열로 변환

* 간편하게 이터러블을 배열로 변환 가능

```JavaScript
function callCats() {
  console.log([...arguments]);
}

callCats('siru', 'nunu', 'mango', 'meonji'); // ["siru", "nunu", "mango", "meonji"]
```



### 35.3 객체 리터럴 내부에서 사용하는 경우

* 객체 리터럴의 프로퍼티 목록에서도 스프레드 문법 사용 가능
  * 스프레드 프로퍼티 제안
* 스프레트 프로퍼티를 활용하여 객체 병합, 변경 및 추가 가능

```javascript
const cats1 = {siru: 1, nunu: 2};
const cats2 = {mango: 10, meonji: 20};

const mergedCasts = { ...cats, ...cats2};

const chagedCats1 = {...cats1, siru: 77};

const addedCats2 = {...cats2, kuku: 11};
```

