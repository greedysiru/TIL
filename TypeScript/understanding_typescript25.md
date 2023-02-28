# Understanding TypeScript(25) - rootDir and outDir

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## rootDir and outDir

* 프로젝트를 유지, 보수 및 개발할 때 파일들을 정리해야만 함
* 전형적으로 src 폴더에는 소스코드를, dist 폴더에는 배포할 빌드된 파일들이 위치
* outDir: 컴파일된 파일들이 어디에 위치해야 하는지
  * 디렉토리 구조가 유지되어 위치하게 됨
* rootDir: 컴파일할 대상 디렉토리를 지정
  * 기본적으로 TypeScript Compiler는 프로젝트 내의 모든 TypeScript 파일들을 컴파일



### tsconfig.json

```json
{
  "compilerOptions": {
    // 컴파일된 파일들이 dist 폴더에 위치
    // ex) ./src/dist/common.ts -> ./dist/utils/common.js
    "outDir": "./dist",
    // 컴파일할 디렉토리를 지정
    "rootDir": "./src"
  }
}
```





# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

