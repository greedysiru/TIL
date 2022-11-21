# 기초 JS, CS 상식 - 정규표현식



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 정규표현식

* 패턴을 이용하여 원하는 문자를 검색, 대체, 추출할 수 있음
* 성능은 매우 느림



### 1. 형식

```
/ : 시작, 종료기호 사이에 패턴이 들어감
i : 플래그
/regexr/i
```



### 2. 예시

#### 휴대폰 번호

```
1. 010-1234-5678
2. 018-123-4567
3. 01X-XXX(X)-XXXX

\d{3}-\d{3,4}-\d{4}
```



### 이메일에서 중간 문자열만 뽑기

```
greedysiru@gmail.com

.+@(.+)\..+
```



### 3. JavaScript에서의 정규표현식

* RegExp 객체로 정규표현식 기능 제공
* Array, Object처럼 Literal로 생성 가능
* 아래 메서드들과 정규표현식을 활용가능
  * RegExp 메서드
  * String 메서드



### 4. Run-length encoding

* 매우 간단한 비손실 압축 방법
* "AAAABBBDD"
  * 4개의 A, 3개의 B, 2개의 D





## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

