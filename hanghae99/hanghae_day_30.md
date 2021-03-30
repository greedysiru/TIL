# [항해99 1기] [Chapter3-2] 주특기 심화 - 리액트 심화반 (5) (2021.3.30)



# 리덕스

## 1. 설치하기

* 리덕스, 리덕스 모듈 내에서 경로 이동을 할 수 있는 히스토리 ,라우터와 히스토리를 역어줄 모듈

```Shell
yarn add redux react-redux redux-thunk redux-logger history@4.10.1 connected-react-router@6.8.0
```

* 불변성 관리를 용이하게 할 수 있는 패키지

```shell
yarn add immer redux-actions
```



## 2. 모듈 만들기

* 예시코드

```React
// 패키지 임포트
import { createAction, handleActions } from "redux-actions";
import { produce } from "immer";

// Action
const LOG_IN = "LOG_IN";
const LOG_OUT = "LOG_OUT";
const GET_USER = "GET_USER";

// Action Creators
const logIn = createAction(LOG_IN, (user) => ({ user }));
const logOut = createAction(LOG_OUT, (user) => ({ user }));
const getUser = createAction(GET_USER, (user) => ({ user }));

// Initial state
const initialState = {
  user: null,
  is_login: false,
};

// Reducer
export default handleActions(
  {
    [LOG_IN]: (state, action) =>
    // 불변성 관리
      produce(state, (draft) => {
        setCookie("is_login", "success");
        draft.user = action.payload.user;
				draft.is_login = true;
      }),
		[LOG_OUT]: (state, action) =>
      produce(state, (draft) => {
        deleteCookie("is_login");
        draft.user = null;
				draft.is_login = false;
      }),
    [GET_USER]: (state, action) => produce(state, (draft) => {}),
  },
  initialState
);

// export
const actionCreators = {
  logIn,
  getUser,
  logOut,
};

export { actionCreators };
```



## 3. 스토어 만들기

```React
// 패키지 및 필요한 컴포넌트 임포트
import { createStore, combineReducers, applyMiddleware, compose } from "redux";
import thunk from "redux-thunk";
import { createBrowserHistory } from "history";
import { connectRouter } from "connected-react-router";

import User from "./modules/user";

// 히스토리 사용
export const history = createBrowserHistory();

// rootreducer
const rootReducer = combineReducers({
  user: User,
  router: connectRouter(history),
});

// 미들웨어
const middlewares = [thunk.withExtraArgument({history: history})];

// 현재의 환경을 알려준다
const env = process.env.NODE_ENV;

// 개발환경에서는 로거를 사용
if (env === "development") {
  const { logger } = require("redux-logger");
  middlewares.push(logger);
}

// redux devTools
const composeEnhancers =
  typeof window === "object" && window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
    ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({
        // Specify extension’s options like name, actionsBlacklist, actionsCreators, serialize...
      })
    : compose;

// 미들웨어 묶기
const enhancer = composeEnhancers(
  applyMiddleware(...middlewares)
);
// 스토어 생성
let store = (initialStore) => createStore(rootReducer, enhancer);

export default store();
```



## 4. 스토어 주입하기

* index.js에 스토어 주입

```React
...
import store from "./redux/configureStore";
import { Provider } from "react-redux";

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
...
```

* App.js

```React
...
import { ConnectedRouter } from "connected-react-router";
import { history } from "../redux/configureStore";
...
function App() {
  return (
    <React.Fragment>
      <Grid>
        <Header></Header>
        <ConnectedRouter history={history}>
          <Route path="/" exact component={PostList} />
          <Route path="/login" exact component={Login} />
          <Route path="/signup" exact component={Signup}/>
        </ConnectedRouter>
      </Grid>
    </React.Fragment>
  );
}
...
```



# Reference

[스파르타코딩클럽 리액트 심화반](https://spartacodingclub.kr/online/react/plus)

