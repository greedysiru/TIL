# 19장 프로토 타입(9)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 19.12 정적 프로퍼티/메서드

* 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출 가능한 프로퍼티/메서드
* 생성자 함수가 생성한 인스턴스로 참조/호출 불가
* 인스턴스/프로토타입 메서드에서 this를 사용하지 않으면, 정적 메서드로 변경 가능

```JavaScript
// 생성자 함수
function Cat(name) {
  this.name = name;
}

// 프로토타입 메서드
Cat.prototype.introduce = function () {
  console.log(`나는 ${name}다. 고양이지.`);
};

// 정적 프로퍼티
Cat.isCat = true;

// 정적 메서드
Cat.sayWhatIs = function () {
  console.log('이것은 고양이를 가리킨다.')
};
```



## 19.13 프로퍼티 존재 확인

### 19.31.1 in 연산자

* 객체 내 특정 프로퍼티 존재 여부 확인
* 프로토타입 체인 상에 존재하는 모든 프로퍼티 검색
* Reflect.has 메서드도 in과 동일하게 동작
  * ES6 도입

```JavaScript
const siru = {
  name: siru,
  isCat: true,
  isFat: false,
};

console.log('name' in siru); // true
console.log('isFool', in siru); // false

console.log(Reflect.has(siru, 'name')); // true
```



### 19.13.2 Object.prototype.hasOwnProperty 메서드

* 객체에 특정 프로퍼티 존재 확인

```JavaScript
const siru = {
  isFool: true,
};

console.log(siru.hasOwnProperty('isFool')); // true
```

