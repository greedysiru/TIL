# [드림코딩 by 엘리] JavaScript 기초 강의(9) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/550) 참고**



# HTTP

* Hyprertext Transfer Protocall
  * Hypertext: 문서, 이미지 등을 포함
* 브라우저 위에서 동작하고 있는 클라이언트와 서버가 어떻게 통신할 지를 정한 것
* request: 클라이언트가 서버에게 요청
* response: 서버가 클라이언트에게 응답



# AJAX

* Asynchronous JavaScript And XML
* HTTP를 이용해서 서버에게 데이터를 요청하여 받아오는 방법
* 웹페이지에서 동적으로 서버에게 데이터를 주고 받을 수 있다.



## XHR

* XMLHttpRequest
* 브라우저 API에서 제공하는 Object 중 하나
  * fetch API: 최근 추가된 브라우저 API, 브라우저와 서버가 통신할 수 있다.
* 간단하게 서버에게 데이터를 요청하고 받아올 수 있다.



## XML

* HTML과 같은 마크업 언어 중 하나
* 태그를 이용해서 데이터를 나타냄
* 불필요한 태그가 많이 들어가서 파일의 크기가 커지고 가독성이 좋지 않다.
* 서버와 데이터를 주고받을 때는 XML말고도 다른 포맷이 많음



# JSON

* JavaScriot Object Notation
* 1999년도, ECMAScript 3rd에서 쓰여진 Object에서 영감을 받아 만들어짐
  * JavaScript의 Object와 같이 Key와 Value로 이루어져 있다.
* 브라우저, 모바일, Object를 파일 시스템으로 저장 할 때 등 많이 사용되고 있다.
* 데이터를 주고받을 때 사용하는 가장 간단한 데이터 포맷
* 가볍고 가독성이 좋다.
* 데이터를 서버와 주고 받을 때 serialization 또는 전송시 사용
  * serialization: 직렬화
* **프로그래밍 언어, 플랫폼에 상관 없이 사용할 수 있다.**



## 1. Object to JSON



### stringify

* Oberloading: 함수 이름은 같지만 어떤 파라미터, 몇개의 파라미터가 전달되는가에 따라서 각각 다른 방식으로 호출되는 것
* replacer: 두번째 파라미터로 콜백함수를 넣어서 세밀하게 변환할 수 있음
* Object를 받아와서 string으로 변환한다.
  * 메소드는 JSON에 포함되지 않는다.
  * 함수는 Object가 있는 데이터가 아니기 때문이다.
  * JavaScript에만 있는 데이터도 포함되지 않는다.(symbol)
* 홀 따옴표를 쌍 따옴표로 바꾼다.

```JavaScript
// boolean같은 primitive도 가능
let json = JSON.stringify(true);
console.log(json); // true

// array
json = JSON.stringify(['apple', 'banana']);
console.log(json); // ["apple", "banana"]

// Objcet
const cat = {
  name: 'siru',
  color: 'black',
  size: null,
  birthDate: new Date(),
  jump: () => {
    console.log(`${name} cant jump`);
  },
};

json = JSON.stringify(cat);
console.log(cat); // {"name":"siru","color":"black","size":null,"birthDate":"2021-06-26T17:31:54.943Z"}
```



### replacer

* stringify의 두번째 파라미터
* 함수 혹은 배열로 전달
  * 원하는 property만 배열에 넣으면 해당 property만 json으로 변환된다.

```JavaScript
// Objcet
const cat = {
  name: 'siru',
  color: 'black',
  size: null,
  birthDate: new Date(),
  jump: () => {
    console.log(`${name} cant jump`);
  },
};

let json = JSON.stringify(cat, ['name']);
console.log(json); // {"name":"siru"};

json = JSON.stringify(cat, (key, value) => {
  // key가 name인 경우 greedysiru로 변환
  return key === 'name' ? 'greedysiru' : value;
});
console.log(json); //  {"name":" greedysiru","color":"black","size":null,"birthDate":"2021-06-26T17:31:54.943Z"}
```





## 2. JSON to Object

### parse

* string을 Object로 변환
* 두번째 파라미터로 콜백함수를 넣어서 세밀하게 변환할 수 있음
* serialize된 stirng을 다시 JSON으로 바꾸는 것이므로 기존의 선언된 함수를 접근할 수 없다.

```JavaScript
// Objcet
const cat = {
  name: 'siru',
  color: 'black',
  size: null,
  birthDate: new Date(),
  jump: () => {
    console.log(`${name} cant jump`);
  },
};

let json = JSON.stringify(cat);
const obj = JSON.parse(json, (key, value) => {
  return key === 'brithDate' ? new Date(value) : value;
});
```



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)