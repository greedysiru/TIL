# 클린코드 자바스크립트 - 함수 다루기(Default Value)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Default Value

* 함수가 받는 매개변수에 기본값을 넣어야 안전하게 함수를 사용 가능
* Error 방지

```JavaScript
function createCat(informatios) {
  informations = informations || {}; // 기본값 {}(객체 리터럴) undefined가 들어오는 것을 방지하여 Error 발생을 막음
  const name = informations.name || 'unknown';
  const color = informations.color || 'unknown';
  return {
    name,
    color
  }
}
```



### 구조 분해와 Default Parameter를 활용하기

* 전달 받은 파라미터의 Default value를 Default Parameter 문법으로 정의할 수 있음

```JavaScript
function createCat({name = 'unknown', color = 'unknown'} = {}) {
  return {
    name,
    color
  }
}
```



### 특정 값이 들어오지 않았을 때의 Error 처리

```JavaScript
const required = (argumentName) => {
  throw new Error(`${argumentName}은 필수 값입니다.`);
}

// name이 들어오지 않으면 Default parameter로 지정되어 있는 required 함수가 실행
function createCat({name = required('name'), color = 'unknown'} = {}) {
  return {
    name,
    color
  }
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

