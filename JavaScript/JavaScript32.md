# [드림코딩 by 엘리] JavaScript 기초 강의(2) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/503) 참고**



## variable

* 변수: 변경될 수 있는 값

### let

* ES6에서 추가된 변수 선언 키워드
* Mutable
* var
  * 그 이전에 사용하였던 변수 선언 키워드
  * 사용하지 말 것
  * 선언 전에 값을 할당한다거나, 출력할 수 있어 예상치 못한 오류 발생의 원인이 되기 쉬움(var hoisting)
  * Block scope가 없음

```JavaScript
let name = 'jaemin';
console.log(name); // jaemin 출력
name = 'siru';
console.log(name); // siru 출력
```

* 메모리: 애플리케이션마다 사용할 수 있는 메모리가 할당되어 있음
* let을 사용해서 변수를 정의하게 되면 메모리 한 부분을 가르킬 수 있는 포인터가 생김
* 추후, 다른 값을 넣게 되면 다른 값을 저장할 수 있게 된다.



### Block scope

* 블럭안의 코드는 블럭 밖에서 접근 할 수 없다.
* **글로벌 변수**는 블럭 안, 밖 어디서는 접근이 가능하다.
  * 애플리케이션이 시작되어 끝날 때까지 메모리에 탑재되어 있다.
  * 최소한으로 사용하는 것이 좋다.

```JavaScript
let globalName = 'global name'; // 글로벌 변수
{
  let name = 'jaemin';
	console.log(name);
	name = 'siru';
	console.log(name);
}
```



### Hoisting

* 변수, 함수가 어디에서 선언이 되었느냐에 상관 없이 제일 위로 끌어올리는 것



## Constant

* 한번 가르킨 포인터가 잠겨있음
* 선언과 동시에 할당이 되면 값을 변경 불가
* Immutable
* 보안, thread safety, 실수를 줄이기 위해



## Variable types

* JavaScript에서는 변수의 타입이 다이나믹하게 할당된다.

### Primitive

* single item: 더 이상 작은 단위로 나눌 수 없는 것

* number, string, boolean, null, undefined, symbol

* number

  * -2 ** 53 ~ 2**53
  * bigInt: 숫자의 제일 마지막에 n을 붙임(Chrome, Firefox)
  * Infinity = 1 / 0
  * negativeInfinity = - 1 / 0
  * NaN: not a number
  * DOM요소를 다룰 때 valid한 값인지 고려해야 함

* string

  * 다른 string과 +를 이용해서 붙일 수 있음

  * template literals: 백틱(`)을 감싸서 변수를 함께 사용할 수 있음

    ```JavaScript
    const name = 'siru';
    const helloSiru = `hi ${name}`;
    ```

* boolean

  * 참과 거짓
  * false: 0, null, undefined, NaN
  * true: any other value
  * 부등호의 참, 거짓

* null: 명확하게 비어있는 상태

* undefined: 선언은 되었지만, 값이 지정되어 있지 않은 것

* symbol

  * 고유한 식별자
  * 동시 다발적으로 일어날 코드에서 우선순위를 주고 싶을 때 사용
  * 동일한 string으로 작성하여도 다른 값으로 취급
  * for 메소드를 사용해서 같은 symbol을 만들 수 있음
  * 출력시 description 메소드 사용

  ```JavaScript
  const symbol1 = Symbol('id');
  const symbol2 = Symbol('id');
  console.log(symbol1 === symbol2) // false
  const gSymbol1 = Symbol.for('id');
  const gSymbol2 = Symbol.for('id');
  console.log(gSymbol1 === gSymbol2) // true
  console.log(`value: ${symbol.description}`)
  ```



### Object

* box container: single item을 한 단위로 묶어서 관리할 수 있는 것

```JavaScript
const siru = { name: 'siru', age: 5};
siru.age = 6;
```

* 한 번 할당된 object는 다른 object 할당이 불가능하다.
* object 안의 변수의 값은 다른 값으로 할당할 수 있다.



### Function

* frist-class function: 다른 데이터 타입처럼 변수에 할당, 함수의 파라미터로 전달, 함수의 return으로 사용 가능



### Dynamic typing

* JavaScript는 선언시 데이터 타입을 명시할 필요가 없다.
* 런타임(프로그램 동작)에서, 할당된 값에 따라 타입이 변경
* 다수의 엔지니어, 규모가 있는 프로젝트에서 오류 발생의 원인이 될 수 있음
  * Type Script로 보완



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)