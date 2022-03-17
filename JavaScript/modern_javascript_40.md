# 19장 프로토 타입(10)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 19.14 프로퍼티 열거

### 19.14.1 for ... in 문

* 객체의 모든 프로퍼티를 순회하며 열거(enumeration)
  * 상속받은 프로퍼티 까지 열거
* 프로퍼티의 개수만큼 순회
* 선언한 변수에 프로퍼티 할당
* 프로퍼티 어트리뷰트가 [[Enumerable]] 일 때 열거 가능
* 배열에는 for ...of 문 권장

```JavaScript
const siru = {
  name : 'siru',
  age : 7,
  gender: woman,
  isGreedy: true,
}

for (const key in siru) {
  console.log(key);
}
```



### 19.14.2 Object.keys/values/entries 메서드

* 고유 프로퍼티만 열거하기 위해서는 위 메서드들이 더 적절
* keys : 열거 가능한 프로퍼티 키를 배열로 반환
* values : 열거 가능한 프로퍼티 값을 배열로 반환
* entries : 열거 가능한 키와 값의 쌍을 배열에 담아 반환(2차 배열)