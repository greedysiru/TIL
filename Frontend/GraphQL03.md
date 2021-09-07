

# GraphQL 서버 깊이 파보기

**본 내용은 인프런 얄팍한코딩님의 얄팍한 GraphQL과 Apollo 강의를 토대로 작성하였습니다.**



## 1. 서버 구성요소 모듈화

* 다양한 데이터와 기능을 다루기 위해 모듈화



### apollo-server 모듈화

* ApolloServer의 생성자 인자
  * typeDefs: 단일 변수 또는 배열로 지정 가능
  * resolvers: 단일 Object 또는 Merge된 배열로 가능



### 파일 구조

```
.
├── node_modules
├── data-in-csv
│   ├── equipments.csv
│   ├── people.csv
│   ├── roles.csv
│   ├── softwares.csv
│   ├── supplies.csv
│   └── teams.csv
├── database.js
├── dbWorks.js
├── index.js
├── package-lock.json
├── package.json
└── typedefs-resolvers
    ├── _mutations.js
    ├── _queries.js
    ├── equipments.js
    └── supplies.js
```

* data-in-csv: csv 확장자 데이터 파일들이 있는 디렉토리
* typedefs-resolvers: 각 typeDefs와 resolvers가 모듈화된 디렉토리
* index.js: 모듈을 한데 불러와서 AplloServer 생성
* dbWorks.js Resolver에 사용할 기능들 모듈화



## 2. GraphQL의 기본 타입들

### 스칼라 타입

| 타입    | 설명                                                     |
| ------- | -------------------------------------------------------- |
| ID      | 기본적으로는 String이나, **고유 식별자 역할**임을 나타냄 |
| String  | UTF-8 문자열                                             |
| Int     | 부호가 있는 32비트 정수                                  |
| Float   | 부호가 있는 부동소수점 값                                |
| Boolean | 참/거짓                                                  |

```JavaScript
    type EquipmentAdv {
        id: ID!
        used_by: String!
        count: Int!
        use_rate: Float
        is_new: Boolean!
    }
```



### Non Null

* 타입 뒤에 !를 붙여 표현
* null을 반환할 수 없음



### 열거 타입

* 미리 지정된 값들 중에서 반환

```JavaScript
const typeDefs = gql`
    enum Role {
        developer
        designer
        planner
    }
    enum NewOrUsed {
        new
        used
    }
`
```





### 리스트 타입

* 특정 타입의 배열을 반환
* 리스트 타입의 Non Null
  * [String!]: 배열 안에서 null 불가
  * [String]!: 빈 배열 또는 배열이 와야함(null 불가)
  * [String!]!: 빈 배열 또는 배열이 올 수 있고 배열 안에서 null 불가

```JavaScript
const typeDefs = gql`
    type EquipmentAdv {
        id: ID!
        used_by: Role!
        count: Int!
        use_rate: Float
        is_new: Boolean!,
        users: [String!]
    }
`
```



### 객체 타입

* 사용자에 의해 정의된 타입들



## 3. 유니언과 인터페이스

### Union

* 타입 여럿을 한 배열에 반환할 때 사용

```JavaScript
const typeDefs = gql`
	union Given = Equiment | Supply
`
```



### Interface

* 유사한 객체 타입을 만들기 위한 공통 필드 타입
* 추상 타입
  * 다른 타입에 implement 되기 위한 타입

```JavaScript
const typeDefs = gql`
    interface Tool {
        id: ID!
        used_by: Role!
    }
`
...
type Equipment implements Tool {
    id: ID!
    used_by: Role!
    count: Int
    new_or_used: NewOrUsed!
}
...
type Software implements Tool {
    id: ID!
    used_by: Role!
    developed_by: String!
    description: String
}
```

# Reference

[얄팍한 GraphQL과 Apollo](https://www.inflearn.com/course/얄팍한-graphql-apollo/dashboard)

