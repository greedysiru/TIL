# 19장 프로토 타입(8)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 19.10 instanceof 연산자

* 이항 연산자
* 좌변 객체, 우변 생성자 함수를 가리키는 식별자를 피연사자로 받음
* 우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변 객체의 프로토타입 체인 상에 존재하면 true로 평가

```JavaScript
function Cat(name) {
  this.name = name;
}

const siru = new Cat('siru');

console.log(siru instanceof Cat); // true
console.log(siru instanceof Object); // true
```



## 19.11 직접 상속

### 19.11.1 Object.create에 의한 직접 상속

* 명시적 프로토타입 지정하여 새로운 객체 생성
  * 추상연산 OrdinarObjectCreate 호출
* 매개변수로 생성 객체의 프로토타입 객체, 프로퍼티 키, 프로퍼티 디스크립터 객체 전달
* new 연산자 없이도 객체 생성 가능
* 프로토타입 지정하면서 객체 생성
* 객체 리터럴에 의해 생성된 객체 상속
* Object.create 메서드를 사용하여 프로토타입을 생성한 경우, Object.prototype의 빌트인 메서드 사용 불가
  * 간접적으로 호출해야 함(Function.prototype.call)



### 19.11.2 객체 리터럴 내부에서 직접 상속

* `__proto__`에 의한 직접 상속
* 객체를 생성하면서 프로토타입 지정하여 직접 상속 가능

```JavaScript
const catProperties = {name: 'siru', age: 7};

const cat = {
  isFat: false,
  __proto__: catProperties,        
}
```

