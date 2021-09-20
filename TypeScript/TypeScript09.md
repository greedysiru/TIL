# 타입스크립트 입문 - Promise, 타입 추론

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. Promise를 이용한 API 함수 타입 정의

* Promise는 TypeScript 내부적으로 타입이 정의되어있다.
* Promise를 return하기 위해서는 제네릭을 선언해야 한다.
* Axios는 Promise를 반환하므로 해당 타입 선언을 알아둘 것

```TypeScript
fucntion fetchItems(): Promise<string[]> {
  let items: string[] = ['a', 'b', 'c'];
  return new Promise(fucntion (resolve) {
     reslove(items);
	});
}

fetchItems();
```



## 2. 타입 추론(Type Inference)

### 타입 추론 기본

* 변수를 선언하거나 초기화 할 때 타입이 추론됨
* 변수, 속성, 인자의 기본 값, 함수의 반환 값 등을 설정할 때 타입이 추론됨

```TypeScript
let a = 10; // a에 대한 타입을 따로 지정하지 않아도 10이 할당되어서 변수 a의 타입은 number로 추론 됨

// 함수 기본값 설정
// 파라미터의 기본값은 10이므로 b의 타입은 number
function getB(b = 10) {
  // c의 타입은 string
  let c = 'hi';
  // +연산자의 피연산자 중 문자열(c)가 있으므로 b도 문자열 취급되어 문자열을 return
  return b + c;
}
```



### 인터페이스와 제네릭을 이용한 타입 추론 방식

* 변수를 선언하고 초기화할 때 제네릭을 이용한 인터페이스로 타입을 선언하면, 타입스크립트가 필요한 속성의 타입을 추론해준다.

```TypeScript
interface Dropdown<T> {
  value: T;
  title: string;
}

let shoppingItem: Dropdown<string> = {
  // 제네릭에 의해 value의 타입이 string으로 추론 됨
  value: 'abc',
  title: 'hello'
}
```



### 복잡한 구조에서의 타입 추론 방식

* extends를 이용하여 확장한 인터페이스의 제네릭에서도 타입스크립트가 필요한 속성이 타입을 추론해준다.

```TypeScript
interface Dropdown<T> {
  value: T;
  title: string;
}

// exteds로 정의된 Dropdown을 확장
// K를 넘겨 DetailedDropdown의 tag 타입을 지정
// K를 넘겨 Dropdown의 value의 타입을 지정
interface DetailedDropdown<K> extends Dropdown<K>{
  derscription: string;
  tag: K;
}

// number가 넘겨져서 value와 tag의 타입이 지정됨
let detailedItem: DetailedDropdown<number> = {
  title: 'abc',
  derscription: 'ab',
  value: 7,
  tag: 77
}
```



### 가장 적절한 타입(Best Common Type)

* 타입스크립트가 해당 코드를 어떤 타입인지 해석하는 알고리즘
* 가장 잘 호환이 될 수 있는 타입을 선정

```TypeScript
let arr1 = [1, 2, 3]; // number[]

let arr2 = [1, 2, true, 'a']; // (string | number | boolean)[]
```



### 문맥상의 타이핑(Contextual Typing)

* 코드의 위치(문맥)를 기준으로 일어남

```TypeScript
// window.onmousedown에 할당되는 타입을 추론하므로 마우스 이벤트와 연관이 있어야 함
window.onmousedown = fucntion(mouseEvent) {
  console.log(mouseEvent.button); // OK, 마우스 이벤트와 연관이 있다고 추론
  console.log(mouseEvent.cat); // Error, 마우스 이벤트와 연관이 없다고 추론
}
```





## 3. TypeScript Language Server

* IntelliSense: 코드 자동 완성, 속성, api 규칙들을 보여줌
* node_modules/typescript
  * typescript 관련 파일
  * tsserver: 타입스크립트의 기능을 사용할 수 있도록하는 서버(타입추론 등)



# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)