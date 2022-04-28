# 31장. RegExp(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 31.4 플래그

* 정규 표현식의 검색 방식을 설정하기 위해 사용
  * 총 6개 존재
* i(Ignore case): 대소문자 구별하지 않음
* g(Global): 대상 문자열 내에서 패턴과 일치하는 모든 문자열 전역 검색
* m(Multi line): 행이 바뀌어도 검색



## 31.5 패턴

* 문자열의 일정한 규칙을 표현
* /(슬래시)로 열고 닫음
* 메타문자: 특별한 의미를 가지는 문자



### 31.5.1 문자열 검색

* 패턴으로 지정한 문자열을 검색
  * 메서드를 사용하여 검색 수행

```JavaScript
const regExp = /siru/;

const target = 'siru is babo';

regExp.test(target); // true
```



### 31.5.2 임의의 문자열 검색

* .은 임의의 문자 한 개 의미

```JavaScript
const target = '링딩동 링딩동 링디기딩딩 링딩동 딩동댕';

const regExp = /.../g;

target.match(regExp); // ["링딩동", " 링딩", "동 링", "디기딩", "딩 링", "딩동 ", "딩동댕"]
```



### 31.5.3 반복 검색

* {m,n}: m번 ~ n번 반복되는 문자열 의미
* {n}: n번 반복되는 문자열 의미
* {n, }: n번 이상 반복 되는 문자열 의미
* 플러스(+): 앞선 패턴이 최소 한번 이상 반복
* 물음표(?): 0번이상반복 되는 문자열

```JavaScript
const target = '암욜맨 따라따따 그대여';

const regExp1 = /따{1,2}/g;

const regExp2 = /따+/g;

const regExp3 = /따?/g;

target.match(regExp1); // ["따", "따따"]

target.match(regExp2); // ["따", "따따"]

target.match(regExp3); // ['', '', '', '', '따', '', '따', '따', '', '', '', '', '']
```



### 31.5.4 OR 검색

* |: or의 의미
* []: 대괄호 내의 문자는 or로 동작
  * 또는 범위 지정 ex) [A-Z]

```JavaScript
const target = '개고양이 고양이 개 개 개개개 고양이고양이개 개고양이 개양이';

const regExp1 = /개|고양이/g;

const regExp2 = /[개고양이]/g;

target.match(regExp1); // ['개', '고양이', '고양이', '개', '개', '개', '개', '개', '고양이', '고양이', '개', '개', '고양이', '개']

target.match(regExp2);
// ['개', '고', '양', '이', '고', '양', '이', '개', '개', '개', '개', '개', '고', '양', '이', '고', '양', '이', '개', '개', '고', '양', '이', '개', '양', '이']
```



### 31.5.5 NOT 검색

* 캐럿(^): 대괄호 안에 있을 시 not

```JavaScript
const target = '개고양이 고양이 개 개 개개개 고양이고양이개 개고양이 개양이';

const regExp = /[^개]+/g;

target.match(regExp); // ['고양이 고양이 ', ' ', ' ', ' 고양이고양이', ' ', '고양이 ', '양이']
```



### 31.5.6 시작 위치로 검색

* 캐럿(^): 문자열의 시작

```JavaScript
const target1 = '시루 안녕';

const target2 = '누누 안녕';

const regExp = /^시루/;

regExp.test(target1); // true

regExp.test(target2); // false
```



### 31.5.7 마지막 위치로 검색

```JavaScript
const target1 = '시루 안녕';

const target2 = '누누 안녕';

const regExp = /안녕$/;

regExp.test(target1); // true

regExp.test(target2); // true
```

