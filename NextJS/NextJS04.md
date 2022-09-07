# NextJS(4) - Global Style, App Components

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Global Style

* Style Jsx를 Global하게 적용 가능
  * App Components에서 사용해야 모든 페이지에서 적용됨
  * NextJS의 각 페이지는 독립적이기 때문


```react
<style jsx global>
        {`
          a {
            color: white;
          }
        `}
</style>
```





## 2. App Components

* 어떤 컴포넌트의 청사진(템플릿)
* 프레임워크 내에 포함된 기능
* 렌더링 되기 전에 먼저 보는 컴포넌트
  * _app.js 형식의 네이밍
* NextJS에서는 Global.css를 import할 수 없음
  * 반드시 module이어야 함
  * App Components에서는 Global.css를 import할 수 있음
* Styles JSX Global 또한 적용 가능

```react
// NextJS는 페이지를 렌더링하기 전 자동적로 이 컴포넌트를 불러옴
import NavBar from "../components/NavBar";
import "../styles/globals.css";

// Component, pageProps: NextJS에서 App Components로 전달하는 객체에 포함된 Properties
export default function CustomApp({ Component, pageProps }) {
  // Component는 렌더링할 컴포넌트를 받아옴
  return (
    <div>
      <NavBar />
      <Component {...pageProps} />
      {/* 모든 페이지에 똑같은 문구를 노출 시킬 수 있음 */}
      <span>This is custom app</span>
      <style jsx global>
        {`
          a {
            color: white;
          }
        `}
      </style>
    </div>
  );
}

```



# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

