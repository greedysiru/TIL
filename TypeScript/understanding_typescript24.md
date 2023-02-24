# Understanding TypeScript(24) - More Configuration & Compilation Options

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## More Configuration & Compilation Options

```json
{
  // 어떻게 컴파일 될지에 대한 옵션
  "compilerOptions": {
    // JavaScript 허용, ts파일에서 js파일 import 가능
    "allowJs": true,
    // JavaScript 파일에서도 에러 체크
    "checkJs": true,
    // tsx파일을 jsx 파일로 어떻게 컴파일할 지
    "jsx": "preserve",
    // 컴파일시 d.ts 파일 생성(프로젝트에 존재하는 모든 타입을 포함)
    "declaration": true,
    // d.ts에 상응하는 소스맵 생성
    "declarationMap": true,
    // SourceMap: 디버깅과 개발을 도와 줌
		// ts 파일을 컴파일하여 생성된 js파일을 ts원본 파일과 연결
    "sourceMap": true,
  	...
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

