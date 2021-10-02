# 실전으로 배우는 타입스크립트 - 외부 라이브러리 모듈화

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 라이브러리 로딩 방식

### cdn에서 라이브러리를 불러오는 경우

* 자바스크립트 모듈로 인식할 수 있도록 모듈화를 해야 함
  * npm으로 설치

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
    ...
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@2.8.0"></script>
    <script src="./app.js"></script>
  </body>
</html>
```



### JavaScript Module

* NPM으로 설치된 패키지를 불러오거나 export된 함수, 변수를 가져올 수 있음

```JavaScript
// 라이브러리 로딩
import 변수명 from '라이브러리 이름';
// 변수, 함수 임포트 문법
import {} from '파일 상대 경로';
```



## 2. 라이브러리 타입 에러

* 라이브러리 내부에 타입 정의가 되어있어 별도 타입 정의를 하지 않아도 되는 라이브러리가 있는 반면 별도의 타입 정의가 필요한 라이브러리가 있음



### index.d.ts

* 외부 라이브러리를 타입스크립트가 인식할 수 있도록 타입을 지정해 놓은 것
* 라이브러리 내부적으로 제공
* 제공하지 않는 경우
  * @types/라이브러리 를 설치(해당 라이브러리의 타입이 정의된 별도 라이브러리)
  * index.d.ts를 직접 선언



### import 문법 오류 해결

```TypeScript
import Chart from 'chart.js';
```

* 위 라이브러리의 import 문의 경우 오류가 발생
* 라이브러리 내부가 CommonJS 모듈로 구성되어 있어 ES6 코드 기반에서는 위 구문이 오류가 발생하게 됨



```TypeScript
import * as Chart from 'chart.js';
```

* (* as sometihng)으로 해결



## 3. Definitely Typed

* 타입스크립트 타입 정의들을 모아놓은 오픈 소스
  * **npm i -D @tpyes/라이브러리명** 으로 설치
* 자바스크립트 라이브러리를 타입스크립트에서 인식할 수 있도록 하려면 타입 정의가 필요
  * 방대한 코드를 타입 정의하려면 비용이 높음
* [타입 정의가 제공되는 오픈소스 라이브러리 검색 사이트](https://www.typescriptlang.org/dt/search?search=)



## 4. 타입 선언 라이브러리가 제공되지 않는 외부 라이브러리 대처 방법

### tsconfing.json

* **typeRoots**: 해당하는 루트의 타입 선언을 가져옴(패키지)
  * 기본값은 **./node_modules/@types**
  * @types가 없을때 타입을 가져올 루트를 추가적으로 설정 가능

```json
{
  "compilerOptions": {
    ...
    "typeRoots": ["./node_modules/@types", "./types"]
  },
  "include": ["./src/**/*"]
}
```



### 예시

* chart.js라는 패키지가 타입 선언 라이브러리가 제공되지 않는 경우
* **types/chart.js/index.d.ts**에 타입 직접 선언

```TypeScript
declare module 'chart.js' {
  // ...
  interface MyChart {
    // ...
  }
}
```



# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)