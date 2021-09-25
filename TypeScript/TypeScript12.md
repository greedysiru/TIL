# 실전으로 배우는 타입스크립트 - 유틸리티 타입

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 유틸리티 타입 소개

* 고급 타입(Advanced Type)
* 제네릭 타입(Generic Type)
* 정의해 놓은 타입을 변환할 때 사용
* 간결한 문법으로 타입 정의
* 중복되는 타입 선언을 줄일 수 있다.
* 상황에 맞는 유틸리티 타입을 직접 정의해서 사용할 수 있음



## 2. Partial

* 특정 타입의 부분 집합을 만족하는 타입을 정의

```TypeScript
interface Pet {
  name: string;
  age: number;
}

type MyPet = Partial<Pet>
const siru: MyPet = {}; // 가능
const nunu: MyPet = { name: 'nunu' }; // 가능
const kami: MyPet = { name: 'kami', age: 3 }; // 가능

// Pet의 Partial은 아래의 인터페이스와 같은 역할을 한다.
interface OptionalPet {
  name?: string;
  age?: number;
}
```



### Partial의 내부 구조

```TypeScript
type Partial<T> = {
    [P in keyof T]?: T[P];
};
```



### Partial 구현하기

```TypeScript
interface UserProfile {
  username: string;
  email: string;
  profilePhotoUrl: string;
}

// 위의 인터페이스의 인덱스에 접근하여 지정된 타입을 재사용
type UserProfileUpdate = {
  username?: UserProfile['username'];
  email?: UserProfile['email'];
  profilePhotoUrl?: UserProfile['profilePhotoUrl'];
}

// 맵드 타입으로 축약
// in으로 모든 속성들을 하나씩 접근
type UserProfileUpdate = {
  [p in 'username' | 'email' | 'profilePhotoUrl']?: UserProfile[p]
}

// keyof로 인터페이스의 key 가져오기
type UserProfileUpdate = {
  // UserProfile의 모든 key가 keyof로 가져와져서 p에 담기게 됨
  // UserProfile의 p(key)로 접근하여 해당 타입을 가져옴
  [p in keyof UserProfile]?: UserProfile[p]
}

// 제네릭으로 축약하면  Partial 구현체와 같은 형태
type Subset<T> = {
  [p in keyof T]?: T[p]
}
```





## 3. Pick

* 기존 타입의 일부를 뽑아내 사용할 수 있음

```TypeScript
interface Product {
  id: number;
  name: string;
  price: number;
  brand: string;
  stock: number;
}

// 상품 목록을 받아오기 위한 API 함수
function fetchProducts(): Promise<Product[]> {
  // ...
}

// 하나의 상품 정보를 보여주는 함수
// Product 인터페이스로부터 일부만 뽑아서 타입 지정
function displayProductDetail(shoppingItem: Pick<Product, 'id' | 'name' | 'price'>) {

}
```



## 4. Omit

* 특정 타입에서 지정된 속성만 제거한 타입을 정의
* Pick의 반대

```TypeScript
interface Pet {
  name: string;
  age: number;
  favorite: string;
}

const siru: Omit<Pet, 'age'> = {
  name: 'siru',
  favorite: 'churu',
}

const nunu: Omit<Pet, 'age'|'favorite'> = {
  name: 'nunu',
}
```





# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)