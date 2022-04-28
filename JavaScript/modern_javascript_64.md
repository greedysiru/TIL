# 27장. 배열(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 27.5 배열 요소의 참조

* 참조할 때에는 대괄호 표기법([]) 사용
  * 대괄호 안에는 인덱스
  * 정수로 평가되는 표현식 사용 가능
  * 요소가 존재하지 않으면 undefined



## 27.6 배열 요소의 추가와 갱신

* 배열에 요소를 동적으로 추가 가능
* 존재하지 않는 인덱스를 사용해 값 할당 가능
* length 프로퍼티는 자동 갱신
* legnth 프로퍼티보다 큰 인덱스에 할당 시에는 희소 배열이 됨



## 27.7 배열 요소의 삭제

* 배열도 객체이므로 delete 연산을 사용하여 특정 요소 삭제 가능
  * length 프로퍼티에 영향을 주지 않음
  * 희소배열이 되므로 사용하지 않는 것이 좋음
* splice 메서드를 사용할 것을 권장



## 27.8 배열 메서드

* 자바스크립트에서는 다양한 배열 빌트인 메서드를 제공
* 패턴은 두 가지
  * mutator method : 원본 배열을 직접 변경하는 메서드
  * accessor method : 새로운 배열을 생성하여 반환하는 메서드
* ES5 이전의 초장기 배열 메서드는 원본 배열을 직접 변경하는 경우가 많음
* 원본 배열을 직접 변경하지 않는 메서드를 사용하는 것을 권장



### 27.8.2 Array.prototype.indexOf

* 인수로 전달된 요소를 검색하여 인덱스 반환
* 전달 받은 요소가 없는 경우, -1로 반환
* 배열에 특정 요소의 유무를 확일할 때 유용
* NaN을 포함하는지 확인할 수 없음
* ES7의 Array.prototype.includes 메서드가 가독성이 더 좋음

```Javascript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

cats.indexOf('siru'); // 0

cats.indexOf('nunu'); // 1

cats.indexOf('mango'); // 2

cats.indexOf('meonji'); // 3

cats.indexOf('boksili'); // -1
```



### 27.8.3 Array.prototype.push

* 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환
* 원본 배열을 직접 변경
* 성능 면에서 좋지 않음
* length 프로퍼티를 활용하여 마지막 요소를 직접 추가할 수 있음
  * 더 빠름
* 원본을 변경하기 때문에 ES6의 스프레드 문법을 활용하는 것이 좋음

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

// push 메서드
cats.push('boksili');

// lengh 메서드를 사용한 요소 추가
cats[cats.length] = 'bocksili';

// ES6 스프레드 문법
const newCats = [...cats, 'bocksili'];
```



### 27.8.4 Array.prototype.pop

* 원본 배열에서 마지막 요소를 제거하고 제거한 요소 반환
* 빈 배열이면 undefined를 반환
* 원본 배열을 직접 변경
* push와 pop을 사용하여 스택을 구현할 수 있음
  * 후입 선출의 자료구조(LIFO)

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

cats.pop(); // meonji
```



### 27.8.5 Array.prototype.unshift

* 윈수로 전달 받은 모든 값을 원본 배열의 선두에 요소로 추가하고 length 프로퍼티 반환
* 원본 배열을 직접 변경
* 스프레드 문법을 사용하는 것을 권장

```javaScript
const cats = ['siru', 'nunu', 'mango'];

// unshift 메서드
cats.unshift('meonji');

// ES6 스프레드 문법
const newCats = ['meonji', ...cats];
```



### 27.8.6 Array.prototype.shift

* 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환
* 원본이 빈 배열이면 undefined를 반환
* 원본 배열 직접 변경 
* shift와 push 메서드를 사용하여 큐를 쉽게 구현 가능
  * 선입선출(FIFO)의 자료구조

```JavaScript
const cats = ['siru', 'nunu', 'mango'];

cats.shift();
```



### 27.8.7 Array.prototype.concat

* 인수로 전달된 값을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환
* 원본 배열은 변경되지 않음
* 인수로 전달한 값이 배열의 경우 배열을 해체하여 추가
* push, unshift 메서드를 대체 가능
* push/unshift/concat 메서드를 사용하는 대신, 스프레드 문법 사용 권장

```JavaScript
const cats = ['siru', 'nunu'];

const newCats = cats.concat('mango', 'meonji');
```



### 27.8.8 Array.prototype.splice

* 원본 배열의 중간에 요소 추가 또는 제거시 사용
* 3개의 매개변수가 있음
  * start : 시작 인덱스
  * deleteCount :시작 인덱스로부터 제거할 요소의 개수. 생략할 경우, 삭제하지 않음
  * mites: 제거한 위치에 삽입할 요소들의 목록
* 원본 배열을 직접 변경

```javaScript
const cats = ['siru', 'nunu'];

cats.splice(1, 1, 'mango', 'meonji'); // [ 'siru', 'mango', 'meonji' ]
```



### 27.8.9 Array.prototype.slice

* 인수로 전달된 범위의 요소들을 복사하여 배열로 반환
* 원본 배열을 변경시키지 않음
* 두 개의 매개변수를 가짐
  * start: 복사를 시작할 인덱스, 음수의 경우 배열의 끝부터 요소를 복사
  * end: 복사를 종료할 인덱스, 생략할 시 기본값은 length 프로퍼티

```JavaScript
const cats = ['siru', 'nunu', 'meonji', 'boksili'];

cats.splice(0, 2); // ['siru', 'nunu'];
```



### 27.8.10 Array.prototype.join

* 배열의 모든 요소를 문자열로 변환
* 전달받은 인수를 구분자로서 사용
* 구분자는 생략 가능, 기본 값은 콤마(,)

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

cats.join(); // 'siru, nunu, mango, meonji'
```



### 27.8.11 Array.prototype.reverse

* 원본 배열의 순서를 반대로 뒤집음
* 원본 배열은 변경
* 변경된 배열을 반환

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];
const reversCats = cats.reverse(); // ['meonji', 'mango', 'nunu', 'siru']
```



### 27.8.12 Array.prototpye.fill

* 인수로 전달 받은 값을 배열의 처음부터 끝까지 요소로 채움
* 원본 배열 변경
* 두 번째 인수로 시작할 인덱스 지정
* 세 번째 인수로 멈출 인덱스 지정

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

cats.fill('siru');

console.log(cats); // ['siru', 'siru', 'siru', 'siru'];
```



### 27.8.13 Array.prototype.includes

* 배열 내에 특정 요소가 포함되어 있는지 확인하여 불린으로 반환
* 두번 째 인수로 검색을 시작할 인덱스를 전달할 수 있음



### 27.8.14 Array.prototype.flat

* ES10에 추가
* 인수로 전달한 깊이만큼 배열 평탄화

```javascript
const cats = ['siru', ['nunu', ['mango']]];

cats.flat(3); //[ 'siru', 'nunu', 'mango'];
```

