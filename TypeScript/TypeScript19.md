# 실전으로 배우는 타입스크립트 - 엄격한 타입 적용

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. strict 옵션

* tsconfig의 옵션
* 코드에서 더 강하게 타입을 정의하도록 동작을 점검
* 추후 타입 정의에 대한 오류를 방지
  * 애플리케이션 
* 안전한 코딩을 위해 키는 것을 권장
* true일 경우 아래의 옵션들도 활성화
  * alwaysStrict
  * strictNullChecks
  * strictBindCallApply
  * strictFunctionTypes
  * strictPropertyInitialization
  * noImplicitAny
  * noImplicitThis
  * useUnknownInCatchVariables

### tsconfig.json

* 프로젝트의 타입스크립트 설정에 strict 활성화

```json
{
  "compilerOptions": {
    ...
    "strict": true,
  },
  "include": ["./src/**/*"]
}
```



## 2. null 타입 및 함수 타입 오류 해결

### null 타입 및 함수 타입 오류 예시

```TypeScript
function initEvents() {
  // rankList는 DOM 객체
  // handleListClick의 스펙이 addEventListener가 원하는 함수 스펙과 다름
  rankList.addEventListener('click', handleListClick);
}

async function handleListClick(event: MouseEvent) {
  ...
}
```

위의 코드는 두 개의 오류가 발생

* DOM 객체가 null일 수도 있는 가능성
  *  타입 가드로 해결(if or 삼항연산자)
* No overload matches this call
  * 넘겨받은 함수의 스펙이 호출하는 함수가 원하는 스펙과 달라서 발생
  * strict 옵션으로 인해 strictFunctionTypes 옵션이 켜져서 발생
  * strictFunctionTypes: 콜백 함수의 타입이 일치하는지도 검사
  * 함수의 스펙을 확인하여 해결



### 오류 예시 해결

```TypeScript
function initEvents() {
  // 타입 가드
  // rankList가 null인 경우 함수를 빠져나가도록 함
  if (!rankList) {
    return;
  }
  rankList.addEventListener('click', handleListClick);
}

// addEventListener의 콜백은 Event 타입을 파라미터로 받아야하므로 아래와같이 지정
async function handleListClick(event: Event) {
  ...
}
```



### 오류 예시 해결 2

* null 처리를 삼항 연산자로도 해결할 수 있음

```TypeScript
selectedId = event.target.parentElement
      ? event.target.parentElement.id
      : undefined;
```





## 3. 타입 단언을 이용한 타입 에러 해결

### 타입 단언

* !를 이용하여 해당하는 변수가 null 이 아니라고 타입 단언을 할 수 있음

```TypeScript
deathsList!.appendChild(li);
```



### 타입 단언 주의점

* 타입 단언을 사용하면, 초기값을 정하지 않아도 오류가 발생하지 않음
* null이 아니라는 보장이 없을 때 사용할 경우 오류 발생의 소지가 있음
* 점진적 타입 정의에서 사용을 하되, 위 사항들 주의



## 4. 옵셔널 체이닝 연산자

* 변수가 null이거나 undefined이면 return

```TypeScript
recoveredList?.appendChild(li);

// 위 옵셔널 체이닝 연산을 풀어내면 아래와 같음
if (recoveredList === null || recoveredList === undefined) {
  return ;
} else {
  recoveredList.appendChild(li);
}
```



## 5. DOM 유틸 함수 활용성을 높이는 타입 정의

* 제네릭을 활용하여 더 구체적인 타입을 정의하면서 활용성을 높일 수 있음

```TypeScript
function $<T extends HTMLElement>(selector: string) {
  const element = document.querySelector(selector);
  return element as T;
}
const confirmedTotal = $<HTMLSpanElement>('.confirmed-total');
```





# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)