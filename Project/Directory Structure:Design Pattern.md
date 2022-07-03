

# 디자인패턴

## 0. 서론

최근 6월부터 회사에서 새로운 프로젝트를 담당하게 되었다. 많은 경험을 할 수 있는 기회를 가지게 되어 정말 기뻤고 좋은 결과를 내기 위해서 최선을 다 하고 있는 중이다. 그 고군분투를 틈틈이 정리해서 공유해보고자 한다.



## 1. 기존 소스코드의 문제점

다루고있는 Repository 중에서 메인 앱 소스코드는 마치 역사책과 같다. 여러 사람들을 거쳐오며, 수많은 흔적들이 남아있기 때문이다. 특히나, 디자인패턴은 일관성 없이 3가지가 혼재하고 있다. 이는 개발 생산성을 대단히 낮추고 많은 치명적인 오류들을 일으켰다. 

그래서 새로 구현할 소스코드에는 이러한 메인 앱 소스코드에서 발생했던 문제들을 방지하고 서비스에 걸맞은 디자인패턴을 도입하기로 하였다. 또 추후에는 메인 앱 소스코드에도 적용할 수 있을 것을 목표로 하였다.

이를 위해서, 우선 메인 앱에서의 문제점들을 팀원들과 함께 이야기해보았고 그것들을 반면교사로삼아 정리해보았다.



### a. 여러 디자인패턴 혼재

* 버그, 에러 원인 파악의 어려움
* 유지, 보수의 어려움
* 새로운 기능 추가의 어려움

**→ 디자인 패턴을 명확하게 정의하고 적용**



### b. 난해한 함수명, 변수

* 이름의 형식이 일정하지 않아, 이름만으로 무슨 역할을 하는 변수(또는 함수)인지 파악하기 어려움

**→  코딩 컨벤션을 정의하고 준수하기**



### c. 하드코딩

* 낮은 재사용성
* 중복 코드와 중복 컴포넌트의 발생

**→ 공통 로직 모듈화, Cumstum Hooks 활용, 컴포넌트 정의 후 문서화**



### d. 명령형 프로그래밍

* 로직 파악의 어려움
* 파악을 위해 깊이 들여다봐야하는 코드

**→ 리액트의 패러다임과 잘 맞는 선언형 프로그래밍을 추구, Custom Hooks 적극 사용**



### e. 디렉토리 구조의 복잡함

* 모듈 파일, 컴포넌트, 페이지 등이 정리되어 있지 않고 흩어져 있음

**→ 폴더 구조를 명확하게 정의하여 문서화, 규칙화**



### f. 로컬스토리지 남발

* 여러 상태값을 로컬 스토리지에 저장
* 보안 및 성능상 좋지 않음

**→ 전역 상태 관리 사용 또는 React state로 관리할 수 있도록하기**



### g. 런타임 에러

- 서비스 운영에서 치명적인 오류들이 발생

**→ 런타임 에러를 방지하기 위해 TypeScript를 사용하고 린트 도구(ESLint)로 에러를 야기할만한 문법들을 방지**



### h. 에러핸들링

- 반복적인 try, catch문 사용
- 에러 발생시 별도의 처리가 되어 있지 않아 앱 전체의 셧다운을 야기

**→ 백엔드와 협업하여 에러 규칙 수립, Error Boundary Component 사용**



### i. API 모듈화 미흡

- app 내 사용되는 API 호출 함수들이 두 개의 파일에만 모여있음

**→ 도메인 기준으로 폴더 생성 및 분류 또는 React Query 도입**



### j. props drilling

- props 전달이 3depth, 4depth 이상으로 들어가게 되어 코드 파악이 어려움

**→ props를 절제하는 디자인패턴 사용하고 2depth를 초과하는 props 사용을 금지하기**



## 2. 디자인 패턴

메인 앱의 문제점을 파악하고 해결책을 정리한뒤 디자인 패턴과 개발 방향은 아래와 같이 정하였다.

> **Container-Presentational parttern을 기반으로한 선언형 프로그래밍을 추구**



### a. 도입 이유

- 직관적이고 생산성이 높은 디자인 패턴
  - 기존 프로젝트들에서 두루 사용되었던 방식 → 낮은 러닝커브
- 로직과 UI의 분리
  - 관심사의 분리
- **선언형 프로그래밍** → React Custom Hook 적극 사용
- 로직의 라벨링을 통한 가독성 증대 → 적절한 **추상화**
- 하나의 함수는 하나의 역할을 한다 → **단일 책임 원칙**



### b. Container란?

- Presentational Component를 감싸는 부모
- 비지니스 로직을 담당
  - Presentational Component에게 로직또는 데이터를 props로 전달

