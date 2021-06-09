# [드림코딩 by 엘리] JavaScript 기초 강의(6) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/516) 참고**



# Objects

* JavaScript의 데이터 타입 중 하나
* 관련된 데이터 또는 함수의 모음
* JavaScript에서 거의 모든 Object는 Object의 instance
* 간편하게 데이터를 관리할 수 있다.
* **key(property)와 value의 집합체**



## Literals and properties

```JavaScript
// object literal syntax
const obj1 = {};
// object constructor syntax
const obj2 = new Object();
// class가 없어도 바로 중괄호로 초기화 가능
const obj3 = { name: 'siru', age: 4};
// 아래와 같이 property를 추가할 수 있다.
obj3.hasJob = true;
// 삭제도 가능
delete obj3.hasJob;
```

* JavaScript는 동적으로 type이 Runtime(프로그램 동작 시점)때 결정된다.
  * 그러므로, 위 처럼 뒤늦게 property를 추가/삭제할 수 있다.
  * 당장 사용하기는 편하지만 유지, 보수에 좋지 않고 예기치 못한 오류를 발생시킬 수 있다.



## Computed properties

```Javascript
obj = { name : 'siru'};
// dot
console.log(obj.name); // siru
// computed properties로 접근
console.log(obj['name']); // siru
// computed properties로 추가
obj['hasJob'] = true;
console.log(obj.hasJob); // true

// Computed properties를 사용해야할 때
function printValue1(obj, key) {
  console.log(obj.key);
}
printValue1(obj, 'name'); // undefined
// obj에 key라는 property가 없으므로 undefined가 나온다.

function printValue2(obj, key) {
  console.log(obj[key]);
}
printValue2(obj, 'name'); // siru
// 정상적으로 출력된다.
```

* Computed properites로 접근 시, string으로 지정하여야 한다.
* dot을 사용하는 경우
  * 코딩하는 순간 key의 값을 가져오고 싶을 때
* Computed properties를 사용하는 경우
  * 정확히 어떤 key가 필요한지 모를 때
  * Runtime에서 결정될 때



## Property value shorthand

* key와 value가 바로 짝지어진다면 :을 생략할 수 있다.

```JavaScript
const person1 = { name: 'siru', age: 4 };
const person2 = { name: 'jm', age: 20 };
const person3 = makePerson('jjm', age: 21 );
console.log(person3); // {name: 'jjm', age: 30};
// Constructor function
function makePerson( name, age ) {
  return {
    // Property value shorthand
    name,
    age
  };
}
```



## Constructor function

* 다른 계산을 하지 않고 순수하게 object만을 생성하는 함수
* class(template)의 역할
* JavaScript에 class가 없었을 때 사용
* 함수명은 대문자로 시작

```JavaScript
const person1 = new Person('siru', 4);
function Person(name, age){
  // this = {};
  this.name = name;
  this.age = age;
  // return this;
}
```



## in operator

* 해당하는 object 안에 key가 있는지 확인
  * key in obj

```JavaScript
const person = {name: 'siru'};
console.log('name' in person); // true
```



## for...in vs for...of

### for...in

* in 뒤의 object의 각 key들이  in 앞의 지역변수에 할당된다.

```JavaScript
pet = { name: 'siru', age: 4, what: 'cat'};
// for (key in obj)
for (key in person) {
  console.log(key); // name, age, what
}
```



### for...of

* 배열과 같이 순차적으로 iterable할 때 사용

```JavaScript
const array = [1, 2, 3, 4, 5];
for (value of array){
  console.log(vlaue);
}
```



## cloning

### cloning이 되지 않는 예시

```JavaScript
const user = { name: 'siru', age: 4};
const user2 = user;
user2.name = 'coder';
console.log(user); // {name: 'coder', age: 4};
```

* 위 코드에서, user는 reference를 가르키고 있다.
  * reference는 name: 'siru', age: 4인 object를 가르키고 있다.
* user2는 user와 동일한 reference의 값이 할당된다.
  * reference가 같으므로 동일한 object를 가르키고 있다.
* user2의 name property를 다른 값으로 변경한다.
  * 원본인  user의 name 또한 해당 값으로 변경된 것이 확인된다.



### Cloning 예시

###  old way

```JavaScript
const user = { name: 'siru', age: 4};
const user2 = {};
for (key in user) {
  user2[key] = user[key];
}
```

* 원본 user를 user2로 복사할 수 있다.



###  new way

* **Object.assign**
  * Object는 JavaScript에 기본 적으로 탑재된 object
  * JavaScript의 모든 object는 Object를 상속

 ```JavaScript
 const user = { name: 'siru', age: 4};
 const user2 = {}
 Object.assign(user2, user);
 // 또는
 user3 = Object.assign({}, user);
 ```



#### 다른 예시

```JavaScript
const fruit1 = { color: 'red' };
const fruit2 = { color: 'blue', size: 'big' };
const mixed = Object.assign({}, fruit1, fruit2);
console.log(mixed.color); // blue
console.log(miexed.size); // big
```

* 뒤로 나온 property가 앞의 것을 덮어 씌운다.



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)