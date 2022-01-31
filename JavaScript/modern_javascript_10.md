## 08장 - 제어문

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 8.0 제어문이란?

* 조건에 따라 코드 블록을 실행, 반복실행할 때 사용
  * 코드 블록: 중괄호({})로 감싼 것
* 코드의 실행을 인위적으로 제어
  * 가독성을 해치는 단점
  * 함수형 프로그래밍 기법에서는 고차함수(파이프라인)을 활용하여 제어문의 사용 억제
  * JavaScript의 고차함수 : forEach, map, filter



## 8.1 블록문

* 0개 이상의 문을 중괄호로 묶은 것
* 하나의 실행 단위 취급
  * 단독 사용 가능
* **블록문은 자체 종결성을 가진다.**
  * 문의 끝에 세미 콜론을 붙일 필요가 없음



## 8.2 조건문

* 주어진 조건식 평과 결과에 따라 코드 블록의 실행 결정
* 조건식 : 불리언 값으로 평가될 수 있는 **표현식**
  * 자바스크립트 엔진에 의해 암묵적 타입변환이 일어날 수 있음



### 8.2.1 if...else 문

* 코드 블록 내의 블록 문이 하나면 중괄호 생략 가능
* 조건식의 평가 결과가 true인 경우 if 문의 코드 블록 실행
  * false인 경우 else문의 코드 블록 실행
* 추가적인 조건 에서의 실행은 else if문으로 정의 가능



```JavaScript
const age = 28;
const isAdult = age > 18? true : false;

if (isAdult) {
  console.log('성인 입니다.');
} else if (age > 13) {
  console.log('중학생 이상입니다.');
} else {
  console.log('어린이 입니다.');
}
```



### 8.2.3 switch 문

* 주어신 표현식을 평가한 뒤, 그 값과 일치하는 case 문으로 실행흐름을 옮김
* case문 : 각 상황에 맞는 값을 지정하고 콜론으로 마침
  * case문 하위에는 실행할 문을 정의
* default문 : 모든 case문에 충족하지 않은 경우 하위의 문을 실행
* break: case 문의 실행문 끝에 break를 적어야 해당 문 실행 후 다음 case문을 거치지 않음
  * 적지 않은 경우, 다음 case문들을 거치며 조건이 충족되면 그 문을 실행하게 됨(폴스루, fall through)
  * 이를 응용할 수 있으나, 가독성이 떨어져 이해하기 어렵게 될 수도 있음
* 조건이 더 많을 때 사용



```JavaScript
var petName = 'siru';
var isMyPet;

switch (petName) {
  case 'mango': isMyPet = false;
    break;
  case 'nunu': isMyPet = false;
    break;
  case 'meonji': isMyPet = false;
    break;
  case 'siru': isMyPet = true;
    break;
}
```



## 8.3 반복문

* 조건식의 평가 결과가 참일 때 코드 블록을 실행



### 8.3.1 for문

* 조건식이 거짓일 아닐 때 코드 블록 반복 실행
* 변수 선언문은 단 한번 실행
* 선언문 실행 이후 조건식 실행
* 조건식이 true이면 코드 블록 실행
* 코드 블록 실행 이후 증감식 실행



```JavaScript
// 변수 선언문; 조건식; 증감식
for (let i = 0; i < 4; i++) {
  console.log(`시루는 츄르를 ${i}번 먹었다.`);
}

// 결과
// 시루는 츄르를 0번 먹었다.
// 시루는 츄르를 1번 먹었다.
// 시루는 츄르를 2번 먹었다.
// 시루는 츄르를 3번 먹었다.
```



### 8.3.2 while 문

* for문과 동일하게, 조건식이 참일 때 코드블록 반복 실행
  * for문과 달리, 종료 조건이 명확하지 않을 때 사용
* 무한루프에 빠질 위험이 있음
  * 방지하기 위해서, if문과 break 문을 사용

```JavaScript
let count = 0;

while (true) {
  console.log(`시루는 츄르를 ${count}번 먹었다.`);
  count += 1;
  // count가 4이면, while문 종료(코드 블록 탈출)
  if (count === 4) {
    break;
  }
}
```



### 8.3.3 do ...while 문

* 코드 블록 먼저 실행하고 조건식을 평가
  * 무조건 코드 블록이 한 번 이상은 실행 됨



```JavaScript
let count = 0;

do {
  console.log(`시루는 츄르를 ${count}번 먹었다.`);
  count += 1;
} while (count < 5)
```



## 8.4 break 문

* 레이블 문, 반복문, switch문의 코드 블록 탈출
  * 이외의 코드 블록에서 사용시 SyntaxError 발생
* 레이블문: 식별자가 붙은 문
  * 레이블 문 탈출 시, break 문에 레이블 식별자를 지정
* 레이블문은 프로그램 흐름을 복잡하게 만들어 가독성을 떨어뜨리고 오류 발생을 높일 수 있으므로 지양
* 레이블 문 의외에서는 break문에 레이블 식별자를 지정하지 않아도 됨



## 8.5 continue 문

* 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킴
* 특정 조건에서 코드 블록의 실행을 넘기고 싶을 때 사용



```JavaScript
// 고양이들의 이름이 있는 배열
const cats = ['siru', 'nunu', 'mango', 'meonji', 'kong'];

// 검색할 고양이의 이름
const searchForCatName = 'siru';

// 검색된 고양이의 위치
let positionForCat;

// for문으로 배열을 순회
for (let i = 0; i < cats.length; i++){
  // 검색할 고양이 이름이 아니면 지나가기
  if (cats[i] !== searchForCatName) {
    continue;
  }
  // 검색한 고양이인 경우 위치 입력
  positionForCat = i;
}

// 결과 출력
console.log(`검색한 ${searchForCatName}은(는) ${positionForCat}에 있습니다!`); // 검색할 시루은(는) 0에 있습니다!
```

