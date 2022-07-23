# React Query(2) - 사용 예시, Query Key, TypeScript 적용

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. React Query 사용 예시

### useQuery

* Data를 Fetching할 때 사용하는 React Query Hook

* 파라미터는 대표적으로 세 가지

  1. queryKey: query의 고유 식별자

  2. Fetcher Function: API를 호출하여 Data를 받아오는 함수, Promise를 return해야 함
  3. options: 쿼리에 대한 옵션. refetchInterval과 같은 것을 설정 가능

* return하는 값은 대표적으로 두 가지

  * isLoading: 로딩 상태를 나타내는 Boolean
  * data: Fetching에 성공해서 받아온 data

* **useQuery를 사용하면, 기존에 API를 불러오고 상태를 최신화하고 로딩 상태를 구현하기 위한 코드들과 Hook을 대체할 수 있음**

* 캐싱을 하여 API 호출을 방지

* refetchInterval를 사용하여 주기적으로 API 호출 가능

  * State를 업데이트하고 UI를 새로고침

```React
import { useQuery } from 'react-query';

function mainPage() {
  // Fetcher Function 정의부
  const fetchingData = () => {
    // Promise를 return
  	return fetch("...api").then(response => response.json());
  };
  
  const { isLoading, data } = useQuery("fetchData", fetchingData, {
    // 이 쿼리를 5초마다 실행
    refetchInterval: 5000,
  });
  
  return (<>
          	<h1>mainPage</h1>
          	// 로딩이 완료되었을 때 렌더링
          	{!isLoading && (
         			<span>{data}</span>
         		)}
          </>)
};
```



## 2. Query Key

* Query에 대해 식별하기 위한 key, array로 되어있음
* 모든 Query는 각각 유일한 key를 가져야 함
* useQuey의 첫번째 인자에서 지정할 수 있음
  * string or array

```React
  const { isLoading, data } = useQuery(["productInfo" , productId], fetchingData);
  const { isLoading, data } = useQuery(["buyInfo" , productId], fetchingData);
```



## 3. TypeScript와 함께 사용하기

* useQuery Hook을 사용할 때, data로 들어올 인터페이스를 제네릭으로 전달

```React
interface IData {
  name: string;
  age: number;
  paidGoods: string[];
}

const { isLoading, data } = useQuery<IData>("fetchData", fetchingData);
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

