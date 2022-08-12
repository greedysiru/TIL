# [프로그래머스] 피로도 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript

function solution(k, dungeons) {
    let answer = 0;
    // 각 던전을 체크하는 배열
    const checkedArray = new Array(dungeons.length).fill(false);
    
     // 깊이 우선 탐색 함수 선언
function DFS(k, dungeons, count, checkedArray) {
    // 모든 경우의 수를 순회
    for (let i = 0; i < dungeons.length; i++) {
        // 방문하지 않았고 현재 피로도 k로 접근 가능한 곳을 접근
        if (!checkedArray[i] && k >= dungeons[i][0]) {
            // 방문 체크
            checkedArray[i] = true;
            // 재귀 호출
            DFS(k- dungeons[i][1], dungeons, count + 1, checkedArray);
            // 방문 체크 해제
            checkedArray[i] = false;
        }
    }
    // 최댓값을 구하기
    answer = answer < count ? count : answer;
}
    DFS(k, dungeons, 0, checkedArray)
    
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

