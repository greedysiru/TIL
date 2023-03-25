

# [프로그래머스] 크기가 작은 부분 문자열 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (t, p) => {
    let answer = 0;
    // p의 길이
    const pLength = p.length;
    // p의 길이와 같고 p보다 작은 t의 부분 문자열 탐색
    let start = 0;
    for (let i = pLength; i <= t.length; i ++) {
        // 부분 문자열
        const partString = t.slice(start, i);
        // 부분 문자열이 p이하면 answer count
        partString <= p && (answer += 1);
        // start 더하기
        start += 1;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

