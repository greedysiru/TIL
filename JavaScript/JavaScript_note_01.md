# JavaScript 노트 (01)

## Math

### 절댓값 (Absolute Number)

> **Math.abs(number);**

* number: 양수 혹은 음수



### 최댓값 (Maximum)

> **Math.max(num1, num2, num3, num4, num5);**

* 여러 파라미터 중, 가장 큰 값을 리턴



### 최솟값 (Minimum)

> **Math.min(num1, num2, num3, num4, num5);**



### 거듭제곱 (Exponentiation)

> **Math.pow(x, y);**

* x<sup>y</sup> 리턴



### 제곱근 (Square Root)

> **Math.sqrt(x);**

* x의 제곱근 리턴



### 반올림 (Round)

> **Math.round(x);**

* 정수로 반올림하여 리턴



### 버림과 올림 (Floor and Ceil)

> **Math.floor(x);**
>
> **Math.ceil(y);**

* **floor**: 버림
* **ceil**: 올림



### 난수 (Random)

> **Math.random();**

* 0이상 1 미만의 값이 랜덤으로 리턴



## string

### 문자열 내 다른 문자열 검색

> **str.indexOf('string');**

* 한 자리, 여러자리 문자열 검색 가능
* 문자열  str 내에 문자열 string이 포함되어 있는지 확인
* 포함된 경우: 문자열이 시작되는 문자열의 인덱스가 리턴
* 포함되지 않은 경우: -1 리턴
* 여러개인 경우: 처음 발견된 인덱스를 리턴



### 마지막 인덱스 찾기

> **str.lastIndexOf('stirng');**

* 가장 뒤에 위치한 검색 결과



### 대문자 변환

> **str.toUpperCase();**

* str의 모든 글자를 대문자로 리턴



### 소문자 변환

> **str.toLowerCase();**



### 시작 지점과 끝 지점으로 자르기

> **str.substring(start, end);**

* start: 시작 인덱스
* end: 끝 인덱스
* start부터 end 전까지의 문자열 리턴
* end 생략 시 start부터 끝까지 문자열 리턴



### 시작 지점과 길이로 자르기

> **str.substr(start, length);**

* start: 시작 인덱스
* length: 문자열 길이
* start부터 length만큼 문자열을 잘라서 리턴



### 앞뒤 공백 없애기

> **str.trim();**



## Array

### 배열의 길이

> **array.length;**



### 배열에서 특정 값 찾기

> **array.indexOf('item');**

* item이 있으면 해당 인덱스 리턴
* 없으면 -1 리턴
* 처음 발견된 인덱스를 리턴



### 배열 값 추가

> **array.push(item1);**
>
> **array.push(item1, item2, item3);**

* 배열에 끝에 추가



### 배열에서 값 빼기

> **array.pop();**

* 배열의 마지막 요소를 뺀 후 그 값을 리턴



### 배열을 문자열로 바꾸기

> **array.join();**

* 배열의 모든 내용을 문자열 하나로 합치고 리턴
*  파라미터: 쉼표를 대체할 문자열



## Date

### 객체 만들기

> **var date = new Date();**

* 파라미터가 없으면 현재 날짜로 설정
* 원하는 날짜를 파라미터로 입력



### 날짜 정보를 받아오는 메소드들

Date 객체를 만들고 사용한다.

```JavaScript
var date = new Date('June 11, 1988 05:25:30');

console.log(date.getFullYear());       // 1988
console.log(date.getMonth());          // 5
console.log(date.getDate());           // 11
console.log(date.getDay());            // 6
console.log(date.getHours());          // 5
console.log(date.getMinutes());        // 25
console.log(date.getSeconds());        // 30
console.log(date.getMilliseconds());   // 0
console.log(date.toString());          // Sat Jun 11 1988 05:25:30 GMT+1000 (KDT)
console.log(date.toLocaleString());    // 6//11/1988, 5:25:30 AM
console.log(date.toLocaleDateString());// 6/11/1988
console.log(date.toLocaleTimeString());  // 5: 25:30 AM
```

* **getMonth()**: 0부터 시작하므로 3은 4월을 의미한다.
* **getDay()**:  요일을 리턴, 일요일 0부터 시작





### 지난 시간 가져오기

> **date.getTIme();**

* date 객체의 시점이 1970년 1월 1일 자정으로부터 몇 ms 지났는지 리턴
* 나눗셈을 적절히 사용하면 초, 분, 시, 일 등의 단위로 변환

