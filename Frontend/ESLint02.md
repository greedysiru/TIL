# ESLint & Prettier - 자동화



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## VSCode Extention

### ESLInt Extention

* 작성중인 코드를 실시간으로 ESLint 규칙에 위배되지 않는지 검사한다.
* 설정 -> 작업영역에서 프로젝트별로 에디터를 세팅
  * 저장할 때마다 ESLint를 실행하여 코드를 자동으로 검사 후 수정한다.

```json
settings.json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.esLint": true
  }
}
```

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)