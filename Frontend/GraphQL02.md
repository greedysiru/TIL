

# GraphQL 서버 만들어보기

**본 내용은 인프런 얄팍한코딩님의 얄팍한 GraphQL과 Apollo 강의를 토대로 작성하였습니다.**



## 1. Apollo 서버 구축하기

### 데이터베이스 모듈 삽입

* csv: 몇가지 필드를 쉼표로 구분한 텍스트 데이터
  * VSC Edit csv 확장으로 편하게 볼 수 있음
* 목 데이터베이스(csv)를 require로 불러올 수 있다.

```javascript
const database = require('./database');
```



### Apollo 서버 설치

### 필요 모듈 설치

```shell
npm i graphql apollo-server
```



### Apollo 서버 생성 및 실행

* ApolloServer
  * typeDef와 resolver를 인자로 받아 서버 생성
* typeDef
  * GraphQL 명세에서 사용될 데이터, 요청의 타입 지정
  * gql(template literal tag)로 생성됨
* resolver
  * 서비스의 액션들을 함수로 지정
  * 요청에 따라 데이터를 반환, 입력, 수정, 삭제
* 서버가 실행되면 GraphQL Playground에서 작성한 GraphQL type, resolver 명세 확인 가능
  * 데이터 요청 및 전송 테스트

```JavaScript
const database = require('./database')
// apollo-server 모듈 불러오기
const { ApolloServer, gql } = require('apollo-server')
// GraphQL 명세에서 사용될 데이터, 요청의 타입 지정
const typeDefs = gql`
  type Query {
    teams: [Team]
  }
  type Team {
    id: Int
    manager: String
    office: String
    extension_number: String
    mascot: String
    cleaning_duty: String
    project: String
  }
`
// 서비스의 액션들을 함수로 지정
const resolvers = {
  Query: {
    teams: () => database.teams
  }
}
// typeDefs, resolvers 두 인자를 받아서 ApolloServer 인스턴스를 생성
const server = new ApolloServer({ typeDefs, resolvers })
server.listen().then(({ url }) => {
console.log(`🚀  Server ready at ${url}`)
})
```



## 2. Query 구현하기

* Query: 데이터를 요청하는 것

### Query 루트 타입

* 자료요청에 사용될 쿼리들을 정의
* 쿼리 명령문마다 반환될 데이터 형태를 지정

```typescript
type Query {
	teams: [Team]
}
```



### 반환 데이터 타입

* 반환될 데이터의 형태를 지정
* 자료형을 가진 필드들로 구성

```typescript
type Team {
	id: Int
	manager: String
	project: String
}
```



### Resolver

* 데이터를 반환하는 함수 선언

```JavaScript
const resolvers = {
  Query: {
    teams: () => database.teams
  }
}
```



### 특정 데이터만 받아오기

* args로 주어진 id에 해당하는 team만 필터링
  * 해당 아이디의 team을 하나만 가져오기

```JavaScript
// resolver
Query: {
  ...
  team: (parent, args, context, info) => database.teams
  	.filter((team) => {
    	return team.id === args.id
  })[0]
}
```

* 쿼리 루트 타입 선언

```typescript
type Query {
	...
	team(id: Int): Team
}
```



### 데이터 연결해서 받아오기

* Underfetching 문제 해결
  * 여러 계층의 데이터를 한 번에 받아올 수 있음

```T
// resolver
Query: {
	...
	teams: () => database.teams
		.map((team) => {
			team.supplies = database.supllies
				.filter((supply) => {
					return supply.team === team.id
				})
				return team
		}),
}
```



## 3. Mutation 구현하기

* 데이터에 추가, 수정, 삭제를 가하는 것
* 개발자들간에 합의된 명세
* Query와 Mutation의 추가, 수정, 삭제는 typeDefs와 resolver를 사용하는 것은 같으나 Mutation은 데이터를 직접 조작하는 것에서 차이



### 데이터 삭제하기

* 삭제 루트 타입

```typescript
type Mutation {
    deleteEquipment(id: String): Equipment
}
```

* 삭제 resolver

```javascript
Mutation: {
      deleteEquipment: (parent, args, context, info) => {
          const deleted = database.equipments
              .filter((equipment) => {
                  return equipment.id === args.id
              })[0]
          database.equipments = database.equipments
              .filter((equipment) => {
                  return equipment.id !== args.id
              })
          return deleted
      }
}
```





# Reference

[얄팍한 GraphQL과 Apollo](https://www.inflearn.com/course/얄팍한-graphql-apollo/dashboard)