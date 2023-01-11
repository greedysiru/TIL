# 클린코드 자바스크립트 - 객체 다루기(Computed Property Name)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Computed Property Name

* 객체의 속성을 동적으로 할당할 수 있음
* event handler, Redux, Vuex 등에서 자주 볼 수 있는 패턴



### Event Handler의 예(React)

```React
import React, {useState} from 'react';

function LoginPage() {
  const [state, setState] = useState({
    id: '',
    password: '',
  });
  
  const handleChange = (e) => {
    // 이벤트 객체의 name에 따라 동적으로 state 변경
    setState({
      [e.target.name]: e.target.value,
    })
  }
  
  return <>
  	<input value={state.id} onChange={handleChange} name="name" />
  	<input value={state.password} onChange={handleChange} name="password" />
  </>
}
```



### 메서드 동적 실행

* 객체 안에 정의한 메서드를 동적으로 실행시킬 수 있음

```JavaScript
const catsChat = {
  siru() {
    return '츄르를 먹고 싶다.';
  },
  nunu() {
    return '그것은 나 또한...';
  },
  mango() {
    return '너넨 그만 먹을 필요가 있다.';
  },
  meonji() {
    return '나는 딱히 관심 없다.';
  }
}

// 정의된 메서드들의 key를 배열로 변환
const keysForCatsChat = Object.keys(catsChat);

// 정의된 메서드들을 모두 실행
keysForCatsChat.forEach((key) => console.log(catsChat[key]()));
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

