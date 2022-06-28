# [프로그래머스] 로또의 최고 순위와 최저 순위 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(lottos, win_nums) {
    const answer = [];
    // 순위를 표현하는 객체
    const rank = {
        6: 1,
        5: 2,
        4: 3,
        3: 4,
        2: 5,
        1: 6,
        0: 6,
    };
    // 0의 갯수
    let countZero = 0;
    // lottos와 win_nums가 일치하는 번호의 수
    let sameNumber = 0;
    // 1. lottos를 하나씩 순회
    for (let lotto of lottos) {
        // 1-1. 0의 갯수는 따로 세기
        if (lotto === 0) {
            countZero += 1;
        }
        // 1-2. win_nums를 순회하며 접근한 lottos 번호와 같은 것이 있는지 세기
        for (let win_num of win_nums) {
            if (lotto === win_num) {
                sameNumber += 1;
            }
        }
    }
    // 2. 최고 순위와 최저 순위를 구하기
    // 2-1. 최고 순위 = lottos와 win_nums가 일치하는 번호의 수 + 0의 갯수
    const highRank = rank[sameNumber + countZero];
    // 2-2. 최저 순위 = lottos와 win_nums가 일치하는 번호의 수
    const lowRank =  rank[sameNumber];
    answer.push(highRank, lowRank);
    return answer;
}
```



## Comment

이중 for문으로 주어진 lottos, win_nums배열을 순회하며 맞춰가면 되는 문제.

filter메서드를 쓰면 더 우아할 것 같다.

## Reference

[프로그래머스](https://programmers.co.kr)

