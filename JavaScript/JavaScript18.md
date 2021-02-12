# [코드잇] 프로그래밍 핵심 개념 in JavaScript (1)(2021.2.12)



**상세 내용 [블로그](https://greedysiru.tistory.com/197) 참고**



# 자료형

## 01. 숫자형

* **숫자형태의 자료형**
* 일반적인 사칙연산의 우선순위 규칙을 따른다.

```JavaScript
// 덧셈
console.log(1 + 2);

// 뺄셈
console.log(2 - 1);

// 곱셈
console.log(2 * 3);

// 나눗셈
console.log(5 / 2);

// 나머지
console.log(7 % 3);

// 거듭제곱
console.log(2 ** 3);
```



## 02. 문자열 기본

* **글자를 값으로 표현하는 자료형**
* 같은 짝 따옴표로 둘러싸서 표현



## 03. 문자열 활용

* 역슬래시를 사용하면 따옴표 안에서 따옴표를 사용 가능
* 백틱(`)을 사용하면, 안의 문자열을 따옴표를 포함하여 그대로 출력한다.
* 문자열끼리의 덧셈(+)은 문자열을 연결한다.

```JavaScript
console.log("I\'m greedysiru");
console.log(`I'm greedysiru`);
console.log('greedy' + 'siru');
console.log('3' + '5'); // 35 출력
```



## 04. 불 대수

* **일상적인 논리를 수학적으로 표현한 것**
* 불대수의 값, **진리값**
  * 어떤 명제가 참인지, 거짓인지를 나타낸다.
  * **True, False**
* 불 대수의 연산
  * AND, OR, NOT



### 명제

* **참과 거짓이 확실한 문장**
* 질문, 주관적인 문장은 명제가 아님



### AND 연산

* x와 y가 **모두 참**일 때, x AND y는 **참**
* **하나라도 거짓**이면, x AND y는 **거짓**



### OR 연산

*  x와 y중 **하나라도 참**이면, x OR y는 **참**
* x와 y **모두가 거짓**이면, x OR y는 **거짓**



### NOT 연산

* **참이면 거짓으로, 거짓이면 참으로 바꾼다.**



## 05. 불린형

* **참과 거짓을 표현하는 자료형**
  * ture, false



### 숫자비교

> 3 >= 2
>
> 3은 2보다 크거나 같다.(true)
>
> 3 <= 2
>
> 3은 2보다 작거나 같다.(false)
>
> 3 === 3
>
> 3과 3은 값이 일치한다. (ture)
>
> 3 !== 3
>
> 3과 3은 일치하지 않는다.(false)

* 등호는 뒤에 쓸 것



### 불린 연산

* **AND(&&)**
* **OR(||)**
* **NOT(!)**
  * 중첩해서 사용할 수 있다.



## 06. typeof 연산자

* **어떤 자료형인지 확인하는 연산자**
* 사칙연산보다 우선순위가 높다.
  * 괄호를 넣어서 우선순위를 줄 것

```Javascript
console.log(typeof 1); // number
console.log(typeof 1.0); // nuber
console.log(typeof '1'); // string
console.log(typeof 'hello' + 'Codeit') // stringCodeit
console.log(typeof 8 - 3); // NaN
console.log(typeof (8 - 3)); // number
```



## 07. 형변환 I

* **자료형을 다른 자료형으로 바꾸는 것**
* **String, Number, Boolean**함수 사용
* true는 숫자로 형변환 하면 1, false는  0
* 존재하는 값을 불린으로 변환하면 true로 된다.
* 없거나 비어있는 경우 false로 변환된다.
  * **falsy : ' ', 0, NaN**



### 문자열로 변환

```JavaScript
console.log(String(10) + String(5)); // 105
```



### 숫자로 변환

```JavaScript
console.log(Number('10') + Number('5')); // 15
```



## 08. 형변환 II

* **JavaScript에서는 일정한 규칙에 따라서 자료형을 변환할 수 있다.**



### 산술 연산

* **연산되어지는 두 값을 숫자형으로 바꾼뒤 연산한다.**
* **주의 : +의 경우, 문자열을 연결하는 기능도 있음**
  * 한쪽이라도 문자열이 있다면, 양쪽 모두를 문자열로 연결한다.
* NaN은 어떤것과 연산을 하여도, NaN이 나온다.

```JavaScript
console.log(4 + '2'); // 42
console.log(4 + 2); // 6
console.log(4 - true); // 3
console.log(4 * false); // 0
console.log(4 / '2'); // 2
console.log('4' ** true); // 4
console.log(4 % 'two'); // NaN
```



### 관계비교 연산

* **산술 연산자처럼 두 값을 숫자로 비교한다.**

```JavaScript
console.log(2 < '3'); // true
console.log(2 > true); // true
console.log('2' <= false);  // false
console.log('two' >= 1); // false
```



### 같음 비교 연산

* **=== : 일치**
  * 형변환이 일어나지 않는다.
* **== : 동등**
  * 숫자형태로 형변환이 일어난다.
* **!== : 불일치**
* **!= : 부등**

```JavaScript
console.log(1 === '1') // false
console.log(1 === true) // false
console.log(1 == '1') // true
console.log(1 == true) // true
```



## 09. 템플릿 문자열

* **일정한 틀, 형식을 가진 문자열**
* 백틱(`) 사용
* **${ }**안에 변수, 연산식 등 자유롭게 넣을 수 있다.

```JavaScript
let year = 2020;
let month = 2;
let day = 12;

function getLeftMonth(x){
  return 12 - x;
}

console.log(`생년월일은 ${year}년 ${month}월 ${day}일 입니다. 올해는 ${getLeftMonth(month)}달 남았습니다.`);
```



## 10. null과 undefined

* **값이 없다는 의미**
* null : **의도적으로 표현**할 때 사용하는 값
* undefined : 값이 없다는 것을 **확인하는 값**

```JavaScript
let codeit; // 값이 지정되지 않은 변수
console.log(codeit); // undefined
codeit = null; // 의도적으로 값이 없다는 의미
console.log(codeit); // null
```



### 일치 비교시

```JavaScript
console.log(null == undefined); // true
console.log(null === undefined); // false
```

* 동등 비교시, 서로 비슷한 의미이므로 true
* 일치 비교시, 서로 다른 자료형이므로 false



# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)