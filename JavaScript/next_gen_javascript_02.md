# Next-Gen JavaScript - Classes



**본 내용은 Udemy의 React 완벽 가이드 with Redux, Next.js, TypeScript 강의를 토대로 작성하였습니다.**



## Classes

* 객체를 위한 핵심 청사진
* class 키워드로 정의
  * 클래스에 정의한 변수
* property와 method를 가짐
  * 클래스에 정의한 함수
* 생성자 함수의 문법적 설탕
* 상속
  * 다른 클래스에 있는 property와 method를 상속하면 잠재적으로 새로운 propery와 method를 추가한다는 뜻



### 예시

```JavaScript
class Human {
  constructor(gender) {
    this.gender = gender;
  }
  
  printGender() {
    console.log(this.gender);
  }
}

// Human 클래스를 상속
class Person extends Human {
  // 클래스의 인스턴스를 생성할 때마다 실행
  constructor(name) {
    // 서브 클래스(상속 받는 클래스)는 super를 호출해야 함
    // gender를 넘겨줌
    super('male');
    // property
    this.name = name;
  }
  
  // method
  printMyName() {
    console.log(this.name);
  }
}

const person = new Person('James');
person.printMyName(); // James
person.printGender(); // male
```



### Class Filed

* class 블록 안에서 할당 연산자로 인스턴스 속성을 지정할 수 있음
  * constructor 없이 속성 지정
* ES7

```JavaScript
class Person {
  static isLive = true;
}
```



### Arrow Function Method

* 화살표 함수 메서드의 this는 호출 형태에 관계없이 항상 인스턴스 객체를 가리킴
  * 화살표 함수의 this는 바로 바깥쪽 스코프에 존재하는 객체를 가리킴

```JavaScript
class Person {
  static isLive = true;
  
  getIsLive = () => {
    return this.isLive;
  }
}
```






## Reference

[[Udemy] React 완벽 가이드 with Redux, Next.js, TypeScript](https://www.udemy.com/course/best-react/)

