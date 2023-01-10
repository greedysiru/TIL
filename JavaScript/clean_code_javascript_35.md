# 클린코드 자바스크립트 - 객체 다루기(Shorthand Properties)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Shorthand Properties

### CSS의 예

* CSS Attributes를 축약해서 표현할 수 있음

```CSS
.some {
  /* margin의 경우 */
  margin-top: 10px;
  margin-right: 5px;
  margin-bottom: 12px;
  margin-left: 7px;
  
  /* 위를 축약하면 아래와 같음 */
  margin: 10px 5px 12px 7px;
  
  /* background의 경우 */
  background-color: #000;
  background-image: url(images/some.png);
  background- repeat: no-repeat;
  backgorund-position: left top;
  
  /* 위를 축약하면 아래와 같음 */
  background: #000 url(images/some.png) no-repeat left top;
}
```



### JavaScript에서

* 객체의 특정 변수를 객체에 담을 때 객체를 그 변수 명과 같은 것으로 표현할 경우 축약할 수 있음
* 함수도 가능

```JavaScript
const name = 'siru';
const age = 8;
const isCute = true;
const isVaccinated = true;

const myCat = {
  name,
  age,
  isCute,
  isVaccinated,
}
```



## Concise Method

* JavaScript 객체의 method를 간결하고 보기 좋게 표현

```JavaScript
const cat = {
  eat: function() {
    console.log('냠냠');
  }
}

// 아래처럼 축약 가능
const cat = {
  eat() {
    console.log('냠냠');
  }
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

