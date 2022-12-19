# 클린코드 자바스크립트 - 경계 다루기(prefix - suffix)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. prefix, suffix

* 접두사, 접미사
* JavaScript getter, setter가 대표적인 예
* 개인 또는 협업에서 prefix, suffix 규칙을 정의하여 컨벤션을 맞추면 좋음
* 일관성을 갖출 수 있는 좋은 방법



## 2. getter, setter

### JavaScript getter

* JavaScript 에서 객체의 프로퍼티에 접근할 수 있게하는 함수를 선언하는 예약어

```JavaScript
const cat = {
  name: 'siru',
  get name() {
    return this.name;
  }
}

console.log(cat.name); // 'siru'
```





### JavaScript setter

* JavaScript에서 객체의 프로퍼티 값을 할당할 수 있게하는 함수를 선언하는 예약어

```JavaScript
const cat = {
  set name(name) {
    this.name = name;
  }
}

cat.name = 'siru';
```



### prefix를 사용하는 경우

* 예약어를 쓰지 않고 prefix로 getter, setter를 표현할 수 있음

```JavaScript
const cat = {
  name = 'siru',
  getName() {
    return this.name;
  }
	setName(newName) {
    this.name = newName;
  }
}
```



## 3.  Prefix, suffix 예시들

### React.js

* hooks의 경우 use prefix가 붙음
  * useState
  * useEffect
  * useContext



### jQuery

* jQuery 객체는 $ prefix 사용



### JavaScript private field

* JavaScript에서는 private filed가 없었음
  * 과거에는 private filed를 의미하는 변수 앞에 `_`를 붙임
* 현재는 private filed를 지원

```JavaScript
function Cat(name) {
  this._name = name;
}

class Cat {
  #name = name;
}
```



### Vue.js

* 권장하는 컴포넌트 네이밍 컨벤션이 있음
  * BaseButton.vue
  * AppButton.vue
  * VButton.vue



### 복수(-s suffix)

* 복수인 경우 -s suffix가 붙임
* 이름만을 봐도, 복수인지 단수인지 빠르게 파악 가능
* actions, reducers



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

