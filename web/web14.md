

# 모듈 번들러와 빌드도구

**본 내용은 10분 테코톡 썬님의 강의를 토대로 작성하였습니다.**



## 1. module

* 분리된 코드의 조각
* 시스템을 이루는 **논리적인 일부분**
* **EcmaScript modules(ESM)**: 자바스크립트의 모듈 시스템은 2015년에 정식으로 도입



## 2. CommonJS

* 많은 자바스크립트 파일을 스크립트 태그를 통해 가져왔을 때, 변수가 겹치면 덮어씌워질 것이다.
  * 예측하기 어렵고 오류가 발생한다.
* 모듈화를 위해서
  * 스코프: 각 모듈을 독립적 스코프를 가진다.
  * 정의: 모듈을 정의할 수 있어야 한다.
  * 사용: 모듈을 사용할 수 있어야 한다.
* 2009년 CommonJS 등장
  * 각각의 파일이 독립적인 스코프를 가지며
  * module.exports를 통해 모듈을 정의
  * require 문법을 통해 모듈을 사용
  * 모든 파일이 로컬에 존재하여 바로 불러올 수 있음을 전제
  * 동기적으로 동작
  * node.js에서 사용됨



### 예시

```JavaScript
module.exports
require('./file.js')
```





## 3. Asynchronous Module Definition(AMD)

* 브라우저 내 실행에 중점을 두고 비동기 모듈 사용
* dojo tookit, require.js



### 예시

```JavaScript
// id: 모듈 식별 인수, dependecies: 모듈의 의존성 배열, factory: 모듈의 실제 구현
// 파일 스코프 역할
define(id?, dependencies?, factory);

require([modulePath], function(module)(){
  // module을 활용하는 실제 코드
});
```



## 4. Universal Module Definition(UMD)

* Common.js 와 AMD를 지원하기 위한 디자인 패턴



## 5. Module Bundler

* 모든 파일을 네트워크 통신을 통해 가져와야 함
  * js, html, css, 이미지 파일
* 모듈 번들러는 여러 모듈을 모아 번들링하여 문제 해결



### 웹팩

* 모든 파일을 모듈로 본다.
  * js, css, 이미지, 폰트 등
* CommonJS 기반
  * module.exports
* 서로 의존성을 가진 여러 모듈을 돌며 여러 개의 자바스크립트 파일을 하나의 자바스크립트로, sass파일을 css파일로 묶음
* 세 가지 필수 설정
  * mode: 개발 또는 프로덕션과 같은 모드
  * entry: 모듈이 시작되는 부분(index.js)
  * output:  번들링된 파일들을 저장할 위치(dist, build)



### 웹팩 - 로더

* 로더(loader): 웹팩이 자바스크립트 파일이 아닌 웹 자원(HTML, CSS, 이미지, 폰트 등)을 변환할 수 있도록 도움
* css-loader: CSS파일을 모듈로서 가져올 수 있게 함
* style-loader: 자바스크립트로 들어간 CSS를 HTML에 넣어 브라우저 렌더링 시 적용할 수 있게 함
* file-loader: 이미지를 모듈로 사용할 수 있게 함



### 웹팩 - 플러그인

* 플러그인(plugin): 로더가 해석하고 번들된 결과물의 형태를 바꾸는 일을 함. 후처리 역할
* 난독화나 특정 문자열 치환 처리
* Define Plugin: 환경 의존적인 정보를 관리하는데 사용



### rollup.js

* ESM을 사용하는 모듈 번들러



## 6. 트랜스파일러

### 바벨

* 크로스 브라우징 문제: 서로 다른 브라우저 스펙으로 인해 하나의 프로젝트 코드로 모든 브라우저를 커버하지 못하는 것
* 트랜스파일러는 크로스 브라우징 문제를 해결
* 최신 스펙의 코드를 브라우저마다 동일하게 동작하도록 변환
* 최신 스펙의 JS, TS, JSX로 작성된 코드 변환
* 코드 변환은 3단계에 걸쳐 이루어짐
  * 코드를 각 토큰으로 분해
  * ES5 스펙으로 변환
  * 변환된 코드를 출력



## 7. 빌드 도구

### Snowpack

* 빠른 빌드를 가능하게 함
* 번들 과정이 없으며 캐시를 사용하여 변경되지 않은 파일은 다시 빌드하지 않음
  * 브라우저가 ESM을 지원하기 때문에 가능
* 번들링이 필요할 시, 웹팩이나 rollup.js를 추가로 사용

# Reference

[[10분 테코톡] 썬의 모듈 번들러와 빌드도구](https://www.youtube.com/watch?v=9b89f21Sizs)