```React
const 컨테이너_컴포넌트 = () => {
	const [상태1, 상태1바꾸기] = useState();
	const [상태2, 상태2바꾸기] = useState();

	const 비지니스_로직1 = () => {
		// 비지니스 로직1
	}

	const 비지니스_로직2 = () => {
		// 비지니스 로직2
	}

	return <프레젠테이셔널_컴포넌트 상태1={상태1} 상태2={상태2} 비지니스_로직1={비지니스_로직1} 비지니스_로직2={비지니스 로직2} />
}
```



### c. Presentational이란?

- **UI를 담당합니다.**
- **로직이 없고** 부모로부터 props를 받기만 합니다.

```React
const 프레젠테이셔널_컴포넌트 = (props) => {
	const {상태1,상태2, 비지니스_로직1, 비지니스_로직2} = props;
	
	return (
		<>
			<title>{상태1}</title>
			<span>{상태2}</span>
			<input onChange={비지니스_로직1} />
			<button onSubmint={비지니스_로직2} />
		</>
	);
}
```



### d. 선언형 프로그래밍

- 목표를 명시하고 알고리즘을 명시하지 않음
  - cf) 명령형 프로그래밍 : 알고리즘을 명시하고 목표를 명시하지 않음
- 추상화와 단일책임원칙을 기반으로 함
- 구체적인 문제 해결 방법은 표현에 포함되어 있음

> 오늘 퇴근하고 구파발역 4번출구로 나와, 100m 앞을 전진하여 왼쪽에 있는 서브웨이에 가서 빵은 오트밀 치즈는 아메리칸 치즈에다가 30초 데워서 토핑은 스테이크와 피망 그리고 양파만을 할거고 그리고 소스는 바베큐 소스랑….
>
> vs.
>
> 퇴근 후 할일: 집근처 서브웨이에서 인기 샌드위치 먹기



#### d.1. 추상화

- 잔가지를 걷고 핵심 개념을 뽑아냅니다.
- 함수와 컴포넌트 명을 보고도 역할을 충분히 파악할 수 있을 정도로 추상화

```React
// 낮은 추상화
<button onClick={showConfirm}>
	전송
</button>
{isShowConfirm && (
	<Confirm onClick={() => {showMessage("성공")}} />
)}

----------------------------------------------------
// 적절한 추상화
<ConfirmButton message="성공">
	전송
</ConfirmButton>

----------------------------------------------------
// 높은 추상화
<ConfirmButton />
```



#### d.2 단일 책임 원칙

* 함수 하나는 하나의 역할만을 함

```JavaScript
async function handleOnClick(type) {
	if (type === 'title') {
		await const {title} = apiCall('title');
	}
	if (type === 'content') {
		await const {content} = apiCall('content');
	}
	if (type === 'user') {
		await const {user} = apiCall('user');
	}
}

----------------------------------------------------

async handleOnclickForFetchTitle() {
	await const {title} = apiCall('title');
}

async handleOnclickForFetchContent() {
	await const {content} = apiCall('content');
}

async handleOnclickForFetchUser() {
	await const {user} = apiCall('user');
}
```



## 3. 결론 및 느낀점

사실 Container-Presentational parttern말고 [Compound Component](https://kentcdodds.com/blog/compound-components-with-react-hooks) 디자인 패턴을 도입해보고 싶었었다. 다만, 서비스 런칭일까지 기한과 가용한 인력이 많지 않아서 러닝커브가 있어보이는 해당 패턴을 도입하기에는 어려워보여, 가장 직관적인  **Container-Presentational parttern**을 도입하게 되었다.

취업 전에 항해99에서 여러개의 프로젝트를 만들고 나서는 간만에 프로젝트를 세팅하였는데, 많이 퇴보하였다고 느꼈다. 서비스내에서 발생하는 문제 처리, 유지 및 보수는 늘었어도 무엇인가 만들어 내는 능력은 뒷걸음질 친 것 같아 씁쓸하였다. 그래도, 이번에 이 프로젝트를 맡게되어 발전할 수 있는 기회를 가지게 되었으니 다행인 것같다. 계속 프로젝트를 개발해나가면서 기존 소스코드의 문제점을 해결할 수 있는 라이브러리와 기술들을 공부하고 있다. 위에 언급한 **Custom Hooks, 전역 상태관리, React-Query**는 공부 중으로 관련 사항도 정리하여 팀원들과 공유 및 도입할 예정이다.



## 4. 참고 문헌

매우 유용한 참고 문헌들이니 꼭 보는 것을 권장한다!

* [Container/Presentational Pattern](https://www.patterns.dev/posts/presentational-container-pattern/)
* [React Hooks: Compound Components](https://kentcdodds.com/blog/compound-components-with-react-hooks)
* [변경에 유연한 컴포넌트](https://jbee.io/web/components-should-be-flexible/)
* [토스 | SLASH 21 - 실무에서 바로 쓰는 Frontend Clean Code](https://www.youtube.com/watch?v=edWbHp_k_9Y)

