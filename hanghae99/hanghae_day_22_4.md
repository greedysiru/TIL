# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (7) (2021.3.22)



# 1. 리덕스

* 전역 상태관리를 편히 할 수 있게하는 라이브러리
* [공식 문서](https://ko.redux.js.org/introduction/getting-started/)
* 리덕스 패키지 설치

```shell
yarn add redux react-redux
```



## 1.1 리덕스 개념과 용어

* 데이터를 한 군데 몰아넣고 다른 곳에서 꺼내볼 수 있다.

* ActionCreator: 액션 생성 함수, 액션을 만들기 위해 사용



### State

* 리덕스에서 저장하고 있는 상태값
* 딕셔너리 형태 ({[key] : value})의 형태로 보관



### Action

* 상태에 변화가 필요할때(가지고 있는 데이터를 변경할 때) 발생
* 객체
* type은 정한 임의의 문자열 넣기

```react
{type: "CHANGE_STATE", data: {...}}
```



### ActionCreator

* 액션 생성 함수
* 액션을 만들기 위해서 사용

```react
const changeState = (new_data) => {
// 액션을 리턴
	return {
		type: 'CHANGE_STATE',
		data: new_data
	}
}
```



### Reducer

*  리덕스에 저장된 상태(데이터)를 변경하는 함수
* 액션 생성 함수 호출 -> 액션 -> 리듀서가 현재 상테와 액션 객체를 받음 -> 새로운 데이터를 만듦 -> 리턴

```react
// 기본 상태값(임의)
const initialState = {
	name: 'siru'
}

function reducer(state = initialState, action) {
	switch(action.type){

		// action의 타입마다 케이스문을 걸기
		// 액션에 따라서 새로운 값을 리턴
		case CHANGE_STATE: 
			return {name: 'siru1'};

		default: 
			return false;
	}	
}
```



### Store

* 프로젝트에 리덕스를 적용
* 스토어에는 리듀서, 현재 애플리케이션 상태, 리덕스에서 값을 가져오고 액션을 호출하기 위한 몇 가지 내장 함수가 포함



### dispatch

* 스토어의 내장 함수
* 액션을 발생시키는 역할

```react
// 발생시킬 액션을 파라미터로 넘겨서 사용
dispatch(action);
```



## 1.2 리덕스의 3가지 특징

* store는 1개만 사용
* store의 state는 오직 action으로만 변경할 수 있다.
  * 데이터가 마구잡이로 변하지 않도록 불변성 유지
* 리듀서는 순수한 함수여야 한다.
  * 파라미터 외의 값에 의존하지 않는다.
  * 이전 상태는 수정하지 않는다.
  * 파라미터가 같으면 항상 같은 값을 반환
  * 리듀서는 이전 상태와 액션을 파라미터로 받는다.



# 2. 리덕스를 통한 리덕스 상태관리

* 리덕스는 여러 컴포넌트가 동일한 상태를 보고 있을 때 유용
* 데이터를 관리하는 로직을 컴포넌트에서 빼서 컴포넌트는 뷰만 관리할 수 있다.
  * 코드 가독성



## 상태관리 흐름

* 리덕스 Store를 Component에 연결
* Component에서 상태 변화가 필요할 때 Action을 부른다.
* Reducer를 통해서 새로운 상태 값을 만들고
* 새 상태값을 Store에 저장
* Component는 새로운 상태값을 받아온다.



# 3. 리덕스 사용하기

## 3.1 덕스(ducks) 구조

* 보통 리덕스를 사용할 때는 모양대로 action, actionCreator, reducer를 분리해서 작성
* 이와 달리 , 덕스 구조는 모양새로 묶는 대신 기능으로 묶어 작성
  * 한 기능을 하는 action, actionCreator, reucer를 한 파일에 넣는다.
* [덕스 구조 설명 사이트](https://github.com/erikras/ducks-modular-redux)



## 3.2 리덕스 모듈 만들기

* src 폴터 아래에 redux 폴더를 만들고 그 안에 modules 폴더를 생성
* modules 폴더 아래에 리덕스 모듈 파일을 생성한다.

```react
//bucket.js
// action
const LOAD = 'bucket/LOAD';
const CREATE = 'bucket/CREATE';

// initialState 기본 값
const initialState = {
  list: ["영화관 가기", "매일 책읽기", "수영 배우기"],
};

// Action Creator
export const loadBucket = (bucket) => {
    return { type: LOAD, bucket };
}

export const createBucket = (bucket) => {
    return {type: CREATE, bucket};
}

// Reducer
export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    // do reducer stuff
    // load할 때는 가진 기본 값을 그대로
    case "bucket/LOAD":
      return state;
    // create할 때는 새로 받아온 값을 가지고 있던 값에 더해서 리턴
    case "bucket/CREATE":
      const new_bucket_list = [...state.list, action.bucket];
      return { list: new_bucket_list };

    default:
      return state;
  }
}

```



## 3.3 Store

* redux 폴더 하위에 configStore.js 파일을 만든다.

```react
//configStore.js
import { createStore, combineReducers } from "redux";
import bucket from './modules/bucket';
import { createBrowserHistory } from "history";

// 브라우저 히스토리를 만들기
export const history = createBrowserHistory();
// root 리듀서
// 리듀서를 여러개 만들게 되면 여기에 하나씩 추가
const rootReducer = combineReducers({ bucket });

// 스토어를 만들기
const store = createStore(rootReducer);

export default store;
```



# 4. 리덕스 연결하기

## 4.1 Store 연결

```react
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import {BrowserRouter} from 'react-router-dom';

// 리덕스를 주입해줄 프로바이더를 불러오기
import { Provider } from "react-redux";
// 연결할 스토어
import store from "./redux/configStore";
ReactDOM.render(
  // 가장 맨 위에 감싸기
  <Provider store={store}>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </Provider>,
  document.getElementById("root")
);
```



## 4.2 컴포넌트에서 리덕스 데이터 사용하기

* App 컴포넌트에 붙은 state를 리덕스로 교체

### 클래스형 컴포넌트에서 리덕스 데이터 사용하기

* 리덕스 모듈과 connect 함수를 불러오기
* 상태값을 가져오는 함수와 액션 생성 함수를 부르는 함수를 만들어준다.
* connect로 컴포넌트와 스토어를 엮기
* 콘솔에 this.props를 찍어보기 (스토어에 있는 값 확인)
* this.state의 list를 지우고 스토어의 값으로 교체
* setState를 this.props.create로 바꾸기



#### 적용 예시

```react
import React from "react";

import { withRouter } from "react-router";
import { Route, Switch } from "react-router-dom";

// import [컴포넌트 명] from [컴포넌트가 있는 파일경로];
import BucketList from "./BucketList";
import styled from "styled-components";
import Detail from "./Detail";
import NotFound from "./NotFound";

// 리덕스 스토어와 연결하기 위해 connect라는 친구를 호출
import {connect} from 'react-redux';
// 리덕스 모듈에서 (bucket 모듈에서) 액션 생성 함수 호출
import {loadBucket, createBucket} from './redux/modules/bucket';

// 스토어가 가진 상태값을 props로 받아오기 위한 함수
const mapStateTopProps = (state) => ({
  bucket_list: state.bucket.list,
});

// 값을 변화시키기 위한 액션 생성 함수를 props로 받아오기 위한 함수
const mapDispatchToProps = (dispatch) => ({
  load: () => {
    dispatch(loadBucket());
  },
  create: (new_item) => {
    dispatch(createBucket(new_item));
  }
});

// 클래스형 컴포넌트는
class App extends React.Component {
  constructor(props) {
    super(props);
    // App 컴포넌트의 state를 정의
    this.state = {
     
    };
    // ref
    this.text = React.createRef();
  }

  componentDidMount() {
    console.log(this.props);
  }

  addBucketList = () => {
    const new_item = this.text.current.value;
    this.props.create(new_item);
  };

  // 랜더 함수 안에 리액트 엘리먼트 넣기
  render() {
    return (
      <div className="App">
        <Container>
          <Title>내 버킷리스트</Title>
          <Line />
          <Switch>
            <Route
              path="/"
              exact
              render={(props) => (
                <BucketList
                  list={this.props.bucket_list}
                  history={this.props.history}
                />
              )}
            />
            <Route path="/detail" component={Detail} />
            <Route
              render={(props) => <NotFound history={this.props.history} />}
            />
          </Switch>
        </Container>
        {/* 인풋박스와 추가하기 버튼 */}
        <Input>
          <input type="text" ref={this.text} />
          <button onClick={this.addBucketList}>추가하기</button>
        </Input>
      </div>
    );
  }
}

const Input = styled.div`
  max-width: 350px;
  min-height: 10vh;
  background-color: #fff;
  padding: 16px;
  margin: 20px auto;
  border-radius: 5px;
  border: 1px solid #ddd;
`;

const Container = styled.div`
  max-width: 350px;
  min-height: 60vh;
  background-color: #fff;
  padding: 16px;
  margin: 20px auto;
  border-radius: 5px;
  border: 1px solid #ddd;
`;

const Title = styled.h1`
  color: slateblue;
  text-align: center;
`;

const Line = styled.hr`
  margin: 16px 0px;
  border: 1px dotted #ddd;
`;
// withRouter 적용
// connect로 묶기
export default connect(mapStateTopProps, mapDispatchToProps)(withRouter(App));
```



### 함수형 컴포넌트에서 리덕스 데이터 사용하기

* useSelector() 적용하기

#### 적용 예시

```react

import React from "react";
import styled from "styled-components";

// redux hook
import {useDispatch, useSelector} from 'react-redux';

const BucketList = (props) => {
  // 버킷리스트를 리덕스 훅으로 가져오기
  const bucket_list = useSelector(state => state.bucket.list);

  console.log(bucket_list);
  
  return (
    <ListStyle>
      {bucket_list.map((list, index) => {
        return (
          <ItemStyle
            className="list_item"
            key={index}
            onClick={() => {
              props.history.push("/detail");
            }}
          >
            {list}
          </ItemStyle>
        );
      })}
    </ListStyle>
  );
};

const ListStyle = styled.div`
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
`;

const ItemStyle = styled.div`
  padding: 16px;
  margin: 8px;
  background-color: aliceblue;
`;

export default BucketList;
```



# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

[리덕스 공식 문서](https://ko.redux.js.org/introduction/getting-started/)

[덕스 구조 설명 사이트](https://github.com/erikras/ducks-modular-redux)