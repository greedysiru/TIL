# 클린코드 자바스크립트 - 배열 다루기(불변성)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 불변성

* 참조형 자료형(배열, 객체)은 원본을 보존해야함
  * 참조형은 주소값을 바라보므로 단순히 새로운 변수에 할당해서는 안됨
  * 예기치 못한 오류 야기(원본 훼손)
* 새로운 변수에 배열을 할당할 때는 배열을 복사하기
* 배열의 새로운 배열을 반환한느 메서드들을 활용



### 원본이 훼손되는 예

```JavaScript
const cats = ['siru', 'nunu'];

// 새로운 변수에 cats 배열 할당
// newCats는 배열 cats의 주소값을 바라보게 됨
const newCats = cats;

cats.push('meonji');
cats.push('mango');
cats.push('jumbacki');
cats.unshift('yaongi');

// newCats를 출력했음에도 원본배열과 똑같은 결과가 나옴
console.log(newCats); // ['yaongi', 'siru', 'nunu', 'meonji', 'mango', 'jumbacki'];
```



### 스프레드 문법

* 스프레드를 사용하여 새로운 변수에 새로운 배열을 할당할 수 있음
  * 새로운 배열을 생성하여 변수에 할당하는 것

```JavaScript
// 상기 코드 예시는 아래와 같이 해결 가능
const newCats = [...cats];
```



### 새로운 배열을 반환하는 메서드

* filter
* map
* slice
* mdn에서 원본 배열을 바꾸는 지에대한 여부를 확인할 수 있음



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

