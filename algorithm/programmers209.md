

# [프로그래머스] 명예의 전당(1)

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (k, score) => {
    // 명예의 전당
    const hallOfName = [];
    // 1. 주어진 score 순회하여 lowest 만들기
    const lowest = score.map((score) => {
        // 2. 현재 명예의 전당에 k명 미만인지 확인
        if (hallOfName.length < k) {
             // 2-1. 미만이라면, 명예의 전당에 score 넣기
             hallOfName.push(score);
        } else {
            // 2-2. 이상이라면, k번째 가수보다 현재 score가 높으면 score를 k번째 가수 대신 넣기
            if (hallOfName[k - 1] < score) hallOfName[k - 1] = score;
        }
        // 3. 내림차순 정렬
        hallOfName.sort((a, b) => b - a);
        // 4. 해당 일에 발표된 명예의 전당 최하위 점수
        return hallOfName[hallOfName.length - 1]? hallOfName[hallOfName.length - 1] : 0;
    });
    return lowest;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

