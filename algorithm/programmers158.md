# [프로그래머스] 옹알이(1) - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (babbling) => babbling.map((bab) => bab.replaceAll('aya', 'O').replaceAll('ye', 'O').replaceAll('woo', 'O').replaceAll('ma', 'O')).map(bab => bab.replaceAll('O', '')).filter(bab => bab === '').length;
```



## Reference

[프로그래머스](https://programmers.co.kr)

