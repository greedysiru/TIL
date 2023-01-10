# 클린코드 자바스크립트 - 배열 다루기(map vs forEach)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## map vs forEach

* 두 메서드 모두 배열 빌트인 메서드
  * 배열 요소 하나하나를 순회하며 전달받은 콜백 함수를 실행
* map은 전달받은 콜백함수를 통해 새로운 형태의 배열을 return
  * 원본배열은 건드리지 않음(불변성 관리)
* forEach는 전달받은 콜백함수를 실행하기만 함
  * return이 콜백함수에 명시되어 있어도 반환값은 undefined
* 즉, 콜백을 통해 새로운 형태의 배열을 만들때는 map을 사용하고 배열을 순회하며 명령만 실행하면 되는 경우에는 forEach를 사용하기



```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji'];

const newCatsMap = cats.map(cat => `${cat} 이리와`);

const newCatsForEach = cats.map(cat => `${cat} 이리와`);

console.log(newCatsMap); // ['siru 이리와', 'nunu 이리와', 'mango 이리와', 'meonji 이리와']

console.log(newCatsForEach); // undefined
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

