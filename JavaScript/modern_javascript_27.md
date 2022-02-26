# 16장 - 프로퍼티 어트리뷰트(3)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 16.4 프로퍼티 정의

* 새로운 프로퍼티를 정의하면서 프로퍼티 어트리뷰트를 명시적으로 정의
* 또는 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의



### 16.4.1 Object.defineProperty

* 인수로 객체의 참조, 프로퍼티 키, 프로퍼티 디스크립터 객체 전달
* 접근자 프로퍼티도 정의 가능
* 프로퍼티 어트리뷰트에서 생략된 writable, enumerable, configurable은 false로 기본값 적용
* Object,defineProperties를 사용하면 여러개의 프로퍼티 한 번에 정의 가능

```JavaScript
const myPet = {};

Object.defineProperty(myPet, 'name', {
  value: 'siru',
  writable: true,
  enumerable: true,
  configurable: true,
})

Object.defineProperty(myPet, 'species', {
  value: '고양이',
  writable: true,
  enumerable: true,
  configurable: true,
})



Object.defineProperty(myPet, 'introduce', {
  // getter
  get() {
    return `${this.name}은 ${this.species}이다.`;
  },
  
  // setter
  set(name, species) {
  	this.name = name;
  	this.species = speices;
	},

	enumerable: true,
  configurable: true,
})
```



## 16.5 객체 변경 방지

* 객체는 직접 변경이 가능
* 객체의 변경을 방지하는 다양한 메서드가 있음
  * 객체 확장 금지 : Object.preventExtensions
  * 객체 밀봉 : Object.seal
  * 객체 동결 : Object.freeze



### 16.5.1 Object.preventExtensions

* 객체 확장 금지
* 프로퍼티의 추가가 금지 됨
* 인수로 확장을 금지할 객체의 참조를 전달
* 동적 추가 및 Object.defineProperty 메서드 둘 다 금지 됨
* Object.isExtensible로 확장 가능 여부 확인 가능
* **프로퍼티의 삭제는 가능**



### 16.5.2 Object.seal

* 객체 밀봉
* 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지
  * **갱신은 가능**
* 인수로 밀봉할 객체의 참조 전달
* **읽기외 쓰기만 가능**
* Object.isSealed 메서드로 밀봉 여부 확인 가능
* 밀봉된 객체의 **configurable 프로퍼티 어트리뷰트는 false 임**



### 16.5.3 Object.freeze

* 객체 동결
* 프로퍼티 추가, 삭제, 갱신 및 프로퍼티 어트리뷰트 재정의 금지
* 인수로 동결할 객체의 참조 전달
* Object.isFrozen 메서드로 동결 여부 확인 가능
* 동결된 객체의 **writable, configurable은 false 임**
* 추가, 삭제, 갱신을 시도하면 무시
  * strict mode에서는 에러 발생



### 16.5.4 불변 객체

* 객체 동결로 객체를 불변하게 만들 수 있지만, 객체 안의 중첩 객체는 적용되지 않음
* 재귀적으로 Object.freeze를 적용하여 중첩 객체까지 적용