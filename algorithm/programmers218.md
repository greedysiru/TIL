

# [프로그래머스] 문자열 바꿔서 찾기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (myString, pat) => myString.includes(pat.split('').map(p => p === 'A'? 'B' : 'A').join(''))? 1 : 0;
```

주어진 `pat`를 배열로 바꾸고 하나씩 순회하며 문자열을 바꿔준다. `pat` 은 다행히도 A 또는 B로 이루어진 문자열이라 삼항연산자로 충분히 대체 로직을 짤 수 있었다.



## Reference

[프로그래머스](https://programmers.co.kr)

