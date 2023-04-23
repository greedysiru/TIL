

# [프로그래머스] 조건에 맞게 수열 변환하기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (arr, k) => k % 2 === 0? arr.map(i => i + k) : arr.map(i => k * i);
```

삼항 연산자로 짝수, 홀수인 경우를 판별하여 각각 조건에 맞는 연산을 한다.



## Reference

[프로그래머스](https://programmers.co.kr)

