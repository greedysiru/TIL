# [코드잇] 프로그래밍과 데이터 in JavaScript (2)(2021.2.16)



**상세 내용 [블로그](https://greedysiru.tistory.com/205) 참고**



# 배열

## 01. 배열 (Array)

* **순서가 있는 여러값의 묶음**
  * 요소(element) : 배열을 이루는 각각의 값
* Property Name이 필요없이 순서있는 데이터를 나열하는 경우

> **ley arrayName = [**
>
> **'element1',**
>
> **'element2'**
>
> **]**



### index

* **각 요소별로 숫자 값이 매겨진다.**
* 객체의 Property Name과 비슷한 역할
* 0 부터 센다.



### 배열의 요소 가져오기

* 인덱싱

> **arrayName[index];**



## 02. 배열 다루기

* **배열 또한 객체이다.**
* 다양한 프로퍼티와 메소드가 있다.



### length 프로퍼티

* **배열의 요소 총 개수를 표시해준다.**

```JavaScript
let myArray = ['a', 'b', 'c', 'd'];

console.log(myArray.length); // 4 출력
console.log(myArray['length']); // 4 출력
console.log(myArray[myArray.length -1]); // 마지막 요소 접근
```



### 요소 추가 & 수정

* **새로운 인덱스를 생성하여 요소를 추가**할 수 있다.
  * 인덱스의 순서를 뛰어넘어 추가하면 undefined가 자동으로 생성
* **기존의 인덱스에 접근하여 요소를 수정**할 수 있다.

> **arrayName[index] = 'element';**



### 요소 삭제

* delete 연산자
  * **요소 값은 지우지만 요소는 empty로 남아있다.**

> **delete arrayName[index];**



## 03. 배열 메소드 I

### splice 메소드

* **element를 추가, 수정, 삭제할 수 있다.**
* 첫 번째 parameter: 삭제를 시작할 index
* 두 번째 parameter에 삭제할 개수 전달
  * 생략할 시, 삭제를 시작할 index부터 배열의 끝 element까지 삭제
  * **0을 입력하면, 삭제 하지 않는다.**
* 세 번째 parameter에 삽입할 element를 입력
* index를 완전히 삭제

> **arrayName.splice(startIndex, deleteCount, item);**



## 04. 배열 메소드 II

### shift 메소드

* 배열의 첫 요소를 삭제
  * parameter가 없음

> **arrayName.shift();**



### pop 메소드

* 배열의 마지막 요소를 삭제
  * parameter가 없음

> **arrayName.pop();**



### unshift 메소드

* 배열의 첫 요소로 값 추가
  * parameter에 추가할 값 입력

> **arrayName.unshift(value);**



### push 메소드

* 배열의 마지막 요소로 값 추가
  * parameter에 추가할 값 입력

> **arrayName.push(value);**



## 05. 배열 메소드 Tip

### indexOf 메소드

* 배열에서 특정한 값을 찾는다.
  * 포함되어 있다면, index를 return
  * 포함되어 있지 않다면, -1을 return
  * 처음 발견된 index가 return
  * optional parameter(두 번째)로 검색을 시작할 index를 입력할 수 있다.

```JavaScript
let brands = ['Google', 'Kakao', 'Naver', 'Kakao'];
console.log(brands.indexOf('Kakao')); // 1
console.log(brands.indexOf('Daum'));  // -1
```



### lastIndexOf 메소드

* 배열에서 특정한 값을 찾는다.
  * 뒤에서 부터 탐색

```JavaScript
let brands = ['Google', 'Kakao', 'Naver', 'Kakao'];
console.log(brands.lastIndexOf('Kakao')); // 3
console.log(brands.lastIndexOf('Daum'));  // -1
```



### includes 메소드

* 배열에서 특정한 값의 존재 여부
  * boolean으로 return

```JavaScript
let brands = ['Google', 'Kakao', 'Naver', 'Kakao'];
console.log(brands.includes('Kakao')); // true
console.log(brands.includes('Daum'));  // false
```



### reverse 메소드

* 배열의 순서를 뒤집는다.

> **arrayName.reverse();**



## 06. for ... of 반복문

* 배열을 다룰 수 있는 for문
  * 변수에 배열의 요소가 할당
* for ... in 은 객체에 최적화되어 있으므로 for ... of를 사용하는 것을 권장

> **for (변수 of 배열){**
>
> **동작부분;**
>
> **}**



## 07. 다차원 배열 (multidimensional array)

* **배열안의 배열이 존재할 경우**
  * 2차원 배열, 3차원 배열 ...
* 여러 값들을 순서나 위치에 중점을 둔 정보로 표현



### 접근하기

* 다차원 배열을 이루는 배열 각각의 index에 접근하면 된다.

```JavaScript
let twoDimensional = [[1, 2], [3, 4]];

console.log(twoDimensional[0][1]); // 2 출력
```



# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)