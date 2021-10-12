# Generator & Iterator (2) - Generator

**본 내용은 10분 테코톡 파노님의 강의를 토대로 작성하였습니다.**



## 1. Generator Function

* Generator Function은 Generator Instance를 생성
* new 키워드를 사용한 인스턴스 생성([[constructor]])이 아닌, 일반적인 함수호출([[call]])을 통해 인스턴스를 생성
  * Generator 함수의 특별한 동작

```JavaScript
function* generatorFunction() {};

const generator = generatorFunction();

typeof generator; // 'object'
```



### Generator Syntax

* **function*** : Generator 함수 선언 키워드
* **yield** : Generator 함수 내부에서 사용하는 키워드
  * next 메서드 호출 시, value로 반환할 값에 사용하는 키워드
  * 다음 next가 호출될 때까지 해당 키워드에서 함수실행이 멈춤
* **yield*** : 또 다른 Iterable 객체를 위임해서 사용하는 키워드

```JavaScript
function* generatorFunction() {
  yield* [1, 2, 3];
}

const generator = generatorFunction();

for (const element of generator) {
  console.log(element);
}
// 1 2 3 출력
```



## 2. Generator Instance

* Iterable 인터페이스와 Iterator 인터페이스를 동시에 구현한 객체



### Generator Instacne의 Iterable Interface

* Iterable 인터페이스
  * @@iterator (Symble.interator) 프로퍼티에 Iterator 객체인 자기자신을 반환하는 함수 저장

```JavaScript
function* generatorFunction() {};

const generator = generatorFunction();

const iterator = generator[Symbol.iterator]();

console.log(generator === iterator); // true
```



### Generator Instance의 Iterator Interface

* value와 done을 반환하는 next 메서드를 포함

```JavaScript
function* generatorFunction() {
  yield 1;
};

const generator = generatorFunction();

const iteratorResult = generator.next();

console.log(iteratorResult); // {value: 1, done: false}
```



### Generator Instance의 Internal Slot

* Generator의 상태(실행 중인지, 중단됐는지 등) 정보가 [[GeneratorState]]에 저장
* 실행 컨텍스트가 [[GeneratorContext]]에 저장
* 실행이 중단된 Generator가 next()가 호출되면 중단 지점부터 다시 실행될 수 있는 이유



## 3. Lazy Evaluation

* 지연평가
* 계산의 결과값이 필요할 때까지 계산을 늦추는 기법
* 필요한 데이터를 필요한 순간에 생성
* Generator의 가장 큰 특징



### 무한수열 예시

* while 문으로 무한 반복문을 선언하더라도 yield로 인해서 함수 평가가 중지가 됨

```JavaScript
function* genFunc() {
  let i = 0;
  
  while (true) {
    yield i++;
  }
}

const gen = genFunc();

// yield에서 함수 평가가 중지가 됨
console.log(gen.next()); // {value: 0, done: false}
console.log(gen.next()); // {value: 1, done: false}
console.log(gen.next()); // {value: 2, done: false}
```



## 4. 함수형 프로그래밍에서 Early Evaluation vs. Lazy Evaluation

### Lazy Evaluation

* 필요한 2번의 순회만 진행
* 필요한 값만 효율적으로 계산할 수 있음

```JavaScript
Object.prototype.lazyMap = lazyMap;
Object.prototpye.take = take;

// this의 element를 순회하는 함수
function* lazyMap(callback) {
  for (const el of this) {
    // callback이 적용된 element의 값만 yiled로써 iterator Result로 반환
    yield callback(el);
  }
}

// 전달 받은 값만큼 길이를 가지는 배열 result를 반환
function take(n = Infinity) {
  const result = [];
  
  for (const el of this) {
    result.push(el);
    
    if (result.length === n) break;
  }
  
  return result;
}

function callback(element) {
  console.log('callback called!');
  
  return element + 1
}

const arr = Array(10000).fill(1);

const mappedArr = arr.lazyMap(callback).take(2);

consoe.log(mappedArr);
// (2)callback called!
// [2, 2]
```



### Early Evaluation

* 만 번의 순회를 진행하게 됨

```JavaScript
...
const arr = Array(10000).fill(1);

const mappedArr = arr.map(callback).take(2);

console.log(mappedArr);
```

# Reference

[[10분 테코톡] 파노의 Generator & Iterator](https://www.youtube.com/watch?v=3uuBHt_SNTA)

