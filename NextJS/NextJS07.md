# NextJS(7) - Server Side Rendering

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Server Side Rendering

* 해당 페이지가 SSR만 할 지 선택 가능
* page가 열렸을 때 data fetching까지 완료하고 보여줄 수 있음
  * 유저는 흰 화면 -> 완전히 렌더링된 페이지를 보게 됨
* SEO 최적화에 유리



## 2. getServerSideProps

* server에서 해당 함수를 실행하고 return하는 객체를 props로 page에 전달할 수 있음
  * server(web backend)에서 실행하게 됨
* 고정된 이름을 사용해야함
* getServerSideProps 함수를 실행하고 App Components의 pageProps로 해당 컴포넌트에 전달 됨



### 예시

```JavaScript
export default function Example({ results }) {
  return (
    <div>
      {results?.map((data) => (
        ...
      ))}
    </div>
  );
}
...
export async function getServerSideProps() {
  const { results } = await (
    await fetch(`http://localhost:3000/example`)
  ).json();
  // props로써 page에 전달
  return {
    props: {
      results,
    },
  };
}
```




# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

