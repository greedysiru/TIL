# [드림코딩 by 엘리] JavaScript 함수

**상세 내용 [블로그](https://greedysiru.tistory.com/597) 참고**



# 1. 함수 선언 & 호출

```JavaScript
// 선언
// 전달받는 파라미터없이 실행되는 함수
function doSomething() {
  console.log('hello');
}
// 호출
doSomthing();
```



# 2. 값을 리턴하는 함수

* 계산 이후에 특정 값을 전달하는 함수
* JavaScript는 parameter에 type을 지정하지 않는 동적 언어이다.

```JavaScript
function add(a, b){
  // 전달받은 a, b를 연선하여 변수에 저장
  const sum = a + b;
  // 더한 결과를 return
  return sum;
}

// 함수가 전달한 값을 result에 저장
// result를 정의함과 동시에 값을 할당 -> 함수 호출 -> 1,2 전달 -> 코드블록 실행(연산) -> 결과 return
const result = add(1, 2);
console.log(result);
```



# 3. 함수를 인자로 전달

```JavaScript
function doSomething(add) {
  console.log(add);
}


function add(a, b){
  const sum = a + b;
  return sum;
}

// 함수 호출
// 함수 자체를 전달하게 되어 함수 자체가 출력된다.
doSomething(add);

// 함수가 바로 호출되어 버림
// doSomething이 호출되기 전에 add가 호출되어 코드블록이 실행
// parameter로 a, b가 전달되지 않았으므로 NaN이 출력된다
doSomthing(add());
```



# 4. 함수를 변수에 할당

```JavaScript
function add(a, b){
  const sum = a + b;
  return sum;
}
// 함수 자체를 변수에 할당
const addFun = add;
addFun(1, 2);
```



# Reference

[JavaScript 함수](https://www.youtube.com/watch?v=PuG2VW18O1E&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=14)