# Generator & Iterator (1) - Iteration Interface

**본 내용은 10분 테코톡 파노님의 강의를 토대로 작성하였습니다.**

## 1. 일반적인 배열 순회 방법

* 배열의 length 프로퍼티를 이용하여 for문으로 인덱스를 증가시켜 데이터에 접근
* 해당 객체에 대한 length 정보가 필요
* index는 0이상의 정수로써 순차적으로 증가해야함
* 단점 : 코드가 명령적이고 의도가 잘 드러나지 않음
* for of 문을 사용하여 순회하는 것이 더 명시적임

```JavaScript
const arr = [1, 2, 3];

for (let i = 0; i < arr.length; i++) {
  const element = arr[i];
  console.log(element);
}
```



## 2. Iteration Interface

* ECMAScript 명세에 정의
* 세 개의 인터페이스로 구성
  * **Iterable**
  * **Iterator**
  * **Iterator Result**



### Iterable

* Iterable 객체는 Iterator 객체를 반환하는 함수를 값으로 갖는 **@@iterator** 프로퍼티를 포함
  * @@iterator: 스펙상의 명칭. 실제로는 iterable 객체의 Symbol.Iterator 프로퍼티에서 해당 함수를 찾을 수 있음
* Symbol.Iterator: Symbol 생성자 함수에 있는 프로퍼티.
  * Well-Known Symbol: ECMAscript 스펙을 구현한 built-in Symbol
  * @@ prefix가 붙는 스펙상 프로퍼티들을 실제로 구현한 빌트인 Symbol 중 하나

```JavaScript
const arr = [1, 2, 3];

console.log(arr[Symbol.iterator]); // values()가 return

arr.values() // Iterator 객체를 return
```



### Iterator

* Interator객체는 IteratorResult를 반환하는 **next** 메서드를 포함
  * next 메서드는 IteratorResult를 반환



### Iterator Result

* Boolean 타입의 값을 갖는 **done**과 모든 타입의 값을 가질 수 있는 value 프로퍼티를 가짐
* Iterator가 끝에 도달하지 않았다면, **done**은 **false**이고 **value**는 이용가능
* Iterator가 끝에 도달했다면, **done**은 **true**이고 **value**는 'iterator의 반환 값'
* done: 순회 완료 여부
* value: 최근 순회 요소

```JavaScript
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();
console.dir(iterator.next()); // done: false, value가 존재하는 Object가 반환
```



## 3. for of 문과 Iterator Interface

* ES6에서 추가
  *  **Iteration Interface**로 인해 가능해 짐
* length 데이터에 의존하지 않고 배열 자체로 순회
* 보다 선언적임

```JavaScript
arr = [1, 2, 3];

for (const element of arr) {
  console.log(element);
}

-------------------------------------------------------------------------------------------------------

const iterable = [1, 2, 3];

// for-of 구현

const iterator = iterable[Symbol.iterator]();

while (true) {
  const itertatorResult = iterator.next();
  
  if (iteratorResult.done) break;
  
  consoel.log(iteratorResult.value);
}
```



## 4. Sperad 연산자

### Math.max()

* 전달받은 인자 중 가장 큰 값을 반환하는 메서드
* 베열을 넘기면 동작하지 않음
* 인자 하나 하나 전달해야 함
* 배열을 전개해 인자를 전달하는 Spread 연산자로 해결

```JavaScript
Math.max([1, 2, 3]); // NaN

Math.max(...[1, 2, 3]); // 3
```

# Reference

[[10분 테코톡] 파노의 Generator & Iterator](https://www.youtube.com/watch?v=3uuBHt_SNTA)