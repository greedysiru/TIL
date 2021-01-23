# [인프런 - 정재남] Javascript 핵심 개념 알아보기 - JS Flow (2)(2021.1.23)



**상세 내용 [블로그](https://greedysiru.tistory.com/137) 참고**

# 1. this

|               | VariablEnvironment     |                                      |
| ------------- | ---------------------- | ------------------------------------ |
|               |                        | environmentRecord (snapshot)         |
|               |                        | outerEnvironmentReference (snapshot) |
| inner         | **LexicalEnvironment** |                                      |
|               |                        | environmentRecord                    |
|               |                        | outerEnvironmentReference            |
|               | **ThisBinding**        |                                      |
| outer         |                        |                                      |
| 전역 컨텍스트 |                        |                                      |

* **ThisBinding**은 **실행 컨텍스트**가 활성화 될 때 일어난다.
* **함수가 호출** 될 때 **this가 결정**된다.



## 호출하는 방식에 따른 ThisBinding

* 전역공간에서
* 함수 호출시
* 메소드 호출시
* callback 호출시
* 생성자함수 호출시



### 전역공간에서

* 처음부터 호출이 되어있으므로 정해져 있다.
* 전역객체를 가르킨다.
* **전역객체** : 개념상으로 전역 컨텍스트를 실행하는 주체
  * **window: 브라우저**
  * **global: node.js**



### 함수 호출시

* 함수는 **전역객체의 메소드**이다.(라고 생각하자)
* 전역객체를 가르킨다.

```JavaScript
function a() {
  console.log(this);
}
a();
```

* 함수를 실행하는 순간에 그것을 호출한 주체는 **전역 공간**이기 때문이다.(window)

<br>

```JavaScript
function b(){
  function c(){
    console.log(this);
  }
  c();
}
b();
```

* 함수 c는 b내부에서 호출되지만, 역시 **window**를 가르킨다. (버그 추정)

<br>

```JavaScript
var d = {
  e: function() {
    function f() {
      console.log(this);
    }
    f(); /* 메소드 안에서 함수로서 호출 */
  }
}
d.e();
```

* 함수 f는 메소드 안에서 호출되었지만, **함수로서 호출되었으므로 this는 전역객체를 가르킨다.**



### 메소드 호출시

* 메소드 호출 주체 (메소드명 앞)

```JavaScript
var a = {
  b: function() {
    console.log(this);
  }
}
a.b(); /* a가 this */

------------------------------------------------------------------------------------

var a = {
  b: {
    c: function() {
      console.log(this);
    }
  }
}

a.b.c(); /* a.b가 this */
```

#### **내부함수에서의 우회법**

* 내부함수에서 this를 호출했을 시, 전역객체를 가르키지 않게 할 수 있다.(메소드의 경우)

```JavaScript
var a = 10;
var obj = {
  a: 20,
  b: function() {
    console.log(this.a); /* 20 출력 */
    
    function c() {
      console.log(this.a); /* this가 window를 가르킴 */
    }
    c( ); /* 10 출력 */
  }
}
obj.b();
```

* 함수 c는 메소드 내부에서 함수로서 호출되었다. 그러므로 함수 c로인해서 indow.a = 10이 출력된다.

<br>

```JavaScript
var a = 10;
var obj = {
  a: 20,
  b: function() {
    var self = this;
    console.log(this.a);
    
    function c() {
      console.log(self.a);
    }
    c(); /* 20 출력 */
  }
}
obj.b();
```

* **this를 다른 변수에 담아, 내부에서 사용하면 위의 문제를 해결할 수 있다.**



### callback 호출시

* **기본적으로는 함수내부에서와 동일**
* 제어권을 가진 함수가 **callback의 this를 명시한 경우 그에 따른다.**
* 개발자가 **this를 바인딩한 채로 callback을 넘기 그에 따른다.**

<br>

* 일반적인 경우 전역객체를 가르킨다.

```JavaScript
var callback = function() {
  console.dir(this); /* 전역객체 window */
};
var obj = {
  a: 1,
  b: function(cb) {
    cb();  
  }
};
obj.b(callback);
```

<br>

* call 메소드로 this를 지정할 수 있다.

```JavaScript
var callback = function() {
  console.dir(this); /* obj */ 
};
var obj = {
  a: 1,
  b: function(cb) {
    cb.call(this); /* this를 call 메소드로 지정 */
  }
};
obj.b(callback);
```

<br>

* setTimeout

```JavaScript
var callback = function() {
  console.dir(this); /* window */
};
var obj = {
  a: 1
};
setTimeout(callback, 100); /* 100secods 뒤에 callback 실행 */
```

* setTimeout에 bind를 사용하여 this를 지정할 수 있다.

```JavaScript
var callback = function() {
  console.dir(this); /* obj */
};
var obj = {
  a: 1
};
setTimeout(callback.bind(obj), 100); /* this를 obj로 지정 */ 
```

<br>

* addEventListener
  * 콜백함수 처리할 때, 그 대상 타겟으로 this를 정하게 되어있다.

```JavaScript
document.body.innerHTML += '<div id = "a">클릭하세요</div>';

document.getElemetById('a')
    .addEventListener('click', function() {
      console.dir(this); /* div#a */
});
```

* bind로 this를 정의할 수 있다.

```JavaScript
document.body.innerHTML += '<div id = "a">클릭하세요</div>';
var obj = { a: 1};

document.getElemetById('a')
    .addEventListener('click', function() {
      console.dir(this); /* obj */
}.bind(obj));
```





#### **call, apply, bind 메소드에 대하여**

* 명시적인 this 바인딩

> func.call(thisArg[ , arg1[ , arg2[ , ... ] ] ] )
>
> func.apply(thisArg, [argsAraay])
>
> func.bind(thisArg[. arg1[, arg2[, ... ] ] ] )

* 대괄호는 생략 가능
* **thisArg** : this를 명시적을 지정
* **call, apply** : 즉시 호출
* **bind** : 새로운 함수 생성(currying)

<br>

```JavaScript
function a(x, y, z) {
  console.log(this, x, y, z);
}
var b = {
  c: 'eee'
};

a.call(b, 1, 2, 3); /* Object {c: "eee"} 1 2 3 */

a.apply(b, [1, 2, 3]); /* Object {c: "eee"} 1 2 3 */

var c = a.bind(b);
c(1, 2, 3); /* Object {c: "eee"} 1 2 3 */

var d = a.bind(b, 1, 2);
d(3); /* Object {c: "eee"} 1 2 3 */
```

* **a.call(b, 1, 2, 3)**: a를 호출하는데 ,this는 b, 인자는 1,2,3으로 
* **a.apply(b, [1, 2, 3])**: a를 호출하는데, 괄호 안을 적용한다. this는 b로 인자는 배열로 실행한다.
* **var c = a.bind(b)**: 새로운 함수 생성. this는 b
* **var d = a.bind(b, 1, 2)**: 새로운 함수 생성, this는 b, 첫 번째 인자와 두 번째 인자는 1,2로 먼저 지정한다. 나머지 인자를 넣어서 호출할 수 있다.



### 생성자함수 호출시

* 인스턴스 자체가 this가 된다.

```JavaScript
function Person(n, a) {
  this.name = n; /* window */
  this.age = a;
}
var gomugom = new Person('고무곰', 30); /* new로 인해 생성자 함수로 사용 */
console.log(gomugom); /* gomugom 객체 */
```



# 2. 콜백함수

* **호출해서 다시 돌려줄 함수**
* 함수에 대한 **제어권**을 넘겨 준뒤 결과를 다시 돌려받는다.



## 제어권

### 실행 시점

* **setIntercal**: 주기마다 함수를 호출

> setInterval( callback, milliseconds )

```JavaScript
var cb = function() {
  console.log('1초마다 실행될 겁니다.');
};

setInterval(cb, 1000);
```

* **함수의 제어권이  setInterval로 넘어간다.**



### 인자

* **.forEach** : 배열의 값과 인덱스를 하나 하나씩 뽑아서 함수 실행

> arr.forEach( callback [, thisArg])

```JavaScript
var arr = [1, 2, 3, 4, 5];
var entries = [];
arr.forEach(function(v, i) { /* v : value i : index */
  entries.push([i, v, this[i]]); /* forEach의 두 번째 인자가  this */
}, [10, 20, 30, 40, 50]);
console.log(entries);
/*
[[0, 1, 10], [1, 2, 20], [2, 3, 30], [3, 4, 40], [4, 5, 50]]
*/
```



### this

* **addEventListener**

> target.addEventListener( type, listener[, useCapture]);

* **type**: 등록할 event type을 나타내는 문자열
* **listener**: 특정 타입의 이벤트가 발생할 때 알림을 받을 객체. 수행하는 객체이거나, Javascript 함수 이어야 한다.( callback)

```JavaScript
document.body.innerHTML = '<div id="a">abc</div>';
function cbFunc(x) {
  console.log(this, x); /* 이벤트 대상이 this, x는 이벤트 객체 */
}

document.getElementById('a')
  .addEventListener('Click', cbFunc);

$('#a').on('click', cbFunc);
```



## 콜백함수의 특징

* 다른 함수 (A)의 인자로 콜백함수(B)를 전달하면, A가 B의 **제어권**을 갖게 된다.
* 특별한 요청(bind)이 없는 한 A에 **미리 정해놓은 방식**에 따라 B를 호출한다.
  * **미리 정해놓은 방식** : 어떤 **시점**에 콜백을 호출할지, **인자**에는 어떤 값들을 지정할지, **this**에 무엇을 바인딩할지 등



## 주의

* 콜백은 **'함수'**이다.

```JavaScript
var arr = [1, 2, 3, 4, 5];
var obj = {
  vals: [1, 2, 3],
  logValues: function(v, i) {
    if(this.vals) { /* 메소드로 호출 시 */
      cosole.log(this.vals, v, i);
    } else {
      console.log(this, v, i);
    }
  }
}
obj.logValues(1, 2); /* 메소드로 호출 */
arr.forEach(obj.logValues); /* callback함수로 전달 */
```



# Reference

https://www.inflearn.com/course/핵심개념-javascript-flow