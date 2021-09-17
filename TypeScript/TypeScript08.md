# 타입스크립트 입문 - 제네릭

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 제네릭이란

* C#, Java 등의 언어에서 재사용성이 높은 컴포넌트를 만들 때 자주 활용
* 여러가지 타입에 동작하는 컴포넌트를 생성하는데 사용



### 기본 문법

```TypeScript
function logText<T>(text: T):T {
  console.log(text);
  return text;
}

// 함수 호출 시 파라미터의 타입을 지정할 수 있음
// 문자열이 들어가면 문자열이 반환
// 호출 시점에 타입을 넘겨줌
logText<string>('Hi');
```



## 2. 기존 문법과 제네릭의 차이

### 함수 중복 선언의 단점

```TypeScript
// 유지 보수 관점에서 좋지 않다.
// 타입을 받기 위해서 중복되는 코드
// 가독성이 떨어지고 전체 코드가 비대해진다.
function logText(text: string) {
  console.log(text);
  return text;
}

function logNumber(num: number) {
  console.log(num);
  return num;
}
```



### 유니온 타입을 이용한 선언 방식의 단점

* 유니온 타입을 사용하면 좀 더 유연한 타입 선언을 할 수 있지만 한계가 있다.
* 파라미터가 유니온 타입으로 선언된 함수 내부에서 해당 파라미터의 접근 가능한 api는 유니온 타입들의 교집합이다.
  * 반환값을 할당하여도 이와 같다.

```TypeScript
function logText(text: string | number) {
  console.log(text);
  // string과 number에서 공통적으로 사용할 수 있는 api만 접근 가능
  
  return text;
}

// 리턴된 텍스트를 반환하여 변수 a에 할당
const a = logText('a');
// 문자열 api에 접근할 수 없다.
a.split(''); // error
```



### 제네릭의 장점과 타입 추론에서의 이점

* 제네릭은 함수 호출시에 파라미터의 타입을 지정할 수 있다.
* 타입이 추론되어 타입에 해당하는 api에 접근할 수 있다.

```TypeScript
function logText<T>(text: T): T {
  console.log(text);
  return text;
}

const str = logText<string>('text');
str.split(''); // api 접근 가능

const flag = logText<boolean>(true);
```



## 3. 제네릭 실전 예제

### interface로 타입 선언하기

* 필요한 인터페이스를 매번 선언해야 하는 단점이 있음

```TypeScript
interface Email {
  value: string;
  selected: boolean;
}

const emails: Email[] = [
  { value: 'naver.com', selected: true },
  { value: 'gmail.com', selected: false },
  { value: 'hanmail.net', selected: false },
];

interface ProductNumber {
  value: number;
  selected: boolean;
}

const numberOfProducts: ProductNumber[] = [
  { value: 1, selected: true },
  { value: 2, selected: false },
  { value: 3, selected: false },
];

// Email 또는 ProductNumber 인터페이스를 파라미터로 받을 수 있음
function createDropdownItem(item: Email | ProductNumber) {
  const option = document.createElement('option');
  option.value = item.value.toString();
  option.innerText = item.value.toString();
  option.selected = item.selected;
  return option;
}

// NOTE: 이메일 드롭 다운 아이템 추가
emails.forEach(function (email) {
  const item = createDropdownItem(email);
  const selectTag = document.querySelector('#email-dropdown');
  selectTag.appendChild(item);
});

numberOfProducts.forEach(function (product) {
  const item = createDropdownItem(product);
})
```



### 인터페이스에 제네릭 선언하기

* 인터페이스를 선언할 때 꺽쇠(<>) 안에 타입을 넘기도록 할 수 있다.

```TypeScript
// T라는 타입을 value의 타입으로 지정
interface Dropdown<T> {
  value: T;
  selected: boolean;
}

// string을 넘겨서 value가 string 타입을 받도록 함
const obj: Dropdown<string> = {
  value: 'hi',
  selected: true,
};

// number를 넘겨서 vlaue가 number 타입을 받도록 함
const numberObj: Dropdown<number> = {
  value: 10,
  selected: false,
}
```





