# 실전으로 배우는 타입스크립트 - API 함수 타입 정의

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. API 함수 타입 정의

* Axios는 라이브러리 내부의 index.d.ts에 정의된 AxiosResponse 타입을 Promise로 반환한다.
* 제네릭을 사용하여 아래와 같이 타입 지정한다.

```TypeScript
// app.ts
// CovidSummaryResponse는 해당 api가 응답하는 데이터의 타입
function fetchCovidSummary(): Promise<AxiosResponse<CovidSummaryResponse>> {
  const url = 'https://api.covid19api.com/summary';
  return axios.get(url);
}
```



## 2. 타입 모듈화

* API 함수 타입을 정의할 때 타입 코드가 너무 길어지면 가독성, 유지보수 측면에서 좋지 않음
* 도메인 별로 타입을 모아서 정리하는 것이 좋음

```TypeScript
// covid/index.ts
interface Conutry {
  Country: string;
  CountryCode: string;
  Date: string;
  NewConfirmed: number;
  NewDeths: number;
  NewRecovered: number;
  Premium: any;
  slug: string;
  TotalConfirmed: number;
  TotalDeaths: number;
  TotalRecovered: number;
}

interface Global {
  NewConfiremd: number;
  NewDeaths: number;
  NewRecovered: number;
  TotalConfirmed: number;
  TotalDeaths: number;
  TotalRecovered: number;
}

export interface CovidSummaryResponse {
  Countries: Conutry[];
  Date: string;
  Global: Global;
  Message: string;
}

```



## 3. reduce API

* 배열 API
* 배열의 각각의 요소를 순회하며 이전 연산 값을 가져와 연산
  * 누적합
* 첫번째 파라미터에 콜백함수가 필요
  * 어떤 연산을 할 것인지에 대해 정의된 콜백함수
* 두번째 파라미터에 초기값 설정

```JavaScript
const pets = [{name: 'siru', age: 6}, {name: 'nunu', age: 3}];

pets.reduce((total, currentItem) => {
  total = total + currentItem.age;
  // return을 해야 값이 누적됨
  return total;
}, 0; // 9
```

# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)