

# GraphQL 클라이언트 만들어보기

**본 내용은 인프런 얄팍한코딩님의 얄팍한 GraphQL과 Apollo 강의를 토대로 작성하였습니다.**



## 1. React와 Apollo Client

* React와 GraphQL 서버와의 연결 방법

### 아폴로 클라이언트 적용

```shell
npm install @apollo/client graphql
```



### ApolloClient 객체 만들기

* client: GraphQL 서버로와 정보를 주고받을 ApolloClient 객체
* uri: GraphQL 서버의 주소
* cache: InMemoryCache를 통한 캐시 관리

```javascript
const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache()
});
```



### React에 적용하기

* root에서 ApolloProvider로 감싸준다.

```react
//   ...
  return (
    <div className="App">
      <ApolloProvider client={client}>
        <header className="App-header">
          <h1>Company Management</h1>
          <nav>
            <ul>
              {NavMenus()}
            </ul>
          </nav>
        </header>
        <main>
          {mainComp[menu]}
        </main>
      </ApolloProvider>
    </div>
  );
//   ...
```



### 쿼리 작성 및 데이터 받아오기

* 컴포넌트에서 데이터베이스로부터 필요한 것들을 적은 쿼리 작성

```javascript
const GET_ROLES = gql`
  query GetRoles {
    roles {
      id
    }
  }
`;
```

* GraphQL에서 받아온 데이터를 렌더링
  * loading: GraphQL 서버에서 정보를 받아오는 동안 표시
  * error: 요청에 오류가 발생할 시 반환
  * data: GraphQL 요청대로 받아진 정보

```JavaScript
// ...
  function AsideItems () {
...
    const { loading, error, data } = useQuery(GET_ROLES);
    if (loading) return <p className="loading">Loading...</p>
    if (error) return <p className="error">Error :(</p>
    return (
      <ul>
        {data.roles.map(({id}) => {
          return (
            <li key={id} className={'roleItem ' +  (contentId === 'id' ? 'on' : '')}
            onClick={() => {setContentId(id)}}>
              <span>{contentId === id ? '🔲' : '⬛'}</span>
              {roleIcons[id]} {id}
            </li>
          )
        })}
      </ul>
    );
  }
// ...
```



## 2. Fragment

* 여러 쿼리에 사용될 수 있는 재사용 가능한 필드 셋
* 중복을 줄임으로써 전체 코드를 간소화



### 재사용되는 요소들 Fragment로 분리

```JavaScript
const Names = gql`
  fragment names on People {
    first_name
    last_name
  }
`
const HealthInfo = gql`
  fragment healthInfo on People {
    sex
    blood_type
  }
`
const WorkInfo = gql`
  fragment workInfo on People {
    serve_years
    role
    team
    from
  }
`
```



### 쿼리 적용

```JavaScript
const GET_PERSON = gql`
  query GetPerson($id: ID!) {
    person(id: $id) {
      id
      ...names
      ...healthInfo
      ...workInfo
      tools {
        __typename
        ... on Software {
          id
        }
        ... on Equipment {
          id
          count
        }
      }
    }
  }
  ${Names}
  ${HealthInfo}
  ${WorkInfo}
`;
```




# Reference

[얄팍한 GraphQL과 Apollo](https://www.inflearn.com/course/얄팍한-graphql-apollo/dashboard)

