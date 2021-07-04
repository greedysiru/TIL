# [프로그래머스] 최솟값 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
//  최솟값 만들기
function solution(A, B) {
    let answer = 0;
    // A를 오름차순 정렬
    A.sort((a, b) => a - b);
    // B를 내림차순 정렬
    B.sort((a, b) => b - a);
    // 각 배열의 요소를 하나씩 접근하여 곱하기
    for (let i = 0; i < A.length; i++) {
        answer += A[i] * B[i];
    }

    return answer;
}
```



## Comment

각 두 배열의 요소를 더하는데 최소가 되도록 만들어야 한다. 즉, A배열에서의 최솟값 * B배열에서의 최댓값을 구하면 최소가 되므로, A는 오름차순 정렬을 하고 B는 내림차순 정렬을 한다. 그리고 `for문`으로 각 배열에 접근하여 곱한다.



## Reference

[프로그래머스](https://programmers.co.kr)

