# Understanding TypeScript(22) - Setting a Compilation Target

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Setting a Compilation Target

### tsconfig.json

* compilerOptions: 어떻게 컴파일 될 지에 대한 옵션
* target: 어떤 JavaScript 버전으로 컴파일 할 지에 대한 옵션
  * es3, es5, es6 등으로 컴파일 시킬 수 있음
  * 오래된 브라우저를 고려하여 옵션을 설정
  * const, let 같은 문법의 경우 es5 옵션이라면 var로 대체 됨

```Json
{
  // 어떻게 컴파일 될지에 대한 옵션
  "compilerOptions": {
    "target": "es5" 
    ...
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

