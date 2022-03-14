# 19장 프로토 타입(7)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 19.9 프로토타입의 교체

* 프로토타입은 임의의 다른 객체로 변경 가능
* 부모 객체인 프로토타입을 동적으로 변경 가능
* 객체간 상속 관계 동적 변경
* 생성자함수, 인스턴스에 의해 교체 가능
* 직접 교체보다는 직접 상속이 더 직관적이고 간편



### 19.9.1 생성자 함수에 의한 프로토타입의 교체

* 생성자 함수 정의부에서 prototype 프로퍼티를 통해 프로토타입을 교체 가능
* 교체시, constructor 프로퍼티와 생성자 함수 간의 연결이 파괴되므로 constructor 프로퍼티도 추가할 것

```JavaScript
const Cat = (function() {
  function Cat(name) {
    this.name = name;
  }
  
  // prototype 교체
  Person.prototype = {
    // constructor도 명시적으로 연결
    constructor: Cat,
    callCatName() {
      console.log(`고양이 ${this.name} 입니다.`);
    }
  };
  
  return Cat;
})
```



### 19.9.2 인스턴스에 의한 프로토타입의 교체

* 생성자 함수의 prototype 프로퍼티에 다른 임의의 객체를 바인딩하는 것은 인스턴스의 프로토타입을 교체하는 것
* `__proto__` 접근자를 통해 교체하는 것은 생성 객체의 프로토타입을 교체하는것
  * 단, 역시 constructor 프로퍼티와의 연결 파괴

```JavaScript
function Cat(name) {
  this.name = name;
}

const siru = new Cat('siru');

// 프로토타입으로 교체할 객체
const catMethod = {
  eatChuru() {
    console.log(`먹는다 나 ${this.name} 츄르를`);
  }
}

siru.__proto__ = catMethod;
```

