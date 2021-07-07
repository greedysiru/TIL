# [드림코딩 by 엘리] 자바스크립트 최신 문법(ES6, ES11)

**상세 내용 [블로그](https://greedysiru.tistory.com/598) 참고**



# ES6

## 1. Shorthand property names

* object에서 key와 value의 이름이 동일한 경우 축약해서 표현할 수 있다.

```JavaScript
const name = 'siru';
const age = '3';

const siruObject = {
  name,
  age,
};
```



## 2. Destructuring assignment

* object에 할당된 key의 value를 중괄호를 사용하여 바로 가져올 수 있다.
  * 중괄호안의 변수 명은 key의 이름과 같아야 한다.
  * 콜론(:)을 사용하여 원하는 이름으로 바꿀 수 있다.
* 배열에서도 사용할 수 있다.

```JavaScript
// object
const siruObject = {
  name: 'siru',
  age: '3',
};

const {name, age} = siruObject;
cosnt {name: catName, age: catAge} = siruObject;

// array
const animals = ['dog', 'cat'];
const [first, second] = animals;
```



## 3. Spread Syntax

* array 또는 object의 item을 각각 낱개로 가져올 수 있다.
  * 간단하게 복사하고, 복사한 요소와 함께 다른 요소를 추가할 수 있다.
  * 두 array 또는 object를 병합 할 수 있다.
  * object에서 key가 동일하다면, 마지막에 온 key의 value가 덮어씌워진다.
  * 주소의 참조값만 복사한다.

```JavaScript
const obj1 = { key: 'key1'};
const obj2 = { key: 'key2'};
const array = [obj1, obj2];

// array copy
const arrayCopy = [...array];

// object copy
const obj3 = {...obj1};

// 병합
const fruits1 = ['apple', 'grape'];
const fruits2 = ['banana', 'kiwi'];

const fruits = [...fruits1, ...fruits2];
```



## 4. Default parameters

* parameter의 초기값을 설정할 수 있다.

```JavaScript
function printMessage(message = 'hi'){
  console.log(message);
}
// parameter를 전달하지 않아도 기본값인 hi가 출력된다.
printMessage();
```



## 5. Ternary Operator

* boolean에 따른 값을 할당할 수 있다.

```JavaScript
const component = isCat ? 'cat' : 'dog';
```



## 6. Template Literals

* 문자열과 변수를 간편하게 작성할 수 있다.

```JavaScript
const catName = 'siru'
const message = `my pet name is ${catName}`
```



# ES11

## 1. Optional chaining

* Object property가 존재할 때 접근
  * 없으면 접근하지 않는다.

```JavaScript
const person1 = {
  name: 'greedysiru',
  job: {
    title: 'S/W Engineer',
    manager: {
      name: 'Ellie',
    },
  },
};

const person2 = {
  name: 'siru',
};

// Optinal chaining
function printManager(person){
  console.log(person.job?.manager?.name);
}
printManager(person1);
printManager(person2);
```



## 2. Nullish Coalescing Operator

### 기존 코드 작성 방식

* JavaScript에서 false 취급하는 것들
  * false, '', 0, null, undefined

```JavaScript
{
  const name = 'siru';
  const userName = name || 'Guest';
  // name이 있으므로 'siru'가 출력
  console.log(userName);
}

{
  const name = null;
  const userName = name || 'Guest';
  // name이 false이므로 'Guest'가 출력
  console.log(userName);
}
```

* 버그: name에 null이 아닌  '', 0, undefined인 경우에도 아래처럼 Guest가 할당된다.



### Nullish Coalescing Operator

* 주어진 변수가 null일 때만 false 취급

```JavaScript
const naume = '';
const userName = name ?? 'Guest';
console.log(userName);

const num = 0;
const message = num ?? 'undefined';
console.log(message);
```



# Reference

[자바스크립트 최신 문법 (ES6, ES11)](https://www.youtube.com/watch?v=36HrZHzPeuY&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=23)