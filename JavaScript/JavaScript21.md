# [코드잇] 프로그래밍과 데이터 in JavaScript (1)(2021.2.15)



**상세 내용 [블로그](https://greedysiru.tistory.com/204) 참고**



# 객체

## 01. 객체와 프로퍼티

## 객체 (Object)

* **여러가지 값을 한 번에 저장할 수 있다.**



### 객체 만들기

> **let object = {**
>
> **key1 : value1,**
>
> **key2 : value2**
>
> **}**



### 속성(Property)

* **key와 value의 한 쌍**
  * key : Property Name
  * value : Property Value
* **Property Value** 안에 **모든 자료형**이 들어갈 수 있다.



### Property Name 주의 사항

* 원칙적으로 따옴표를 붙어야 하지만 붙이지 않아도 JavaScript에서 문자열로 형변환
* **첫 글자는 반드시 문자, 밑줄(_), 달러 기호($) 중 하나로 시작**
* **띄어쓰기 금지**
* **하이픈(-) 금지**
* 불가피하게 규칙을 어기는 경우, **따옴표**를 붙인다.



## 03. 객체에서 데이터 접근하기

### 점 표기법

* 따옴표로 감싸진 property name을 가진 것은 접근하지 못한다.

> **object.propertyName**



### 대괄호 표기법

* 따옴표로 감싸진 property name에 접근할 수 있다.
* 대괄호 안에 **변수**를 넣거나 '+'연산자를 넣을 수 있다.
  * **변수에 담긴 값을 가져올 때는 대괄호 표기법을 사용해야만 한다.**

> **object['property name']**



### 객체안의 객체 접근

> **object.propertyName1.propertyName2**
>
> **object.porpertyName1['propertyname2']**



## 05. 객체 다루기

### 프로퍼티 생성 & 수정

* **생성**: Property Name에 value를 입력한다.
* **수정**: 원하는 Property Name에 접근 후 새로운 Property Value를 입력

> **object.propertyName = 'Property Value';**



### 프로퍼티 삭제

* **delete 연산자 사용**

> **delete object.propertyName;**



### in 연산자

* **해당하는 Property Name을 가진 Property가 존재하는지의 여부를 불린으로 return**

> **console.log('porpertyName' in object);**



### 예시

```JavaScript
let profile = {
  name : 'greedysiru',
  bornYear: 2020,
  isVeryNice: true,
  language: {
    title: 'JavaScript',
    status: 'beginner'
  },
  hobby: null
}

if ('name' in profile){
  console.log(`name 값은 ${profile.name}입니다.`);
} else {
  console.log('프로퍼티가 없습니다.')
}
// name 값은 greedysiru입니다. 출력
```



## 06. 객체와 메소드

* 객체는 연관성 있는 함수들을 묶을 수 있다.
* 메소드는 어떤 객체의 고유한 동작이며 함수에 의미를 부여할 수 있다.
  * 같아보이는 함수라도 객체에 따라 다르게 동작
  * 이름 중복을 피할 수 있고 객체에 집중할 수 있다.
* **이런 함수들을 객체의 메소드라고 한다.**
  * console.log 또한 메소드

> **let object = {**
>
> **functionName: function (parameter) {**
>
> **실행할 명령어;**
>
> **}**
>
> **}**



### 메소드 접근

* 대괄호 표기법으로도 접근 가능하다.

> **object.functionName('parameter');**



### 예시

```JavaScript
let rectAngle = {
  width: 30,
  height: 50,
  getArea: function () {
    return rectAngle.width * rectAngle.height;
  }
}

let triAngle = {
  width: 15,
  height: 40,
  getArea: function () {
    return triAngle.width * triAngle.height / 2;
  }
}
```

* 같은 이름의 함수인 **getArea**는 객체에 따라서 다르게 동작한다.



## 07. for ... in 반복문

* **객체 안의 프로퍼티를 가지고 반복적인 동작 수행**
  * 객체의 property name이 변수에 담기게되고 동작부분을 Property의 갯수만큼 반복한다.

> **for (변수 in 객체) {**
>
> **동작부분**
>
> **}**



### 예시

```JavaScript
let profile = {
  name : 'greedysiru',
  bornYear: 2020,
  isVeryNice: true,
  language: {
    title: 'JavaScript',
    status: 'beginner'
  },
  hobby: null
}

for (let key in profile) {
  console.log(profile[key]);
}
```

* profile의 key값들이 변수 key에 담겨져 Property의 갯수만큼 블록문을 반복한다.
* 변수 key를 이용하여 profile의 Property Value에 매번 접근하여 모든 값들을 출력할 수 있다.



## 0.8 for ... in 주의사항

### 숫자형(양수) 프로퍼티 네임

* Property Name은 숫자형(양수)을 작성해서 사용할 수 있다.
* **사용될 때는 문자열로 형 변환이 되어 사용된다.**
* 대괄호 표기법으로만 접근이 가능하다.



### 정수형 프로퍼티 네임

* **객체는 정수형 Property Name을 오름차순으로 먼저 정렬 후, 나머지 Property들은 추가한 순서대로 정렬하는 특징이 있다.**
* 의도치 않은 결과를 가져올 수 있음에 주의



## 09. Date 객체

* **내장 객체(Standard built-in objects) : JavaScript에서 미리가지고 있는 객체**
* **날짜와 관련된 객체**



### Date 객체 만들기

```JavaScript
let myDate = new Date();
```

* 변수 선언 후 new 연산자와 Date() 함수 사용
* 객체를 만든 순간의 시간이 저장된다.
  * 요일, 월, 일, 년도, 시간, 시간대



### 특정 시점 날짜 생성 (밀리초)

```JavaScript
let myDate = new Date(1000);
```

* 넣어준 숫자값의 밀리초만큼 **유닉스 시간(타임 스탬프)**을 지난 객체가 생성
* **유닉스 시간(타임 스탬프)** : 1970년 1월 1일 00:00:00 UTC



### 특정 시점 날짜 생성 (문자열)

* 날짜로 해석이 가능한 문자열을 넣어 해당 날짜의 객체 생성
  * YYYY-MM-DD : 해당 년, 월, 일의 자정 기준
  * YYYY-MM-DDThh:mm:ss : 해당 년, 월, 일 시간을 기준

```JavaScript
// 년, 월, 일
let myDate1 = new Date('2020-02-15');

// 년, 월, 일, 시간
let myDate2 = new Date('2020-02-15T20:16:20');
```



### 소괄호 안에 여러가지 값 전달하여 생성

* 년, 월, 일, 시, 분, 초, 밀리초
  * **년, 월은 필수**
  * **월은 0부터 시작**

```javascript
let myDate = new Date(2020, 1, 15, 22, 19, 6, 16);
```



## 10. Date 메소드

* 생성한 Date객체에 메소드를 사용할 수 있다.
* **getDate(): 객체의 일자**
* **getDay() : 객체의 요일**
  * 일요일부터 0 ~ 6 까지



### getTime

* **유닉스 시간(타임 스탬프)으로부터 몇 밀리초 지났는지 알아낸다.**

```Javascript
let myDate = new Date();

console.log(myDate.getTime());
// 유닉스 시간으로부터 지금이 몇 밀리초 지났는지 출력
```



## 11. Date 객체 Tip

### Date 객체 정보 수정하기

*  **set으로 시작하는 메서드는 생성된  Date 객체의 정보를 수정**
* **setFullYear()**
* **setMonth()**
* **setDate()**

```JavaScript
let myDate = new Date();

myDate.setFullYear(2012);
myDate.setMonth(4);
myDate.setDate(2);
```



### 간단하게 시간 정보 알아내기

```JavaScript
let myDate = new Date();

console.log(myDate.toLocalDateString()); // myDate가 가진 날짜에 대한 정보 (년. 월. 일)
console.log(myDate.toLocaleTimeString()); // myDate가 가진 시간에 대한 정보 (시:분:초)
console.log(myDate.toLocaleString()); // myDate가 가진 날짜와 시간에 대한 정보 (년. 월. 일 시:분:초)
```



### Date.now() 메소드

* **메소드가 호출된 시점의 타임스탬프를 반환**

```JavaScript
let myDate = new Date();

console.log(Date.now() === myDate.getTime()); // true
```



### Date 객체의 형변환

```JavaScript
let myDate = new Date();

console.log(String(myDate)); 
console.log(Number(myDate)); 
console.log(Boolean(myDate)); // true
```

* String 변환 시, Date 객체의 날짜값이 그대로 문자열로 변환
* **Number 변환 시, getTime() 메소드를 사용한 것과 똑같은 수치의 타임스탬프 값**
  * 이를 이용해서, 두 Date 객체 끼리의 시간 차이를 구할 수 있다.

# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)