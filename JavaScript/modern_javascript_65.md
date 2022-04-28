# 27장. 배열(3)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 27.9 배열 고차 함수

* 고차 함수: 함수를 인수로 전달받거나 함수를 반환하는 함수
  * 외부 상태의 변경이나 가변을 피하고 불변성을 지향하는 함수형 프로그래밍에 기반
* 조건문과 반복문을 제거
* 변수의 사용 억제
* 순수 함수를 통해 부수 효과를 최대한 억제



### 27.9.1 Array.prototype.sort

* 배열 요소 정렬
* 원본 배열을 직접 변경하며 정렬된 배열 반환
* 기본적으로 오름차순으로 요소 정렬
* 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따름
  * 숫자를 정렬할 때는 정렬 순서르 정의하는 비교 함수를 인수로 전달
  * 비교 함수는 양수, 음수 또는 0을 반환해야 함
  * 음수인 경우, 첫 번째 인수를 우선하여 정렬
  * 0이면 정렬하지 않음
  * 양수인 경우 두 번째 인수를 우선하여 정렬

```JavaScript
const cats = [
  {name: 'siru', age: 7},
  {name: 'nunu', age: 5},
  {name: 'mango', age: 6},
];

// 비교 함수 정의
function compare(key) {
  return (a, b) => (a[key] > b[key] ? 1: (a[key] < b[key] ? -1 : 0));
}

// age 기준으로 오름차순 정렬
cats.sort(compare('age'))

// name 기준으로 오름차순 정렬
cats.sort(compare('name'));
```



### 27.9.2 Array.prototype.forEach

* for문을 대체하는 고차 함수
* 자신을 호출한 배열을 순회하면서 콜백 함수를 전달받아 반복 호출
* 콜백 함수에 배열의 요소 값, 인덱스, this를 순차적으로 전달 가능
* 원본 배열을 변경하지 않음
  * 콜백 함수를 통해 변경 가능
* 반환 값은 undefined
* 두 번째 인수로 this로 사용할 객체 전달 가능
  * 화살표 함수의 경우, 상위 스코프의 this를 참조하므로 전달하지 않아도 됨
* 반복문 처럼 break, continue를 사용할 수 없음
* 성능상 for문보다 좋지 않지만 가독성이 좋으므로 사용을 권장

```JavaScript
['siru', 'nunu', 'mango'].forEach((cat, index, cats) => {
  console.log(`${cat}은(는) ${cats}에 속한 고양이 중 ${index + 1} 번째 입니다.`);
})
```



### 27.9.3 Array.prototype.map

* 자신을 호출한 배열의 모든 요소를 순회하여 전달 받은 콜백 함수 반복 호출
* 콜백 함수의 반환값으로 구성된 새로운 배열 반환
* 원본 배열은 변경되지 않음
* map 메서드를 호출한 배열과 map 메서드가 생성하여 반환한 배열은 1:1 매핑 됨
  * length가 서로 반드시 일치
* 콜백 함수는 배열의 요소 값, 인덱스, this를 순차적으로 받을 수 있음

```JavaScript
const explainsForCats = ['siru', 'nunu', 'mango'].map((cat, index, cats) => {
  return `${cat}은(는) ${cats}에 속한 고양이 중 ${index + 1} 번째 고양이 입니다.`;
})

console.log(explainsForCats);
/*
['siru은(는) siru,nunu,mango에 속한 고양이 중 1 번째 고양이 입니다.', 'nunu은(는) siru,nunu,mango에 속한 고양이 중 2 번째 고양이 입니다.', 'mango은(는) siru,nunu,mango에 속한 고양이 중 3 번째 고양이 입니다.']
/*
```

