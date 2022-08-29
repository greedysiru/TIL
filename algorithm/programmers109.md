# [프로그래머스]  땅따먹기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(land) {
    return Math.max(...land.reduce((acc, row) => {
        return [
            row[0] + Math.max(acc[1], acc[2], acc[3]),
            row[1] + Math.max(acc[0], acc[2], acc[3]),
            row[2] + Math.max(acc[0], acc[1], acc[3]),
            row[3] + Math.max(acc[0], acc[1], acc[2])
        ]
    }, [0, 0, 0, 0]));
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

