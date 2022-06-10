# setInterval과 클로져



## 1. React에서 직면한 클로져 이슈

사용자가 검색 조건을 입력하면, API를 호출하여 해당 조건의 결과를 보여주는 용도의 페이지를 작업한 경험이 있다. 이에 더해서, **입력된 검색 조건을 토대로 6초마다 호출하여 결과를 최신화하는 기능도 구현해야 했었다**. 당시에 아래와 같은 코드로 해당 기능을 구현하려고 하였었다.(회사 코드를 가져와 설명할 수는 없으므로 예시로 대체하겠다.)



### 첫번째 시도

* 각 검색 조건을 useState로 다루도록 함
  * 각 검색 조건에 해당하는 UI가 있고 이벤트 핸들러에 의해 set~ 이 호출
* useEffect로 컴포넌트가 마운트된 시점에서 타이머를 세팅
  * 6초단위로 호출되도록 하였음
  * 언마운트 시점에서 타이머를 클리어

```React
// 검색 페이지 컴포넌트
function searchPage = () => {
  // 사용자가 입력한 결과를 담을 state들
  const [searchWord, setSearchWord] = useState('');
  const [startDate, setStartDate] = useState('');
  const [endDate, setEndDate] = useState('');
  // 검색 결과를 담을 객체(state)
  const [searchResult, setSearchResult] = useState({});
  
  // api 호출 함수
  const getSearchResult = async (params) => {
    // api 호출
    const {result} = await api.fetchSearchResult(params);
    // 검색 결과를 담기
    setSearchResult(result);
  };
  
  // 컴포넌트가 렌더링되는 시점에서 타이머 세팅
  useEffect(() => {
    	const searchTimerId = setInterval(() => {
        const params = {searchWord, startDate, endDate};
        getSearchResult(params);
        // 6초단위로 실행
      }, 6000);
    
    	return () => clearInterval(searchTimerId);
  }, []);
  
  // 그외 이벤트 핸들러와 렌더링 관련 코드들
  ...
}
```



위와 같은 코드를 사용하여 검색 기능을 구현할 수 있었고 정상적으로 api를 호출하여 검색 결과를 화면에 출력해내는 것까지 해낼 수 있었다. **하지만, 6초 주기로 검색 결과를 호출해내는 타이머가 의도대로 작동하지 않았다.** 아래와 같은 문제가 발생하였었다.

> 검색 조건 입력 -> 검색 -> 검색 결과 출력 -> 일정시간 경과 -> api가 호출되지 않음

console.log를 사용하여, 해당 원인을 파악해보니 타이머가 실행할 때, **state로 정의한 검색 조건들이 첫 마운트 시점에서의 초깃값으로 유지되는 것이 문제였다.** 즉, setInterval이 생성되었을 시점의 식별자 정보들이 살아있게되는 **클로저**가 원인이었다.



## 2. 클로저

클로저는 이전의 모던 자바스크립트 Deep Dive 책이라는 것에서 공부한 경험이 있었다. 해당 서적에는 아래와 같이 클로저가 설명되어 있었다.

* 함수와 그 함수가 선언된 렉시컬 환경과의 조합(by. MDN)
* **함수의 생명주기가 다했음에도 외부 함수의 식별자를 참조하는 것**
* 캡슐화의 목적으로 주로 사용 됨

**즉, 위 문제는 클로저로 인해 발생한 것이다. setInterval의 콜백 함수가 초기화 된 state 값들을 기억하고 있었기 때문이다. state의 업데이트가 일어나도  콜백함수는 실행된 시점에서의 외부 함수의 식별자(state)를 가지고 있었다.** 

 

## 3. 해결 방법

사실, 이 이슈의 해결 방법은 널리 알려져있다. 구글에 서치해보면 관련한 좋은 블로그 글들과 자료들이 나올 것이다. 대표적인 좋은 자료는 [Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)를 참고하자.

