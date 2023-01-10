# 클린코드 자바스크립트 - 배열 다루기(JavaScript의 배열은 객체다)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## JavaScript의 배열은 객체다



### 배열에 인덱스가 아닌 프로퍼티 할당

* 배열은 객체와 같이 프로퍼티에 값을 할당할 수 있음
* 즉, JavaScript의 배열은 객체

```JavaScript
const arr = [1, 2, 3];

// 아래 할당문들은 정상적으로 할당이 됨
arr[3] = 'Test';
arr['property'] = 'String';
arr['obj'] = {};
arr[{}] = [1, 2, 3];
arr['func'] = function () {
	return 'Function in Array';
};

// 아래 객체는 위 배열과 같이 할당할 수 있음
const obj = {
  3: 'Test',
  property: 'String',
  obj: {},
  '{}' : [1, 2, 3],
  func : function () {
    return 'Function in Object';
  }
}
```



### 배열과 객체의 차이

* 배열은 프로퍼티 명을 인덱스로 가지는 객체
  * 인덱스는 0부터 순차적으로 1씩 증가하는 정수



### 배열인지 검사할 때

* 최근 문법이라 폴리필이 필요할 수도 있음

```JavaScript
const cats = ['siru', 'nunu', 'mango'];

console.log(Array.isArray(cats)); // true
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

