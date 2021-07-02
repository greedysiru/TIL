# [프로그래머스] 정수 내림차순으로 배치하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 정수 내림차순으로 배치하기
function solution(n) {
  // n을 문자열화하기
  const nString = String(n);
  // n을 배열에 넣기
  const nArray = [];
  for (let i = 0; i < nString.length; i++) {
    nArray.push(nString[i]);
  }
  // 내림차순 정렬
  nArray.sort((a, b) => b - a);
  return parseInt(nArray.join(''));
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

