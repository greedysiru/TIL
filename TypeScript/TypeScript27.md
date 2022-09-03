# TypeScript(8)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. tsconfig.json

* TypeScript 설정 파일
* IDE가 이를 감지하여 프로젝트에서 TypeScript로 작업하는 것을 알게 됨
  * 자동완성기능 제공

### 예시

```json
{
  // where, 어디에 타입스크립트 파일이 있는 지
  // TypeScript -> JavaScript로 컴파일하고 싶은 모든 디렉터리 넣기
  "include": ["src"],
  // 컴파일 옵션
  "compilerOptions": {
    // JavaScript 파일이 생성될 디렉터리 지정
    "outDir": "build",
    // 어떤 버전의 JavaScript로 컴파일 할 지
    "target": "ES6",
    // TypeScript가 어떤 런타임 환경에서 동작할 지 알려줌
    "lib": ["ES6", "DOM"],
    // 엄격 모드
    "strict": true,
    // JS 허용
    "allowJs": true
  }
}
```



## 2. Declaration Files

* TypeScript는 내장된 JavaScript API를 위한 기본적인 타입 정의를 가지고 있음
* tsconfig에서 lib 속성에 ES6, DOM을 지정하면 이에 맞는 d.ts(타입 정의) 파일을 가져오게 됨
  * call signatures 및 interface 등이 정의되어 있음



## 3. JSDoc

* @ts-check
  * TypeScript가 JavaScript를 체크
* JSDoc
  * 코멘트로 이루어진 문법
  * 함수 위에 코멘트를 적으면, TypeScript가 이 코멘트를 읽을 수 있음
* 큰 규모의 JavaScript 프로젝트를 TypeScript로 한번에 바꾸기는 어려움
  * JSDoc을 활용하여 점진적으로 JS -> TS

```javascript
// @ts-check

/**
 * 고양이가 우는 소리를 return
 * @param {string} who
 * @returns {string}
 */
export function cry(who) {
  if (who === 'cat'){
    return '야옹';
  }
  if (who === 'dog'){
    return '멍멍';
  }
}

```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

