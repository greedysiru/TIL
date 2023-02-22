# Understanding TypeScript(21) - Including & Excluding Files

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Including & Excluding Files

### tsconfig.json

* TypeScript Project를 관리하는 중요 파일
* include와 exclude에 디렉토리 또는 파일이 겹치면
  * include - exclude 하여 남은 파일들이 컴파일

```TypeScript
{
  "compilerOptions": {
   ...
  },
  // include - exclude
  // 컴파일 제외할 대상
  "exclude": [
    // dev가 포함된 ts 파일인 경우 컴파일 제외
    "*.dev.ts",
    // 모든 폴더 안의 dev가 포함된 ts 파일인 경우 컴파일 제외
    "**/*.dev.ts",
    // node_modules는 컴파일 제외 시킴
    // 명시하지 않더라도 자동으로 node_modules 디렉토리는 컴파일이 제외됨
    "node_modules"
  ],
  // 컴파일을 할 대상
  "include": ["some.ts"],
  // 컴파일을 할 파일
  "files": []
}
```





# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

