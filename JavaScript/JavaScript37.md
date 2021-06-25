# [드림코딩 by 엘리] JavaScript 기초 강의(7) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/544) 참고**



# 자료구조

* 비슷한 종류의 데이터들을 묶어서 한데다가 보관하는 것
* 방식, 형식에따라 다양한 자료구조가 있음
* cf) Object
  * 서로 연관된 특징과 행동들을 묶어놓는 것
  * JavaScript는 다양한 종류의 데이터를 담을 수 있다.

# Array

* 0부터 시작하는 인덱스 번호가 있는 자료구조
* 한 배열에는 동일한 배열을 넣어야 한다.
* 인덱스로 접근할 수 있다.
* 삽입과 삭제가 편함



## 1. Declaration

```JavaScript
const arr1 = new Array();
const arr2 = [1, 2];
```



## 2. Index position

```javascript
const fruits = ['apple', 'banana'];
console.log(fruits.length); // 2
console.log(fruits[0]); // apple
console.log(fruits[1]); // banana
```

* index는 0부터 시작



## 3. Lopping over an array

```JavaScript
const fruits = ['apple', 'banana'];

// for loop
for (let i = 0; i < fruits.length ; i++){
  console.log(fruits[i]);
}

// for of
for (let fruit of fruits) {
  console.log(fruit);
}

// forEach
fruits.forEach(fruit => console.log(fruit, index));
```



## 4. Addition, Deletion, Copy

### push

* 맨 뒤에 요소를 추가

```JavaScript
const fruits = ['apple', 'banana'];
fruits.push('pineapple', 'peach');
```



### pop

* 맨뒤의 요소를 빼서 return

```JavaScript
const fruits = ['apple', 'banana'];
console.log(fruits.pop()); // banana
```



### unshift

* 맨 앞에 요소를 추가

```JavaScript
const fruits = ['apple'];
fruits.unshift('banana');
```



### shift

* 앞에서부터 요소를 빼서 return

```JavaScript
const fruits = ['banana', 'apple'];
console.log(fruits.shift()); // banana
```



### unshift, shift

* push와 pop보다 매우 느림
  * 뒤에서 넣거나 지우는 것은 기존 빈공간을 다루는 것이므로 빠르다.
* 앞에서 데이터를 넣게 되면, 그 뒤의 데이터는 앞에 빈공간을 만들기 위해서 밀리거나 당겨져야 한다.
  * 전체 데이터 -1 만큼 움직여야 한다.
* pop, push 사용을 권장
* 중간에 데이터를 넣고 빼는 것은 인덱스를 활용하므로 빠르다.



### splice

* 지정된 인덱스의 요소를 지울 수 있다.
* 몇 개를 지울 것인지를 쓸 수 있다(생략가능)
  * 생략한 경우, 그 인덱스로부터 모든 데이터를 삭제
* 3번째 파라미터부터 넣을 요소를 전달할 수 있다.

```JavaScript
const fruits = ['banana', 'apple'];
fruits.push('orange', 'kiwi');
// 시작 인덱스 ~ 몇개를 지울 것인지(생략 가능)
fruits.splice(1, 1); 
fruits.splice(2, 1, 'melon');
```



### 두가지 배열 연결

```JavaScript
const fruits1 = ['apple', 'kiwi'];
const fruits2 = ['orange', 'banana'];
newFruits = fruits.concat(fruits2);
console.log(newFruits); // ['apple', 'kiwi', 'orange', 'banana'];
```



## 5. Searching

### indexOf

* 앞에서부터 값이 배열의 몇번째 인덱스에 있는지 return
* 해당 값이 없으면 -1 return

```JavaScript
const fruits = ['apple', 'banana'];
console.log(fruits.indexOf('banana')); // 1
```



### includes

* 값이 배열에 존재하는 boolean을 return

```JavaScript
const fruits = ['apple', 'banana'];
console.log(fruits.includes('melon')) // false
```



### lastIndexOf

* 뒤에서부터 배열의 요소 검색하여 인덱스 return

```JavaScript
const fruits = ['apple', 'banana', 'apple'];
console.log(fruits.lastIndexOf('apple')); // 2
```



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)