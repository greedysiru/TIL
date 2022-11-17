# 기초 JS, CS 상식 - 이벤트 루프



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. JavaScript

* JavaScript는 Sigle Thread 언어
* JavaScript Engine의 Call Stack은 하나만 존재



## 2. Event Loop

* 비동기적으로 데이터를 불러오고 애니메이션을 실행시킬 수 있는 이유
* JavaScript Engine에 포함되어 있지는 않음
* 브라우저 또는 Node.js에서 자체적으로 관리
* Event Loop로 인해 브라우저는 Multi Thread로 동작하게 됨
* Web APIs에 의해 생성된 콜백 함수를 태스크 큐에서 빼와 콜스택에 넣는 역할을 함



### Web APIs

* 브라우저에서 제공하는 API
* DOM API, Timer, AJAX 실행은 브라우저에 위임
* 보통 Web APIs에 Call Back을 넘기게 됨
* Call Back들은 비동기 작업이 끝나면, Task Queue에 넣어져 순차적으로 꺼내 Call Stack에 push



### 동작 방식

1. 전역 스코프에서 script 실행
2. 코드가 순차적으로 실행
3. Web API를 만나면, 콜스택에 쌓임
4. 이와 동시에 브라우저 내부적으로 Web API가 실행
5. Web API는 바로 종료
6. Web API 이후, 다음 함수를 만나면 콜스택에 쌓임
7. 해당 함수 정의부의 로직 실행
8. 함수 로직 실행 완료 후, 해당 함수는 콜스택에서 빠져 나옴
9. 콜스택이 비면 비동기 콜백을 태스크 큐로부터 콜스택에 쌓음(틱)
10. 콜백 함수 실행



## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)