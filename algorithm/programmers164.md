

# [프로그래머스] 등수 매기기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (score) => {
    const rank = {};
    score.map(([math, eng]) => (math + eng) / 2)
        .sort((a, b)=> b - a)
        .forEach((avg, index) => !rank[avg]? rank[avg] = index + 1 : null);
    return score.map(([math, eng]) => rank[(math + eng) / 2]);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

