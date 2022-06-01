# 이벤트 처리하기

* React 엘리먼트에서의 이벤트 처리는 DOM 엘리먼트에서의 이벤트 처리와 상이함
  * 이벤트는 소문자대신 카멜 케이스를 사용
  * JSX를 사용하여, 함수로 이벤트 핸들러를 전달



### HTML vs. React

#### HTML

```HTML
<button onclick="submitInfos()">
  Submit
</button>
```



#### React

```React
<button onClick={submitInfos}>
	Submit
</button>
```



### 기본 동작 방지하기

* 기본 동작을 방지하기 위해서 리액트에서는 preventDefault를 명시적으로 호출

#### HTML

```HTML
<!-- HTML에서는 false를 반환하면 기본 동작이 방지 -->
<button onclick="console.log('clicked!'); return false">
  Submit
</button>
```



#### React

* 이벤트핸들러가 받는 event 객체는 합성 이벤트
  * W3C 명세에 따라 정의 됨

```React
...
function submintInfos(e) {
  e.preventDefault();
  console.log('clicked!');
};

...
return (
  <button onClick="submitInfos">
    Submit
  </button>
);
...
```



### 클래스형 컴포넌트에서의 이벤트 핸들러

* 클래스형 컴포넌트에서의 이벤트 핸들러는 일반적으로 클래스의 메서드를 사용하게 됨
* JSX 안에서 클래스의 메서드를 전달할 때, 메서드 앞의 this는 undefined
  * 그러므로 함수의 프로토타입메서드인 bind로 this를 클래스와 바인딩해야 함
  * 퍼블릭 클래스 필드 문법을 사용 또는 콜백에 화살표 함수를 사용해도 this 문제를 해결 가능



#### function.prototype.bind

```React
class Button extends React.Component {
  constructor(props) {
    super(props);
		// 메서드와 인스턴스를 바인딩
		this.submitInfos = this.submitInfos.bind(this);
  }
  submitInfos() {
    console.log('submit!');
  }

	render() {
		return (
    	<button onClick={this.submitInfos}>
      	Submit
      </button>
    )    
  }

};
```



#### 퍼블릭 클래스 필드 문법

* 아직 실험단계의 문법(ES 제안)

```React
class Button extends React.Component {
  ...
  // 퍼블릭 클래스 필드
  submitInfos = () => {
    console.log('submit!');
  }

	render() {
		return (
    	<button onClick={this.submitInfos}>
      	Submit
      </button>
    )    
  }

};
```



#### 콜백에 화살표 함수 사용

```React
class Button extends React.Component {
	...
  
  submitInfos() {
    console.log('submit!');
  }

	render() {
		return (
      // this가 handleClick 내에서 바인딩
    	<button onClick={() => this.submitInfos()}>
      	Submit
      </button>
    )    
  }

};
```



# Reference

[React 공식 문서](https://ko.reactjs.org/)

