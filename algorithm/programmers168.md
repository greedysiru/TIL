

# [프로그래머스] 덧칠하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (n, m, section) => {
    let paintCount = 0;
    // 페인트칠이 끝날 지점
    let endPoint = 0
    section.forEach((s) => {
        // 현재 접근한 영역이 endPoint보다 크면
        if (s > endPoint) {
            // patinCount를 더하고
            paintCount += 1;
            // endPoint를 이동
            endPoint = s + m - 1;
        }
    });
    return paintCount;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

