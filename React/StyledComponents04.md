# Styled Components(4)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## Themes & TypeScript

* styled-components 모듈에 theme에 대한 타입을 추가
  * 자동완성 기능
  * 일관적인 테마 정의



### styled.d.ts 정의하기

* d.ts 파일 : 선언 파일
* styled-components의 Definitely Typed 에서 비어있는 DefaultTheme 인터페이스를 정의하기

```TypeScript
import 'styled-components';

// styled Components 테마 정의 확장
declare module 'styled-components' {
  export interface DefaultTheme {
    backgorundColor: string;
    textColor: string;
  }
}
```





# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

