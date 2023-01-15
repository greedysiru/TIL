# 클린코드 자바스크립트 - 객체 다루기(Prototype 조작 지양하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Prototype 조작 지양하기

* Class 문법이 있는 지금 prototype을 사용할 이유는 없음
  * 생성자 함수로 class를 구현했던 때에는 prototype을 사용
  * Class는 문법적 설탕으로 결국에는 prototype 문법으로 바뀜
* 빌트인 객체의 prototype을 건드리는 것은 위험
  * 런타임에서 예기치 못한 에러를 발생시킬 수 있음



### prototype를 활용한 상속

```JavaScript
// 생성자 함수
function Cat(name, color) {
  this.name = name;
  this.color = color;
}

// Cat 생성자 함수로 인해 만들어진 인스턴스는 아래 메서드를 사용할 수 있게 됨
Cat.prototype.introduceSelf = function () {
  return `안녕하세요. ${this.name}입니다. ${this.color}색 옷을 입고 있습니다. 그럼 이만.`;
}

// 인스턴스 생성
const siru = new Cat('시루', '카오스');

siru.introduceSelf(); // '안녕하세요. 시루입니다. 카오스색 옷을 입고 있습니다. 그럼 이만.'
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

