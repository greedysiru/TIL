# NextJS(3) - Routing, CSS Modules, Styles JSX

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Routing

* NextJS 어플리케이션에서 a태그를 네비게이팅에 사용하면 안 됨
  * a태그로 인한 이동은 전체 어플리케이션이 새로고침 됨
* NextJS에서 앱 내에 네비게이팅에 사용해야만하는 컴포넌트가 있음
  * Link 컴포넌트
* router 관련 proptery, function을 사용하기 위해서는 useRouter Hook을 사용



```React
import Link from "next/link";
import { useRouter } from "next/router";

export default function NavBar() {
  // NextJS에서 제공하는 라우터 훅
  // location에대한 정보
  // path, back, basePath
  const router = useRouter();
  return (
    <nav>
      {/* Link 컴포넌트는 href만을 지정 */}
      <Link href="/">
        {/* 스타일링 또는 선택자 부여는 a태그에 해야 함 */}
        <a style={{ color: router.pathname === "/" ? "red" : "blue" }}>Home</a>
      </Link>
      <Link href="/about">
        <a style={{ color: router.pathname === "/about" ? "red" : "blue" }}>
          about
        </a>
      </Link>
    </nav>
  );
}
```



## 2. CSS Modules

* Next.js에서의 스타일링 방법중 하나
* .module.css 파일을 생성하여 선택자별 스타일링 정의
* 적용시에는 적용할 요소의 className attribute에 모듈에 정의한 클래스를 넣어주기
* 장점
  * 중복 고민없이 class 명을 정의 및 사용
  * 페이지가 빌드 될 때 NextJS가 클래스 이름 뒤에 무작위 문자를 뭍임
* 단점
  * css 모듈 파일 생성 -> 선택자 정의 -> 스타일링 정의 -> 선택자를 필요한 요소에 부여 하는 과정이 김
  * 여러개의 class 선택자를 가지는 요소의 경우 문법이 장황하여 가독성이 떨어짐

```React
...
    <nav>
      {/* Link 컴포넌트는 href만을 지정 */}
      <Link href="/">
        {/* 스타일링 또는 선택자 부여는 a태그에 해야 함 */}
        {/* 두 개 이상의 class 선택자는 리터럴 템플릿 사용 */}
        {/* 또는 배열의 형태에서 join을 사용하여(쉼표) 문자열 전환 */}
        <a
          className={`${styles.link} ${
            router.pathname === "/" ? styles.active : ""
          }`}
        >
          Home
        </a>
      </Link>
      <Link href="/about">
        <a
          className={`${styles.link} ${
            router.pathname === "/about" ? styles.active : ""
          }`}
        >
          about
        </a>
      </Link>
    </nav>
  );
}

```



## 3. Styles JSX

* NextJS에서만 할 수 있는 스타일링 방법
* 컴포넌트에서 받은 props를 사용 가능
* CSS-in-JS
* 서버 렌더링을 지원하지는 않음
  * Web Components와 유사한 Shadow CSS 지원

```React
...
<nav>
      <Link href="/">
        <a className={router.pathname === "/" ? "active" : ""}>Home</a>
      </Link>
      <Link href="/about">
        <a className={router.pathname === "/about" ? "active" : ""}>about</a>
      </Link>
      {/* NextJS에서 복잡한 문자열의 클래스를 만들어 해당 요소에 스타일링 적용 */}
      {/* 정의한 스코프에서만 스타일링이 적용됨 */}
      <style jsx>{`
        nav {
          background-color: tomato;
        }
        a {
          text-decoration: none;
        }
        .active {
          color: blue;
        }
      `}</style>
</nav>
...
```





# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

