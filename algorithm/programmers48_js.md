# [프로그래머스] 최소 직사각형 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```javascript
function solution(sizes) {
    let answer = 0;
    // 지갑의 가로 길이
    let width = 0;
    // 지갑의 세로 길이
    let height = 0;
    // 주어진 sizes 배열을 하나씩 접근
    for (let size of sizes) {
        // 가로와 세로 중 더 긴 것을 담은 변수
        const numA = size[0] < size[1] ? size[1] : size[0];
        // 가로와 세로 중 더 짧은 것을 담은 변수
        const numB = size[0] < size[1] ? size[0] : size[1];
        // 지갑의 가로와 세로를 최신화
        width = width < numA ? numA : width;
        height = height < numB ? numB : height;
    }
    // 지갑의 크기
    answer = width * height;
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

