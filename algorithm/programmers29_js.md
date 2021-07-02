# [프로그래머스] 제일 작은 수 제거하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 제일 작은 수 제거하기
function solution(arr) {
  const arrMin = Math.min(...arr);
  console.log(arrMin)
  const arrFiltered = arr.filter((value) => value !== arrMin);
  if (arrFiltered.length > 1) {
    return arrFiltered;
  } else {
    return [-1];
  }
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

