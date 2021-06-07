# [드림코딩 by 엘리] JavaScript 기초 강의(3) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/508) 참고**



## variable

### rw(read/write)

* 읽고 쓰기가 가능한 것
* 값을 할당 변경
* let



## Constant

### r(read only)

* 읽기만 가능
* 다른 값으로 바꾸기 불가능
* const(Constant)



## Primitive vs. Object

* Primitive: 값 자체가 메모리에 저장
* Object: 메모리에 저장되지 않고 reference를 가리킴(포인터)
  * reference는 실제로 object가 담겨있는 메모리를 가리킴
  * const로 선언한 경우, 포인터가 잠기지만 object는 변경이 가능



## Immutable vs. Mutable

* Immutable: 데이터 자체를 바꿀 수 없음

  * primitive types, frozen objects

  > **primitive의 경우, 특정한 문자열을 정의하면 그 문자열을 통째로 메모리를 올린 후 다른 문자열로 변경이 가능하지만 문자열의 일부를 다른 것으로 변경하거나 데이터 자체를 변경하는 것은 불가능하다.**

* Mutable: objects, array



## Operator

### String concatenation

* **+**를 이용하여 문자열끼리 합치기 가능
* 문자열에 숫자를 더하면, 숫자가 문자열 취급되어 합해진다.
* 백틱(**`**)을 사용하면 변수와 문자열을 유연하게 사용할 수 있다.
  * 줄바꿈, 특수 기호도 인식이 가능

```javascript
console.log('my' + ' cat');
console.log('1' + 2);
console.log(`string literals: 1 + 2 = ${1 + 2}`);
```



### Numeric operators

* **+, -, /, *, %, ****: 덧셈, 뺄셈, 나누기, 곱셈, 나머지, 제곱



### Increment and decrement operators

* **++**: 증가

  * 앞에 쓰면 preincrement 먼저 더하고, 뒤에 쓰면 postincrement 나중에 더한다.
  * --도 동일

  ```JavaScript
  let x = 3;
  let y = ++x;
  console.log(y) // 4
  let z = y++;
  console.log(z) // 4
  ```



### Assignmenrt operators

* **=**: 할당

  * Numeric operators와 같이 사용할 수 있다.

  ```JavaScript
  let x = 3;
  x += 1
  ```



### Comparison operators

* 비교 연산자
  * **<, <=, >, >=**



### Logical operators

* **|| (or)**
  * 하나라도 true면, true
  * 가장 앞이 true이면, 더이상 뒤의 연산을 진행하지 않는다.
  * 그러므로 함수로 호출되거나 많은 연산이 실행되어야 나오게되는 boolean은 제일 뒤에 두는 것이 좋다.
* **&& (and)**
  * 모든 것이 true이어야 true
  * 가장 앞이 false이면, 더이상 뒤의 연산을 진행하지 않는다.
  * 그러므로 함수로 호출되거나 많은 연산이 실행되어야 나오게되는 boolean은 제일 뒤에 두는 것이 좋다.
  * null check에 활용
* **! (not)**
  * boolean을 반대로



### Equlity

* **==, !=** : loose equality
  * 타입을 변환하여 비교한다.
* **===, !==**: strict equality
  * 타입을 변환하지 않고 비교한다.
  * strict를 사용하는 것을 **권장**

```JavaScript
const stringNum = '1';
const pureNum = 1;

console.log(stringNum == pureNum); // true
console.log(stringNum != pureNum); // false
console.log(stringNum === pureNum); // false
console.log(stringNum !== pureNum); // true
```

<br>

* object의 경우
  * 같은 값이 입력되어 있어도, 각각 다른 reference를 가르키고 있다.

```JavaScript
const cat1 = { name: 'siru'};
const cat2 = { name: 'siru'};
const cat3 = cat1;
console.log(cat1 == cat2); // 다른 ref, false
console.log(cat1 === cat2); // 다른 ref, false
console.log(cat1 === cat3); // 같은 ref, true
```

<br>

* 다양한 예시

```JavaScript
console.log(0 == false); // true
console.log(0 === false); // false
console.log('' == false); // true
console.log('' === false); // false
console.log(null == undefined); // true
console.log(null === undefined); // false
```



## Conditional operators

### if, else if, else

* **if**: true이면 block의 명령어를 실행
* **else if**: if가 아닌경우 넘어와서 실행
* **else**:if, else if 모두 아닐 때 실행



### Ternary operator

* 값을 할당하거나 간단하게 데이터를 출력시 간단하게 사용

  ```JavaScript
  const name = 'siru';
  console.log(name === 'jm'? 'yes' : 'no');
  ```

* nesting을 남발하면 가독성이 좋지 않다.
  * if, switch를 사용



### switch

* 변수의 값에 따라서 명령을 실행

```JavaScript
const browser = 'IE';
switch (browser) {
  case 'IE':
    console.log('bad');
    break;
  case 'Chrome':
  case 'Firefox':
    console.log('good');
    break;
}
```



## Loops

### while

* statement가 false가 나올 때 까지 반복

```JavaScript
let i = 3;
while (i > 0){
  console.log(`while: ${i}`);
  i--;
}
```



### do-while loop

* block을 먼저 실행 후 조건을 확인

```JavaScript
let i = 3;
do {
  console.log(`do while: ${i}`);
  i--;
} while (i > 0);
```



### for loop

* begin, condition, step을 주고 반복문 실행
  * begin의 변수는 지역변수

```JavaScript
for (let i = 3; i > 0; i = i - 2){
  console.log(`inline variable for: ${i}`);
}
```



### nested loop

* loop를 중첩하여 사용할 수 있다.
* 아래의 경우 O(n<sup>2</sup>)이므로 cpu에 좋지 않다. 되도록 지양할 것.

```JavaScript
for (let i = 0; i < 10; i++){
  for (let j = 0; j < 10, j++){
    console.log(`i: ${i}, j: ${j}`);
  }
}
```



### break, continue

* break: loop을 완전히 끝냄
* contiunue: 한번 skip하고 loop 진행





# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)