이 글에서 말하는 아이디어는 **setInterval에 전달되는 콜백을 렌더링될 때마다 최신화하자이다.**



### useRef

* useRef는 current 프로퍼티로 전달된 인자로 초기화된 변경 가능한 ref 객체를 반환
* 반환된 객체는 컴포넌트의 전 생애주기동안 유지 됨
  * 매번 렌더링에서 동일한 ref 객체 제공
* current 프로퍼티가 변경되어도 useState와 달리 리렌더링을 발생시키지 않음



useRef의 정의는 위와 같다([React 공식 문서](https://ko.reactjs.org/docs/hooks-reference.html#useref)). useRef는 렌더링에 관계없이 동일한 ref 객체를 제공한다. **그러므로 리렌더링이 되었을 때 current 프로퍼티에 콜백 함수를 전달하여 클로저를 방지할 수 있다. useState는 리렌더링을 일으키고 그 시점에서 생성된 콜백함수는 최신화된 state를 바라보기 때문이다.** 더해서, useRef는 리렌더링을 일으키지 않으므로 무한 렌더링을 방지한다. (이것이 useState를 사용하지 않는 이유다.)



### 해결 코드

```React
// 검색 페이지 컴포넌트
function searchPage = () => {
  // 사용자가 입력한 결과를 담을 state들
  const [searchWord, setSearchWord] = useState('');
  const [startDate, setStartDate] = useState('');
  const [endDate, setEndDate] = useState('');
  // 검색 결과를 담을 객체(state)
  const [searchResult, setSearchResult] = useState({});
  
  const getSearchResult = async (params) => {
    const {result} = await api.fetchSearchResult(params);
    setSearchResult(result);
  };
  
  // 해결 코드
  const useInterval = (callback) => {
    		// 변경 가능한 객체
        const savedCallback = useRef();
				
    		// 새로운 콜백을 넣음
        useEffect(() => {
            savedCallback.current = callback;
        });
        
        useEffect(() => {
          // 새로운 콜백을 실행하는 함수
          function tick() {
            savedCallback.current();
          }
          // 타이머 세팅
          let id = setInterval(tick, 6000);
          return () => clearInterval(id);
        }, []);
  }

// useState에 의해 리렌더링되면, 새로운 콜백이 전달 됨
useInterval(() => {
  getSearchResult();
});
  
  // 그외 이벤트 핸들러와 렌더링 관련 코드들
  ...
}
```



## 4. 느낀점

JavaScript의 클로저는 모던 자바스크립트 Deep Dive라는 서적을 읽으며 공부한 적이 있다. 해당 서적은 JavaScript를 공부하기에는 좋은 책임에는 분명하나 실무에서 React.js를 다루면서 그 책에 나오는 수준의 이슈는 경험하지 못했었다. 그래서 개발 커뮤니티에서 프론트엔드 개발자는 JavaScript에 대해서 빠삭하게 알아야한다는 말이 공감은 되지 않았다. 하지만, 이번에 setInterval과 관련한 클로저 이슈를 경험하면서 그 말이 정말 맞다는 것을 알게 되었다. 클로저를 몰랐어도 해당 이슈는 워낙 유명한 것이라 블로그를 보며 해결을 할 수 있었겠지만, 모른 채로 해결하는 것은 그저 코드를 복사해서 붙여넣는 것에 지나지 않는다. 주니어에서 코드 몽키가 되는 것이 아닌, 생각하며 해결해내는 프론트엔드 개발자가 되기 위해서 꾸준한 JavaScript 공부를 해야겠다고 다시금 다짐하였다.

혹여나, 이 부족한 글을 참고하시거나 읽으신 분들이 있다면 잘못된 부분을 지적해주십사한다. 정말 감사할 것 같다!



## Reference

* **모던 자바스크립트 Deep Dive**
* [Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)
* [React 공식 문서](https://ko.reactjs.org/docs/hooks-reference.html#useref)