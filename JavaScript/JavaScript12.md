# [인프런 - 정재남] Javascript 핵심 개념 알아보기 - JS Flow (1)(2021.1.22)



**상세 내용 [블로그](https://greedysiru.tistory.com/131) 참고**



# Intro

* ES6 이전 까지의 Javascript 전체를 관통하는 핵심 개념들에 대해서 전반적인 흐름을 살펴본다.



# 1. Data Types

* Primitive Type : 기본형
  * Number
  * String
  * Boolean
  * null
  * undefined
* Reference Type : 참조형
  * Object
    * Array
    * Function
    * RegExp



## 메모리의 측면에서 이해하기

### Primitive type

```JavaScript
var a;
a = 'abc';
a ='avcdef';
```

|    주소    | ...  | 1002 |            1003            | 1004 | 1005 | ...  |
| :--------: | :--: | :--: | :------------------------: | :--: | :--: | :--: |
| **데이터** |      |      | 이름: a 값: @5004 -> @5005 |      |      |      |

|    주소    | ...  | 5002 | 5003 | 5004  |   5005   | ...  |
| :--------: | :--: | :--: | :--: | :---: | :------: | :--: |
| **데이터** |      |      |      | 'abc' | 'avcdef' |      |

1. 변수 'a'가 선언되면, 메모리 안에 데이터가 담길 공간 1003번을 확보한다. 식별자는 변수명이다.
2. 문자열 'abc'를 'a'에 할당할 때, 'abc'를 메모리의 빈공간에 넣는다. 그리고 그것의 주소값을 식별자가 a인 1003번의 값에 넣는다.
3. 문자열 'abcdef'를 'a'에 할당할 때도 위와 같이 빈공간에 넣은 후 주소값을 'abcdef'의 주소값으로 변경한다.



### Reference type

```JavaScript
var obj = {
  a: 1,
  b: 'bbb'
};
obj.a = 2;
```

|    주소    | ...  |        1002         | 1003 | 1004 | ...  |  5002   | 5003 | 5004  | 5005 | 5006 | ...  |
| :--------: | :--: | :-----------------: | :--: | :--: | :--: | :-----: | :--: | :---: | :--: | :--: | :--: |
| **데이터** |      | 이름: obj 값: @5002 |      |      |      | @7103~? |  1   | 'bbb' |  2   |      |      |

|    주소    | ...  |            7103            |       7104        | 7105 | ...  | 8104 | 8105 | 8106 | 8107 | 8108 | ...  |
| :--------: | :--: | :------------------------: | :---------------: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| **데이터** |      | 이름: a 값: @5003 -> @5005 | 이름: b 값: @5004 |      |      |      |      |      |      |      |      |

1. 객체의 경우, 변수 'obj'가 선언되면, 메모리에 공간 1002를 확보하고 식별자는 변수명을 넣는다.
2. 메모리 구조상 들어갈 수 있는 데이터는 하나뿐이다. 그러므로, 묶음 처리해서 주소만 넣어 놓는다. (5002)
3. 주소 7103에 a가 들어가고 값은 다른 주소 5003번에 할당된다.
4. 주소 7104에 b가 들어가고 값은 다른 주소 5004번에 할당된다.
5. 객체의 값이 전부 할당이 끝나면 객체의 주소가 담겨있는 5002번 주소가 obj에 들어간다.
6. 프로퍼티 'a'의 값을 바꿀 때, 'obj'가 있는 1002번을 찾아간다.
7. 1002번에서 각 객체의 주소값이 있는 5002번을 찾아간다.
8. 프로퍼티 'a'가 있는 7103번을 찾아간다.
9. 2의 주소 5005번을 할당한다.
10. 'a'의 값의 주소를 5005번으로 바꾼다.



**Primitive type인 경우 값이 변경되면 주소 또한 변경된다. 반면, Reference type은 프로퍼티의 값이 변경되어도 변수 자체의 주소가 변경되지 않는다.**



### 중첩 객체

```JavaScript
var obj = {
  x: 3,
  arr: [3, 4]
};
abj.arr = 'str';
```

|    주소    | ...  |        1002         | 1003 | 1004 | ...  |  5002   | 5003 |  5004   | 5005 | 5006  | ...  |
| :--------: | :--: | :-----------------: | :--: | :--: | :--: | :-----: | :--: | :-----: | :--: | :---: | :--: |
| **데이터** |      | 이름: obj 값: @5002 |      |      |      | @7103~? |  3   | @8104~? |  4   | 'str' |      |

|    주소    | ...  |       7103        |             7104             | 7105 | ...  |       8104        |       8105       | 8106 | 8107 | 8108 | ...  |
| :--------: | :--: | :---------------: | :--------------------------: | :--: | :--: | :---------------: | :--------------: | :--: | :--: | :--: | :--: |
| **데이터** |      | 이름: x 값: @5003 | 이름: arr 값: @5004 -> @5006 |      |      | 이름: 0 값: @5003 | 이름:1 값: @5005 |      |      |      |      |

1. 객체 'obj'는 변수와 배열을 포함한다.
2. 'obj'는 1002번에 할당, 그 주소는 5002번에 할당된다.
3. 5002번에 프로퍼티들의 주소가 저장된다.
4. 'x'는 7103에 저장되고 값은 5003번 주소에 저장된다.
5. 'arr'은 7104에 저장되는데 참조형 데이터이다. 
6. 5004번에 주소(8104,8105)들이 저장되고 각각 0,1로 식별자가 입력된다.
7. 3은 할당되어 있으므로 그대로 사용하고 4는 5005번에 새로 할당한다.
8. 'ajb.arr'에 새로운 값 문자열'str'을 넣으면, 새로운 공간 5006번에 'str'이 할당된 뒤, arr의 주소 값이 변경된다.
9. 기존의 데이터가 있던 5004번과 8104번, 8105번은 링크가 사라지고 Garbage Collecting처리된다. (참조 카운트 0)



### 변수 복사

```JavaScript
var a = 10;
var b = a;
var obj1 = { C: 10, d: 'ddd'};
var obj2 = obj1;
b = 15;
obj2.c = 20;
```

|    주소    | ...  |       1002        |       1003        |         1004         |         1005         | ...  | 5002 |  5003   | 5004  | 5005 | 5006 | ...  |
| :--------: | :--: | :---------------: | :---------------: | :------------------: | :------------------: | :--: | :--: | :-----: | :---: | :--: | :--: | ---- |
| **데이터** |      | 이름: a 값: @5002 | 이름: b 값: @5002 | 이름: obj1 값: @5003 | 이름: obj2 값: @5003 |      |  10  | @7103~? | 'ddd' |  15  |  20  |      |

|    주소    | ...  |            7103             |       7104       | 7105 | 7106 | ...  |
| :--------: | :--: | :-------------------------: | :--------------: | :--: | :--: | :--: |
| **데이터** |      | 이름: c 값: @5002 ->  @5006 | 이름:d 값: @5004 |      |      |      |

* 기본형 데이터는 복사를 할 경우, 가르키는 데이터 주소를 그대로 가져온다.
  * 복사한 값을 가지고 있던 'b'의 값이 변경되면, 새로운 값이 할당된 주소를 가져오게 된다.
* 참조형 데이터도 복사를 할 경우, 가르키는 데이터 주소를 그대로 가져온다.
  * **복사한 값을 가지고 있던 'obj2.c'의 값이 변경되면, 해당 프로퍼티의 새로운 값이 할당된 주소로 바뀐다.**
  * **이러한 이유로, 원본 데이터의 값도 바뀌는 문제가 발생할 수 있다.**
  * **해결 방법: 매번 새로운 객체, 불변성**



# 2. Execution context

* 동일한 조건/환경을 지니는 코드 뭉치를 실행할 때 필요한 조건/환경정보
* 동일한 조건/환경을 지니는 코드 뭉치 : **함수 or 전역 공간**
* **함수를 실행할 때 필요한 환경정보 or 그것을 담은 객체**



### 스택

* 마지막에 들어온 것이 가장 먼저 빠지는 것

```JavaScript
var a = 1;
function outer() {
  console.log(a);    // 1번(console.log가 찍히는 순서)
  
  function inner(){
    console.log(a);  // 2번
    var a = 3;
  }

inner(); // 2번을 실행하게 함

console.log(a);   // 3번 실행
}
outer(); // 1번을 실행하게 함
console.log(a);  // 4번 실행
```

1. 전역 context가 열려 전역 공간이 한줄 한줄 실행

2. **outer()** 만나서 함수의 실행 context가 열려 1번이 실행

3. **inner()** 를 만나서 함수의 실행 context가 열려 2번이 실행



가장 나중에 열린 context가 가장 먼저 실행되므로 **스택**이다. 그리고 이렇게 실행해 관여하는 것을 **콜스택**이라고 한다.



### Call stack

* 현재 어떤 함수가 동작하고 있는지, 다음에 어떤 함수가 호출되어야하는 지 등을 제어하는 자료구조이다.
* 표로 표현하면 아래와 같다.

|   들어온 순서   |      1       |   2   |   3   |
| :-------------: | :----------: | :---: | :---: |
| **context 명**  | 전역 context | outer | inner |
| **나가는 순서** |      3       |   2   |   1   |



### inner

* VariableEnvironment: 2개의 객체를 내장하고 있다.LexicalEnvironment의 가장 처음에 수집한 정보에 대한 snapshot. 초기 값이 유지. 
  * environmentRecord (snapshot) 
  * outerEnvironmentReference (snapshot)
* LexicalEnvironment: 2개의 객체를 내장하고 있다. 이후에 값이 변경된다. 어휘적/사전적 환경.
  * environmentRecord
  * outerEnvironmentReference
* ThisBinding



### Lexical Environment

**envirionmentRecord : 현재 문백의 식별자 정보, HOISTING**

* HOISTING : 추상적인 개념. 식별자 정보를 실행 context 맨위로 끌어올리다.
* 전역공간이 처음 실행 될 때 **envirionmentRecord의 정보를 수집**한다.
* 현재 context에 선언된 **식별자들이 무엇이 있는지 수집**한다.
* 예시

```JavaScript
console.log(a());
console.log(b());
console.log(c());

function a(){ // 함수 선언문은 전체를 끌어 올린다.
  return 'a';
}
ver b = function bb() { // HOISTING
  return 'bb';
}
var c = function() { // HOISTING
  return 'c';
}
--------------------------------------------------------------------------------------------------------------
function a(){ 
  return 'a';
}
var b;
var c;                        // 끌어올려진 전체가 environmetnRecrod

console.log(a());
console.log(b());
console.log(c());

b = function bb() {
  return 'bb';
}
c = function() {
  return 'c';
}
-------------------------------------------------------------------------------------------------------------
// 실제 environmetRecord
environmentRecord{
  function a(){ ... },
  b,
  c
}
```



**outerEnvironmentaReference : 현재 문맥에 관련 있는 외부 식별자 정보**

* inner의 경우, outer의 LexicalEnvironment이다.
* outer의 경우, 전역의 LexicalEnvironment이다.

| **inner** | LexicalEnvironment        |
| --------- | ------------------------- |
|           | environmentRecord         |
|           | outerEnvironmentReference |
| **outer** | **LexicalEnvironment**    |
|           | environmentRecord         |
|           | outerEnvironmentReference |
| **전역**  | **LexicalEnvironment**    |
|           | environmentRecord         |

* Scope : outerEnvironmentReference가 관여
  * Scope : 변수의 유효 범위. Execution context에 의해 결정된다.
  * inner에서는 내부의 변수와 outerEnvironmentReference로 인해 outer의 LexicalEnvironment에 접근할 수 있다.
  * outter에서는 자신 내부의 변수와 전역의 LexicalEnvironmnet에 접근할 수 있으나, inner에서 선언한 변수에는 접근할 수 없다. 참조할 수 없기 때문이다.
  * 즉, inner에서 선언한 environmentRecord는 그 안에서만 존재한다.
  * 반면, outer에서 선언한 environmentRecrod는 inner에 접근할 수 있다.
  * 전역에서 선언한 변수는 어디서든 접근 가능
* Scope chain : 어떤 변수를 찾을 때까지 가까운 곳 부터 차례때로 찾는 것
  * 예시

|       | case 1     | case 2     | case 3     |
| ----- | ---------- | ---------- | ---------- |
| inner | var a = 1; |            |            |
| outer | var a = 2; | var a = 2; |            |
| 전역  | var a = 3; | var a = 3; | var a = 3; |

* inner에서
  * case 1 : a =1 가 나온다.
  * case 2 : a =2 가 나온다.
* 즉, 자신에게 가장 가까운 것만 접근한다. **(Shadowing)**



## 3. 코드 실행 분석하기

```JavaScript
var a = 1;
function outer() {
  console.log(a);    // 1번(console.log가 찍히는 순서)
  
  function inner(){
    console.log(a);  // 2번
    var a = 3;
  }

inner(); // 2번을 실행하게 함

console.log(a);   // 3번 실행
}
outer(); // 1번을 실행하게 함
console.log(a);  // 4번 실행
```

| 0 .    | GLOBAL                                               | Execution Context                                            | 활성화                                              |
| ------ | ---------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------- |
| **전** | 1. 변수 a 선언                                       |                                                              |                                                     |
|        | 2. 함수 outer 선언                                   |                                                              |                                                     |
| **역** | 3. 변수 a에 1 할당                                   |                                                              |                                                     |
|        | 4. outer 함수 호출 -> OUTER Execution Context 활성화 |                                                              |                                                     |
| **컨** | **O**                                                | 5. 함수 inner 선언                                           |                                                     |
|        | **U**                                                | 6. outer context에서 a탐색 <br /> -> global context에서 a 탐색 -> 1출력 |                                                     |
| **텍** | **T**                                                | 7. inner 함수 호출 <br />-> INNER Execution Context 활성화   |                                                     |
|        | **E**                                                | **I**                                                        | 8. 변수 a  선언                                     |
| **스** | **R**                                                | **N**<br />**N**                                             | 9. inner context에서 a 탐색<br /> -> undefined 출력 |
|        |                                                      | **ER**                                                       | 10. 변수 a에 3 할당                                 |
| **트** | **컨**<br />**텍**                                   | 11. inner context  종료                                      |                                                     |
|        | **스**<br />**트**                                   | 12. outer context에서 a 탐색 -> global context에서 a 탐색 -> 1출력 |                                                     |
|        | 13. outer context 종료                               |                                                              |                                                     |
|        | 14. global context에서 a 탐색 -> 1출력               |                                                              |                                                     |
| 15.    | global context 종료                                  |                                                              |                                                     |



# Reference

https://www.inflearn.com/course/핵심개념-javascript-flow