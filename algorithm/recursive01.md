# 자료구조와 알고리즘 - 재귀 함수



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. 재귀 함수란?

* 자기 자신을 호출하는 함수
* 재귀 호출(Recursion call)
* 함수 호출은 Call Stack에 쌓이므로, 스택 자료구조와 유사하게 동작
* 함수형 프로그래밍에선 루프 구현을 재귀로 구현
* 무한 루프에 빠지지 않도록 주의



## 2. 자바스크립트에서의 재귀 함수

* 콜 스택에 제한
  * 자바스크립트 엔진마다 제한 수는 다름
  * 크롬의 경우 1만개
* 꼬리 재구(Tail recursion)가 제공되지 않음
* 성능이 좋지 않음



## 3. 재귀로 구현해야 편한 알고리즘

* Union-Find
* DFS
* Backtracking
* 스택을 통해서 구현할 수도 있지만, 코딩테스트에서는 빨리 푸는 것이 중요하므로 추천하지 않음



## 4. 예시 코드

* 반드시 탈출 코드를 넣어야 함

```JavaScript
function recursion(a) {
  console.log(a);
  if (a > 10) {
    retrun a;
  }
  return recursion(a + 1);
}
```



```JavaScript
function fibonacci(x) {
  if (x <= 2){
    return 1;
  }
  
  return fibonacci(x - 1) + fibonacci(x - 2);
}
```







## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

