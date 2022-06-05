# 폼

* HTML폼 엘리먼트는 React의 다른 DOM 엘리먼트와 다르게 동작
  * input, textarea, select와 같은 폼 엘리먼트는 사용자의 입력을 기반으로 자신의 state를 관리 및 업데이트
* React에서는 제어 컴포넌트를 사용하여 JavaScript 함수로 사용자가 입력한 데이터에 접근하는 방법이 편리



## 제어 컴포넌트(Cotrolled Component)

* React에 의해 값이 제어되는 입력 폼 엘리먼트
  * React state를 신뢰 가능한 단일 출처로 만들어 폼 엘리먼트와 결합
  * React 컴포넌트는 폼에 발생하는 사용자 입력값을 제어



### input

 ```React
 class signupForm extends React.component {
   costructor(props) {
     super(props);
     this.state = {
       nickname: '',
       password: '',
     };
     
     // 닉네임과 비밀번호 input에 지정할 이벤트 핸들러
     handleChangeInput(event) {
       // name과 value를 구조분해할당으로 가져오기
       const {name, target: {value}} = event;
       // name을 동적으로 key로 지정하여 value를 넣기
       this.setState({[name]: value});
     }
       
     handleSubmit(event) {
       alret('회원가입이 신청되었습니다');
       // 기본 폼 동작을 방지하는 메서드
       event.preventDefault();
     }
 
     render() {
       return (
       	<form onSubmit={this.handleSubmit}>
         	<label>
           	닉네임 :
             <!-- value 어트리뷰트는 this.state.nickname이 되고 항상 화면에 이를 표시, 사용자가 입력하는 값으로 업데이트 됨 -->
             <input 
               name="nickname"
               type="text" 
               value={this.state.nickname} 
               onChange={this.handleChangeInput}
              />
           </label>
           <label>
           	비밀번호 :
             <input
               name="password"
               type="password" 
               value={this.state.password} 
               onChange={this.handleChangeInput}
              />
           </label>
           <input type="submit" value="submit" />
         </form>
       )
     }
   }
 }
 ```



### select

* React에서는 선택된  option 태그에 selected 어트리뷰트를 사용하는 것 대신 select 태그에 value 어트리뷰트를 사용
* select 태그에 multiple 옵션을 허용할 수 있음
  * value 어트리뷰트에 배열을 전달

```react
...
<select value={this.state.value} onChange={this.handleChange}>
	<option value="cat">cat</option>
  <option value="dog">dog</option>
</select>
...
```

# Reference

[React 공식 문서](https://ko.reactjs.org/)

