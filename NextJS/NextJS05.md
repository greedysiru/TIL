# NextJS(5) - Patterns, Head Component

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Patterns

* Layout Pattern
* Layout 컴포넌트란
  * 페이지들의 전반적인 Layout 정의(Navigation 등)
  * global로 import할 것들을 불러옴(Google Analytics, SEO 관련 모듈 등)
  * Global style 적용
* 정의한 Layout component를 App Components에서 불러오기

```React
import NavBar from "../components/NavBar";

export default function Layout({ children }) {
  return (
    <>
      <NavBar />
      <div>{children}</div>
    </>
  );
}
```





## 2. Head Component

* NextJS에서 Head를 관리하기 위한 Component를 제공
  * title, meta description, 작성자 정보 등
* vs. React
  * React의 경우 React helmet과 같은 별도의 라이브러리를 사용해야함
  * 프로젝트 환경에 따라서 충돌, 오류 등이 일어날 수 있어 불안정함
  * NextJS의 경우 프레임워크단에서 많이 사용하는 기능들을 기본적으로 제공해줌(안정적, 편의성)

```React
import Head from "next/head";

export default function Seo({ title }) {
  return (
    <Head>
      <title>{title} | Next Movies</title>
    </Head>
  );
}
---------------------------------------------------
  
import Seo from "../components/Seo";

export default function About() {
  return (
    <div>
      <Seo title="About" />
      <h1>About</h1>
    </div>
  );
}
```




# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