### 제네릭으로 타입 선언하기

* 제네릭을 활용하여 여러 상황에서의 타입을 유연하게 선언할 수 있음
* 타입 코드를 줄일 수 있다.

```TypeScript
// 인터페이스에 제네릭을 적용하여 타입 적용 시점에서 받은 T를 value의 타입이 되도록 함
interface Dropdown<T> {
  value: T;
  selected: boolean;
}

// emails의 value는 string 타입을 가지게 됨
const emails: Dropdown<string>[] = [
  { value: 'naver.com', selected: true },
  { value: 'gmail.com', selected: false },
  { value: 'hanmail.net', selected: false },
];

// numberOfProducts의 value는 number 타입을 가지게 됨
const numberOfProducts: Dropdown<number>[] = [
  { value: 1, selected: true },
  { value: 2, selected: false },
  { value: 3, selected: false },
];

// createDropdwonItem 함수는 호출시에 T를 넘겨 다시 인터페이스 Dropdown에 T를 넘기게 됨
function createDropdownItem<T>(item: Dropdown<T>) {
  const option = document.createElement('option');
  option.value = item.value.toString();
  option.innerText = item.value.toString();
  option.selected = item.selected;
  return option;
}

// 아래처럼 다양한 타입에서 함수를 호출하여도 제네릭으로 인해 타입 코드는 줄이고 유연성은 높일 수 있음
emails.forEach(function (email) {
  const item = createDropdownItem<string>(email);
  const selectTag = document.querySelector('#email-dropdown');
  selectTag.appendChild(item);
});


numberOfProducts.forEach(function (product) {
  const item = createDropdownItem<number>(product);
})

```



## 4. 제네릭의 타입 제한

### 타입에 대한 힌트 주기

* 아래와 같이 어떤 타입이 들어올 지 예상할 수 없을 때 api에 접근할 수 없다.

```TypeScript
// 제네릭의 타입 제한
function logTextLength<T>(text: T): T {
  console.log(text.length); //Error 어떤 타입이 들어올 지 알 수 없으므로 해당 api에 접근 불가
  return text;
}

logTextLength<string>('hi');
```

* 위와 같은 문제를 방지하기 위해서 어느정도의 타입에 대한 힌트를 넘겨 api를 접근 토록 할 수 있다.
  * but. 파라미터가 제한될 수 있음

```TypeScript
// 제네릭의 타입 제한
function logTextLength<T>(text: T[]): T[] {
  console.log(text.length);
  return text;
}

logTextLength<string>('hi'); // 배열이 아니므로 error
```



### 정의된 타입으로 타입 제한하기

* 정의된 타입을 확장해서 제네릭 타입을 제한할 수 있다.

```TypeScript
// number 타입의 length 프로퍼티를 가지는 인터페이스
interface LengthType {
  length: number;
}

// 제네릭이 받는 타입은 LengthType의 확장이므로 함수 내부에서 해당 프로퍼티에 접근 가능
function logTextLength<T extends LengthType>(text: T): T {
  text.length;
  return text;
}

// 숫자, 배열, 객체 파라미터로 사용 가능
logTextLength('A');

logTextLength([1, 2, 3]);

logTextLength({length: 10});
```



### keyof로 제네릭의 타입 제한하기

* keyof를 이용하여 인터페이스의 key중 한가지만 사용하도록 제한할 수 있음

```TypeScript
interface ShoppingItem {
  name: string;
  price: number;
  stock: number;
}

// ShoppingItem의 한 가지 키만 제네릭으로 받도록 제약
function getShoppingItemOption<T extends keyof ShoppingItem>(itemOption: T): T {
  return itemOption;
}

getShoppingItemOption<number>(10); // Error

getShoppingItemOption<string>('item'); // Error

getShoppingItemOption('name'); // ShoppingItem의 key이므로 사용 가능

getShoppingItemOption('a'); // Error ShoppingItem의 key에 속하지 않음
```



# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)