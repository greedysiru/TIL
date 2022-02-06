# 10장 - 객체 리터럴(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 10.4 메서드

* 자바스크립트의 함수는 일급 객체이므로 값으로 취급 가능함
  * 즉, 객체에서 프로퍼티로 사용 가능하며 이를 **메서드**라 함



```JavaScript
const siru = {
  isCat: true,
  isDog: false,
  eatChuru: function () {
    console.log('맛잇다!');
  }
}
```



## 10.5 프로퍼티 접근

* 2가지의 표기법을 사용하여 접근 가능
* 접근 연산자 좌측에는 객체로 평가되는 표현식이 위치
* 프로퍼티 키가 존재하지 않아도 undefined가 발생할 뿐 에러가 발생하지 않으니 주의



### 마침표 표기법

* 마침표 접근 연산자 사용
* 프로퍼티 키가 식별자 네이밍을 준수한 경우 사용 가능



### 대괄호 표기법

* 대괄호 프로포터 접근 연산자 사용
* **내부의 프로퍼티 키는 반드시 따옴표로 감싸야 함**
  * 그렇지 않으면, 식별자로 해석함
* 프로퍼티 키가 식별자 네이밍을 준수하지 않은 경우 사용



## 10.6 프로퍼티 값 갱신

* 이미 존재하는 프로퍼티에 접근하여 값을 할당하면 갱신 됨

```JavaScript
const myPet = {
  name : 'siru';
}

console.log(myPet.name); // siru

myPet.name = 'nunu';

console.log(myPet.name); // nunu
```



## 10.7 프로퍼티 동적 생성

* 존재하지 않는 프로퍼티에 값을 할당

```JavaScript
const myPet = {};

const myPet.name = siru;
```



## 10.8 프로퍼티 삭제

* delete 연산자를 사용하여 삭제
* 존재하지 않은 프로퍼티를 삭제 시도시 무시

```JavaScript
const siru = {
  isCat: true,
  isDog: false,
};

delete siru.isDog;
```



## 10.9 ES6 객체 리터럴 확장 기능

### 10.9.1 프로퍼티 축약 표현

* 프로퍼티 키와 값이 동일할 때 축약하여 표현할 수 있음

```JavaScript
const siru = 'siru';
const nunu = 'nunu';

const pets = {siru, nunu};

console.log(pets); // {siru: "siru", nunu: "nunu"}
```



### 10.9.2 계산된 프로퍼티 이름

* 대괄호 표기법으로 객체 리터럴 내부에서 프로퍼터 키를 동적 생성할 수 있음

```JavaScript
const cat = 'cat';

const cats = {
  [`${cat}-1`] : 'siru',
  [`${cat}-2`] : 'nunu',
  [`${cat}-3`] : 'cong',
  [`${cat}-4`] : 'mango',
}
```



### 10.9.3 메서드 축약 표현

* function 키워드를 생략한 메서드 축약 표현

```JavaScript
const siru = {
  eat() {
    cosnole.log('쩝쩝');
  }
}
```

