# 실전으로 배우는 타입스크립트 - 타입 시스템 적용

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 기존 자바스크립트 코드에 타입스크립트 적용시 주의할 점

* 기능적인 변경은 절대 하지 않을 것
  * 타입을 입히는 것을 우선으로 할 것
* 테스트 커버리지가 낮을 땐 함부로 타입스크립트를 적용하지 않을 것
* 처음부터 타입을 엄격하게 적용하지 않을 것
  * 점진적으로 strict 레벨을 증가
  * any타입으로 루즈하게 시작



## 2. 타입스크립트 기본 환경 구성

- NPM 초기화
- 타입스크립트 라이브러리 설치
- 타입스크립트 설정 파일 생성 및 기본 값 추가



## 3. 점진적인 타입 시스템 적용 - JSDoc

* 코드 상단에 **@ts-check** 를 주석 추가하면 TypsScript Language Server가 실행
* JavaScript임에도 불구하고 타입정의가 가능해짐
* 가독성, 생산성, 재활용 측면에서 좋지 않음
  * 초기 타입 시스템 적용시에만 사용
  * 타입스크립트를 도입하는 것에 비용이 너무 클 경우 JSDoc 도입 고려



### JSDoc을 사용하여 api 호출 응답 타입 정의

* api 호출 응답 타입 지정
  * api 문서를 참고
  * 사이트에서 직접 호출하여 응답 확인

```TypeScript
// @ts-check
...
/**
 * @typedef {object} CovidSummary
 * @property {Array<object>} Country
 */
...
/** 
 * @returns {Promise<CovidSummary>}
*/
function fetchCovidSummary() {
  const url = 'https://api.covid19api.com/summary';
  return axios.get(url);
}
...
async function setupData() {
  const { data } = await fetchCovidSummary();
  setTotalConfirmedNumber(data);
  setTotalDeathsByWorld(data);
  setTotalRecoveredByWorld(data);
  setCountryRanksByConfirmedCases(data);
  setLastUpdatedTimestamp(data);
}
```



## 4. 타입스크립트 프로젝트 구성 및 기본 설정 추가

### NPM 초기화

* 프로젝트 폴더에서 NPM 초기화

```shell
npm init -y
```



### 타입스크립트 라이브러리 설치

* 타입스크립트를 적용할 수 있도록 설치

```shell
npm i typescript --save -dev
```



### 타입스크립트 설정 파일 생성 및 기본 값 추가

* **tsconfig.json**에 프로젝트에서의 타입스크립트 설정 정의
* allowJS: 타입스크립트 컴파일 작업 진행할 때 자바스크립트 파일도 포함될 수 있는지를 설정해주는 속성
  * 기존에 존재하는 자바스크립트 프로젝트에 타입스크립트 점진적 적용시 사용
* target: 타입스크립트 파일을 컴파일 후 빌드 디렉토리에 생성되는 자바스크립트의 버전
* outDir: 빌드 디렉토리
* moduleResolution: 모듈 해석 전략 지정
* lib: 타입스크립트 파일을 자바스크립트로 컴파일 할 때 포함될 라이브러리 목록
  * ES2015: 프로미스와 같은 ES2015 문법을 타입스크립트에서 인식
  * DOM: DOM API
* include: 변환할 폴더를 지정

```TypeScript
{
  "compilerOptions": {
    "allowJs": true,
    "target": "ES5",
    "outDir": "./built",
    "moduleResolution": "Node",
    "lib": ["ES2015", "DOM", "DOM.Iterable"]
  },
  "include": ["./src/**/*"]
}
```



### 타입스크립트 컴파일 하기

*  package.json에서 sripts 추가

```json
...
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "tsc"
  },
...
```



## 5. 기존 서비스에 TS 적용할 때 알아두면 좋은 점

### 빌드시에 타입 에러가 발생 했을 때

* 타입스크립트 컴파일 시, 에러가 발생했음에도 불구하고 빌드가 됨
* 타입스크립트 관점에서의 에러(타입 에러)이지, 동작과 관련된 에러가 아님
* 타입 에러와 런타임 에러는 서로 관계가 없을 수도 있음



### 기존 서비스에 JavaScript 파일이 많을 때

* tsconfig.json의 allowJS 옵션이 true이면 JavaScript 파일을 허용
  * 점진적 적용
* 모든 JavaScript 파일을 TypeScript로 바꿀 필요 없음
* 타입 에러로 인해 런타임 오류가 우려되는 파일만 선택적으로 TypeScript 적용



## 6. 타입스크립트 에러 디버깅 방법

* 에러코드나 에러메시지를 구글링하기
  * 스택오버플로우나 관련 문서를 참고하기

# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)