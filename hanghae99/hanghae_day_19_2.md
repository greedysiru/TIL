# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (1) (2021.3.19)

# 1. 웹과 DOM

## 1.1 웹의 동작 개념

* 브라우저가 하는 일
  * 서버가 만들어 놓은 API라는 창구에 미리 정해진 약속대로 **요청**
  * **받은 파일을 그려주기**
* 서버가 하는 일
  * 데이터를 클라이언트에게 전달
  * **JSON형식**으로 전달



## 1.2 서버리스

* 미리 설정이 된 서버를 빌려다 쓰는 것
  * ex. aws의 EC2
* 서버의 사양, 네트워크 설정이 미리 되어있으므로 인프라 작업을 하지 않아도 된다.
* **백엔드 리스가 아니다.**



## 1.3 DOM

* html 단위 하나 하나를 객체로 생각하는 모델
  * div, p, h1, h2, span
* **트리구조**

![JavaScript25-1](../JavaScript/images/JavaScript25-1.png)



# 2. JavaScript 문법(ES6)

* ES6: 자바스크립트 표준 문법 중 하나로 가장 보편화된 것



## 2.1 Class

* 객체 지향 프로그래밍에서 특정 객체를 생성하기 위해 **변수와 함수를 정의하는 일종의 틀**
* 객체 단위로 코드를 그룹화하고 쉽게 **재사용**
* **constructor**: 생성자 함수
  * 클래스 인스턴스를 생성하고 생성한 인스턴스를 초기화
  * 초반에 어떤 값이 들어갈지 정함



### 상속

*  **extends** 키워드 사용
* 생성되어 있는 클래스를 상속받을 수 있다.
* **super**
  * 부모 클래스에 접근할 수 있다.
  * 부모의 constructor를 호출하면서 인수를 전달
  * this를 사용할 수 있다.
  * **메소드로 사용**
  * **키워드로 사용**
* 부모 클래스와 자식 클래스에 같은 이름을 가진 함수가 있을 경우
  * **자식 클래스에서 부모 클래스의 함수를 오버라이딩 한다.**
  * 같은 이름 함수를 쓸 수 있다는 의미



### 예시

```javaScript
class Cat {
	// 생성자 함수
  constructor(name) {
		// 여기서 this는 이 클래스
		this.name = name; 
	}

	// 함수
	showName(){
		return this.name;
	}
}

// extends는 Cat 클래스를 상속.
class MyCat extends Cat {
	// 생성자 함수
  constructor(name, age) {
		// super를 메서드로 사용
		super(name); 
		this.age = age; 
	}
	// 오버라이딩
	showName(){
		// super를 키워드로 사용하기
		return '내 고양이 이름은 '+super.showName()+'입니다.';
	}
	
	showAge(){
		console.log('내 고양이는 '+this.age+'살 입니다!');
	}
}

let my_cat = new MyCat('siru', 4);
my_cat.showName();
my_cat.showAge();
```





## 2.2 const, let, var와 Scope

* **Scope: 변수를 불러서 사용할 수 있는 범위**
* JavaScript에서 선언과 할당이 동시에 가능
* 블록: 중괄호 안
* **const는 재할당이 되지 않는다.**
  * 상수
  * **블록 단위**의 스코프를 가진다.
* **let은 재할당이 가능**
  * 변수
  * **블록 단위**의 스코프를 가진다.
* var
  * 변수
  * **함수 단위**의 스코프를 가진다.



## 2.3 =, ==, ===

* **=**
  * **어떤 변수에 값을 할당**
* **==**
  * **유형을 비교하지 않는 등차**
  * 변수값을 기반으로 비교
  * 0 == "0" 이어도 true 반환
* **===**
  * **유형도 비교하는 등차**
  * 0 === "0" 은 false



## 2.4 Spread 연산자

* **어떤 객체 안의 요소를 객체 밖으로 꺼낸다.**
* **...**: 스프레드 문법
* 딕셔너리(중괄호)에도 사용 가능

```JavaScript
let array = [1, 2, 3, 4, 5];
let new_array = [...array];

console.log(new_array); // [1, 2, 3, 4 ,5] 출력
```



## 2.5 조건부 삼항 연산자

* if문의 단축 형태

> **조건? 참일 경우 : 거짓인 경우**

```JavaScript
let info = {name: "siru", id: 0};
let is_me = info.name === "siru"? true : false;
console.log(is_me); // true
```



## 2.6 Array 내장 함수

### map

* 배열에 속한 항목을 변환할 때 사용
* 원하는대로 변환 후 새로운 배열로 생성
* 원본 배열은 값이 변하지 않는다.
* 원본 배열과 길이가 같다.

```JavaScript
const array_num = [0, 1, 2, 3, 4, 5];

const new_array = array_num.map((array_item) => {
  // array_item에 +1 한 것을 생성
  return array_item + 1;
})

console.log(new_array); // [1, 2, 3, 4, 5, 6]
console.log(array_num); // [0, 1, 2, 3, 4, 5]
```



### filter

* 조건을 만족하는 항목만 골라서 새 배열로 생성
* 원본 배열은 그대로, 새로운 배열을 만들 수 있다.

```JavaScript
const array_num = [0, 1, 2, 3, 4, 5];

const new_array = array_num.filter((array_item) => {
  // array_num 원소 중 3보다 큰 것만 리턴
  // return에는 true , flase 의 boolean이 들어간다.
  return array_item > 3;
})

console.log(new_array); // [4, 5]
```



### concat

* 배열과 배열을 합치거나 배열에 특정 값을 추가하는 함수
* 원본 배열은 변하지 않는다.
* 중복되는 것도 적용된다.
* **중복을 피하고 싶으면 Set() 자료형을 사용**
  *  스프레드 문법과 사용할 것 -> 리스트 변환

```JavaScript
const array_num01 = [0, 1, 2, 3];
const array_num02 = [3, 4, 5];

const merge = array_num01.concat(array_num02);

// 중복 항목이 들어간다.
console.log(merge) // [0, 1, 2, 3, 3, 4, 5]

// 중복 제거하기
const new_merge =[... new Set(array_num01.concat(array_num02));]
```



### from

* 배열을 만들고자 하는 것이나 유사배열을 복사해서 새로운 배열로 만들 때
  * 텍스트를 하나하나 잘라서 배열에 넣을 때
  * DOM list 같은 유사배열을 넣을 때
* 새로운 배열을 만들 때 (초기화)



```JavaScript
// 문자열 배열화
const my_name = "siru";
const my_name_array = Array.from(my_name);
console.log(my_name_array); // ["s", "i", "r", "u"]

// 인덱스 번호로 생성 가능
const text_array = Array.from('hello', (item, idx) => {return idx});
console.log(text_array) // [0, 1, 2, 3, 4]

// 새 배열을 만들기
const new_array = Array.from({length: 4}, (item, idx) => {return idx;});
console.log(new_array) // [0 , 1, 2, 3]
```





# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)