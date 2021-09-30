# 실전으로 배우는 타입스크립트 - 점진적인 타입 적용

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 자바스크립트 프로젝트에 타입스크립트를 적용하는 순서

### 타입스크립트 프로젝트 환경 구성

* NPM을 초기화하여 **package.json** 파일 생성
* 프로젝트 폴더에서 **npm i typescript -D**를 입력하여 라이브러리 설치
* 타입스크립트 설정 파일 **tsconfig.json**을 생성하고 기본 값 추가
* 서비스 코드가 포함된 자바스크립트 파일을 타입스크립트로 변환
* **tsc** 명령어로 타입스크립트 파일을 자바스크립트로 변환

```json
{
  "compilerOptions": {
    "allowJs": true,
    "target": "ES5",
    "outDir": "./dist",
    "moduleResolution": "Node",
    "lib": ["ES2015", "DOM", "DOM.Iterable"]
  },
  "include": ["./src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```



## 2. 엄격하지 않은 환경(loose type)에서 프로젝트 돌려보기

* 테스트코드가 있다면 테스트코드가 통과하는지 확인
* 프로젝트의 자바스크립트 파일들을 타입스크립트 파일로 변환
  * 서비스에 직접적인 영향을 미치는 중요한 파일들부터 점진적으로 변환
* 타입스크립트 컴파일 에러가 나는 것 위주로만 먼저 에러가 나지 않게 수정
  * **기능을 변경하지 않도록 주의**
* 테스트코드가 성공하는지 확인



## 3. 명시적 any 선언

* 프로젝트 테스트 코드가 통과하는지 확인
* 타입스크립트 설정 파일에 **noImplicitAny: true**를 추가
  * 적어도 any로 타입을 지정해야 함
* 가능한 타입을 적용할 수 있는 모든 곳에 타입 적용
  * 당장 적용하기 어려우면 **any**를 선언
  * 라이브러리를 사용하는 경우, **Definitely Typed**에서 **@types** 관련 라이브러리 설치
* 테스트 코드가 통과하는지 확인



### noImplicitAny

* true인 경우 모든 함수와 변수에 타입을 적용해야 함
* 파악하기 어려운 경우, any로라도 적용



## 4. 화살표 함수 타입 정의

* ES6+ 문법의 함수 선언 방법인 화살표 함수의 타입 정의는 아래와 같다.

```TypeScript
const sum = (a: number , b:number): number => {
  return a + b;
}
```



* 화살표가 하나인 경우에는 괄호를 생략할 수 있지만, 타입을 지정할 때는 괄호가 필요하다.

```TypeScript
const callNumber = (a: number): number => {
  return a;
}
```



## 5. DOM 관련 타입 구체화

### 예시1

* 선택자 정보를 받아 querySelector를 이용하여 DOM 요소를 리턴하는 함수
* 선택자는 문자열로 입력되므로 파라미터는 **string** 타입

```TypeScript
function $(selector: string) {
  return document.querySelector(selector);
}
```



### 예시2

* id 문자열을 받아와 해당 id를 가지는 요소를 만들어 리턴하는 함수
* id는 문자열로 입력되므로 파라미터는  **string** 타입

```TypeScript
function createSpinnerElement(id: string) {
  const wrapperDiv = document.createElement('div');
  wrapperDiv.setAttribute('id', id);
  wrapperDiv.setAttribute(
    'class',
    'spinner-wrapper flex justify-center align-center',
  );
  const spinnerDiv = document.createElement('div');
  spinnerDiv.setAttribute('class', 'ripple-spinner');
  spinnerDiv.appendChild(document.createElement('div'));
  spinnerDiv.appendChild(document.createElement('div'));
  wrapperDiv.appendChild(spinnerDiv);
  return wrapperDiv;
}
```



## 6. API 함수 타입 구체화

* API 문서를 참고하여 파라미터들이 각각 어떤 타입을 가질지 확인하여 타입 지정

```TypeScript
enum CovidSatus {
  confirmed = 'confirmed',
  Recovered = 'recovered',
  Deaths = 'deaths'
}
function fetchCountryInfo(countryCode: string, status: CovidSatus) {
  // status params: confirmed, recovered, deaths
  const url = `https://api.covid19api.com/country/${countryCode}/status/${status}`;
  return axios.get(url);
}
```



### 내장 객체 타입 정의

* 자바스크립트 내장 객체이면 타입이 추론됨

```TypeScript
function getUnixTimestamp(date: Date) {
  return new Date(date).getTime();
}
```



## 7. DOM 함수 관련 타입 오류 분석 & 해결

### 오류 분석

```typescript
function $(selector: string) {
  return document.querySelector(selector);
}

...

// DOM
const deathsTotal = $('.deaths');

...

function setTotalDeathsByCountry(data: any) {
  // deathsTotal: Element
  deathsTotal.innerText = data[0].Cases; // 'Element' 형식에 'innerText' 속성이 없습니다.ts(2339)
}
```

* deathsTotal은 특정 태그를 접근해서 가져온 변수
  * Element 타입
* **Element는 lib.dom.d.ts에 정의된 구현체**
  * 가장 기본적인 DOM 객체 타입 구조체
  * HTMLElement: Element를 상속받아 확장한 구조체
  * HTMLParamElement: 더 구체적인 구조체(p태그)
* $함수를 이용하여 가져온 요소를 deathsTotal에 할당하면 Element 타입이 추론되어 할당
* Element 타입에는 innerText 속성이 없으므로 오류 발생



### 오류 해결

```TypeScript
function $(selector: string) {
  return document.querySelector(selector);
}

...

// DOM
const deathsTotal = $('.deaths') as HTMLParagraphElement;

...

function setTotalDeathsByCountry(data: any) {
  deathsTotal.innerText = data[0].Cases;
}
```

* 가져온 요소를 할당할 때 타입 단언을 이용하여 HTMLParagraphElement를 타입 지정
  * 해당 타입엔 innerText가 있으므로 오류 해결
* deathsTotal에 HTMLParagraphElement를 할당하면 오류가 발생
  * $함수로 가져온 요소는 Element 타입 인데, 변수 할당시에 서로 타입이 맞지 않으므로 발생

# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)

