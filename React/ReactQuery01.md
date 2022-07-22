# React Query(1) - 세팅

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. React Query란?

* Data Fetching을 위한 라이브러리
* 리액트에서 API 호출, 이에 따른 상태 및 로딩 관리를 간단하게 할 수 있게 도와줌
* 불러온 Data의 캐싱 지원



## 2. React Query 세팅

* React Query 사용을 위해 Root에서 Provider로 React Query를 주입하기
* 전역적으로 주입이 되므로 하위 컴포넌트에서 React Query를 사용할 수 있음

```React
import React from "react";
import ReactDOM from "react-dom";
import { QueryClient, QueryClientProvider } from "react-query";
import App from "./App";

const queryClient = new QueryClient();

ReactDOM.render(
      <QueryClientProvider client={queryClient}>
        <App />
      </QueryClientProvider>,
  document.getElementById("root")
);
```

# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

