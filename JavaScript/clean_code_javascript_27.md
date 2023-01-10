# 클린코드 자바스크립트 - 배열 다루기(Array.length)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Array.length

* 배열 길이
* 실무에서 많이 사용되는 배열 프로퍼티



### Array.length에 임의의 값 할당

* Array는 근본적으로 객체
  * length 또한 동적으로 할당 가능
* length에 배열의 실제 길이보다 큰 값을 넣으면, 그 만큼 배열에 빈 요소들이 생김
* 즉, legnth의 실질적인 의미는 길이보다는 **마지막 요소의 인덱스**에 가까움

```JavaScript
const cats = ['siru', 'nunu', 'mango'];

console.log(cats.length); // 3

cats.length = 10;

console.log(cats.length); // 10

// 빈 요소가 생기게 됨
console.log(cats); // cats ['siru', 'nunu', 'mango', , , , , , , ]
```



### Array.length 특성 활용

* 상기대로, length의 특징을 활용하여 아래와 같은 메서드를 만들 수 있음

```JavaScript
Array.prototype.clear = function () {
  this.length = 0;
}

const cats = ['siru', 'nunu', 'mango'];
cats.clear();

console.log(cats); // cats []
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)
