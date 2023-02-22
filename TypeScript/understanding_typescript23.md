# Understanding TypeScript(23) - Understanding TypeScript Core Libs

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Understanding TypeScript Core Libs

### lib

* TypeScript가 아는 기능 또는 객체를 설정
  * TypeScript가 알고 있어야 객체 또는 기능에 접근해도 Error를 발생시키지 않음
* 대표적으로
  * dom
  * ES6
  * DOM.Iterable
  * ScriptHost
  * 위 옵션들은 default로, 명시하지 않아도 기본으로 TypeScript가 알고 있음

```TypeScript
{
  // 어떻게 컴파일 될지에 대한 옵션
  "compilerOptions": {
    // default
    "lib": [
      // DOM APIs
      "dom",
      "ES6",
      "DOM.Iterable",
      "ScriptHost"
    ],
  	...
  }
}
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

