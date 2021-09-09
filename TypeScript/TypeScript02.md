# 타입스크립트 입문 - 타입스크립트 시작하기

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 타입스크립트 프로젝트 시작하기

### 타입스크립트 설치

```shell
npm i  typescript -g
```

* -g: npm 전역 설치 옵션
  * 시스템 레벨에서 사용하기 위해서 설치할 때 사용
  * mac의 경우 **/usr/local/lib/node_modules**에 설치



### 컴파일 하기

* **.ts 확장자**로 이루어진 파일을 **.js 확장자** 파일로 컴파일
* Webpack과 같은 모듈 번들러로 컴파일 할 수 있다.

```shell
tsc index.ts
```



## 2. 타입스크립트 설정 파일

* 컴파일 할 때 별도의 옵션을 설정할 수 있다.
* tsconfig.json에 설정
  * 객체의 형식으로 key, value 지정
  * compilerOptions: 컴파일 시의 부가적인 옵션
  * allowJs: 해당 프로젝트 안에 자바스크립트 허용
  * noImplicitAny: 최소한 any타입을 설정해야 함

```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": true
  }
}
```



## 3. 타입스크립트 플레이그라운드

* [플레이그라운드 사이트](https://www.typescriptlang.org/play?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCoASMFmgY7p7ehCTkVOle4jUMdRLYTqCc8LEZzCZmoNJODPHFZZXVtZYYkAAeRJTInDQS8po+rf40gnjbDKv8LqD2jpbYoACqAEoAMsK7sUmxkGSCc+VVQQuaTwVb1UBrDYULY7PagbgUZLJH6QbYmJAECjuMigZEMVDsJzCFLNXxtajBBCcQQ0MwAUVWDEQNUgADVHBQGNJ3KAALygABEAAkYNAMOB4GRogLFFTBPB3AExcwABT0xnM9zsyhc9wASmCKhwDQ8ZC8iElzhB7Bo3zcZmY7AYzEg-Fg0HUiS58D0Ii8AoZTJZggFSRxAvADlQAHJhAA5SASAVBFQAeW+ZF2gldWkgx1QjgUrmkeFATgtOlGWH0KAQiBhwiudokkuiIgMHBx3RYbC43CCJSAA)
* 타입스크립트를 자바스크립트로 변환된 코드를 볼 수 있는 사이트

# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)