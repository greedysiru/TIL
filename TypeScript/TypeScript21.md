# TypeScript(2)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. Type Alias

* 타입 별칭
* 타입을 변수처럼 재활용할 수 있음

```TypeScript

const siru: Cat = {
  name: 'siru',
  age: 8,
  isVaccinated: true,
}

const nunu: Cat = {
  name: 'nunu',
  age: 6,
}
```



## 2. readonly

* 객체의 요소를 읽기 전용으로 지정할 수 있음
  * 재할당을 방지
* 배열에 readonly 속성을 부여하면, 배열 원본을 변형시키는 메서드의 호출 방지
  * 원본을 변형하지 않는 map과 같은 메서드는 호출 가능
* 원본 변형을 방지하기 위한 장치

```TypeScript
type Cat = {
  readonly name: string;
  age: string;
  isVaccinated?: boolean;
}


```



## 3. Tuple

* 정해진 길이와 각 요소에 정해진 타입을 가지는 자료형

```typescript
const developer: [string, string] = ['JM', 'JavaScript'];
```



## 4.  unknown

* 변수의 타입을 모를 때 사용
  * ex) API 호출 응답에 대한 타입
* TypeScript가 unknown 타입의 변수가 오류를 일으키지 않도록 방지

```TypeScript
// API 응답
const response: unknown = API();

// response는 unknown이므로 연산을 할 때 Type Guard를 거쳐 오류를 방지하도록 함
// Type Guard가 없으면 Type Checker가 오류 발생 시킴
if (typeof response.age === 'number') {
  	// 이 블록에서는 response.age가 number라는 것이 보장
  	console.log(20 + response.age);
}

```



## 5. void

* 함수가 아무것도 return을 하지 않을 때 사용

```TypeScript
function echo(): void {
  console.log('echo~ echo~');
}
```



## 6. never

* 함수가 절대 return하지 않을 때 발생
  * exception 발생(error)
* 존재하지 않는 타입일 때

# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

