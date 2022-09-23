# NextJS(8) - Routes, Context Parameter

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Rotues

### 1.1 Dynamic Routes

* NextJS에서는 폴더 단위로 Route를 정의할 수 있음
  * Nested Route
* Dynamic Routes의 경우, 대괄호 안에 parameter를 적어주기
* Catch All Routes
  * 대괄호 안에 세 개의 점을 추가하여 모든 경로를 포착하도록 할 수 있음
  * ex) [...params].js
  * 배열의 형태로 들어오게 됨



#### 예시

```
├── pages
│   └── users
│       ├── [id].js: Dyanamic Route
│       ├── [...params].js: Catch All Routes
│       ├── all.js: /users/all로 접근하면 띄워지는 페이지
│       └── index.js: /users로 접근하면 띄워지는 페이지
...
```



### 1.2 useRouter

* Next에서 제공하는 Route 관련 기능을 사용할 수 있는 Hook
  * route 이동, route state, route masking 등을 사용 가능
* userRouter에서 가능한 기능은 Link에서도 사용 가능

```React
...
export default function Example() {
  const router = useRouter();
  const onClick = (id, title) => {
    router.push(
      {
        // 이동시킬 url
        pathname: `/users/${id}`,
        // Query String(state)
        query: {
          title: '사용자 정보',
        },
      },
      // masking
      `/users/${id}`
    );
  };
  return (
    <div
      onClick={() => onClick(users.id)}
      >
      // ...
    </div>
  );
}

```



## 2. Context Parameter

* getServerSideProps 함수에서 전달받게 되는 Parameter
* Dynamic Route를 사용하는 경우 params에 router parmeter가 포함 됨

### 예시

```React

export default function Example({ params }) {
  const [param1, param2] = params;
  ...
  );
}

export function getServerSideProps({ params: { params } }) {
  return {
    props: {
      params,
    },
  };
}

```




# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

