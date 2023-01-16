# 클린코드 자바스크립트 - 객체 다루기(hasOwnProperty)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## hasOwnProperty

* 프로퍼티를 가졌는지 확인하는 메서드

```JavaScript
const cat = {
  name: 'siru',
}

cat.hasOwnProperty('name'); // true
cat.hasOwnProperty('age'); // false
```



### for ... in 문에서의 활용

```JavaScript
for (const key in object) {
  // JavaScript는 프로퍼티 명칭으로서 hasOwnProperty를 보호하지 않음
  // 따라서, 아래처럼 사용해야 안전하게 메서드를 실행할 수 있음
  if (Object.prototype.hasOwnProperty.call(object, key)) {
    const element = object.[key];
  }
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

