# Understanding TypeScript(26) - Stop Emitting Files on Compliation Errors, etc options

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Stop Emitting Files on Compliation Errors

* noEmitOnError: 오류가 있으면 컴파일된 결과를 내보내지 않음
  * 기본적으로는 비활성화 되어 있음




## etc compilerOptions

* removeComments: 주석 제거 여부
* noEmit: TypeSCript가 컴파일하고 output을 내지 않음
  * babel과 같이 쓰는 경우, TypeScript는 타입 체커로만 사용
* downlevelIteration: 이터러블을 지원하도록 하는 옵션
  * for...of, spread, distrcturing
  * 컴파일된 용량이 늘어날 수 있음



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

