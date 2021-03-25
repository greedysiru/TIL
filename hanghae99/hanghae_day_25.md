# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (10) (2021.3.25)



# 1. 리덕스와 FireStore

* firestore를 리덕스 스토어 넣기 위해서 미들웨어가 필요하다.
* 액션 -> 미들웨어 -> 리듀서 순으로 처리가 된다.



## 1.1 redux-thunk

* 객체 대신 함수를 생성하는 액션 생성 함수를 작성 가능
* 패키지 설치

```shell
yarn add redux-thunk
```



### 미들웨어 추가(configStore.js)

```react
import { createStore, combineReducers, applyMiddleware, compose } from "redux";
import thunk from "redux-thunk";
import bucket from "./modules/bucket";
import { createBrowserHistory } from "history";

export const history = createBrowserHistory();

const middlewares = [thunk];

const enhancer = applyMiddleware(...middlewares);
const rootReducer = combineReducers({ bucket });
const store = createStore(rootReducer, enhancer);

export default store;
```



## 1.2 리덕스에 Firestore 적용

### Firebase와 통신하는 함수 만들기

```react
const bucket_db = firestore.collection("bucket");

// 파이어베이스와 통신
export const loadBucketFB = () => {
  return function (dispatch) {
    
    bucket_db.get().then((docs) => {
      let bucket_data = [];
      docs.forEach((doc) => {
        // 도큐먼트 객체를 확인
        console.log(doc);
        // 도큐먼트 데이터 가져오기
        console.log(doc.data());
        // 도큐먼트 id 가져오기
        console.log(doc.id);

        if(doc.exists){
          bucket_data = [...bucket_data, {id: doc.id, ...doc.data()}];
        }
      });

      console.log(bucket_data);
      // 액션 생성 함수에 가져온 데이터 넣기
      dispatch(loadBucket(bucket_data));
    });
  };
};
```



### 리듀서 고치기

```react
...
case "bucket/LOAD": {
      if(action.bucket.length >0){
        return { list: action.bucket };
      }

      return state;
    }
...
```



### 사용하기

```react
...
// loadBucketFB를 import
// load()를 componentDidMount에서 호출
const mapDispatchToProps = (dispatch) => ({
  load: () => {
    dispatch(loadBucketFB());
  },
  create: (new_item) => {
    dispatch(createBucket(new_item));
  }
});
...
```





# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)