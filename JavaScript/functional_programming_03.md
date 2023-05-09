# 함수형 프로그래밍과 ES6+ - Set, Map을 통해 알아보는 이터러블/이터레이터 프로토콜



**본 내용은 프로그래머스의 함수형 프로그래밍과 ES6+ 강의를 토대로 작성하였습니다.**



## Set, Map을 통해 알아보는 이터러블/이터레이터 프로토콜

### for...of

* array, set, map 각각을 `for...of`로 순회
  * 모든 경우에서 각 요소를 순차적으로 순회 가능
* `for...of` 는 key에 mappinge된 value를 접근하는 방식으로 동작하지 않음

```JavaScript
const arr = [1, 2, 3];
for (const a of arr) console.log(a);
arr[0]; // 1
arr[1]; // 2
arr[2]; // 3

const set = new Set([...arr]);
for (const s of set) console.log(s);
// 인덱스로 요소에 접근이 되지 않음
set[0]; // undefined

const map = new Map([['a', 1], ['b', 2], ['c', 3]]);
for (const m of map) console.log(m);
map[0]; // undefined
```



### Symbol.iterator

* ES6에서 추가된 Symbol
* 객체의 key로 사용
* iterable은 `Symbol.iterator`가 정의되어 있어야 함
  * array
  * set
  * map

```JavaScript
const arr = [1, 2, 3];
arr[Symbol.iterator]; // iterator 함수로 접근 됨
```



### 이터러블/이터레이터 프로토콜

* 이터러블: 이터레이터를 return하는 `[Symbol.iterator()]`를 가진 값
* 이터레이터: value, done을 key로 가진 객체를 리턴하는 next()를 가진 값
  * 길이가 2인 arr의 iterator는 아래와 같이 동작
  * iterator.next() -> {value: 1, done: false}
  * iterator.next() -> {value: 2, done: false}
  * iterator.next() -> {value: undefined, done: true}
* 이터러블/이터레이터 프로토콜: 이터러블을 for ...of, 전개 연산자 등과 함께동작하도록 한 규약
* array, set, map은 JavaScript 빌트인 객체로 이터러블/이터레이터 프로콜을 준수
* map의 keys, values, entries 메서드는 iterator를 return



## Reference

[[프로그래머스] 함수형 프로그래밍과 ES6+](https://school.programmers.co.kr/learn/courses/7637)

