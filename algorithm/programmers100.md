# [프로그래머스] 구명보트 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(people, limit) {
    // 보트 카운트
    let boatCount = 0;
    // 시작 지점
    let startIndex = 0;
    // 끝 지점
    let endIndex = people.length - 1;
    // 입력받은 사람 몸무게를 오름차순 정렬
    people.sort((a, b) => a - b);
    // 사람들이 구명보트에 다 탈때까지 실행
    while (startIndex <= endIndex) {
        if (startIndex === endIndex){
            endIndex = -1;
        }
        // 현재 가장 가벼운 사람과 가장 무거운 사람이 보트 한계 이하이면 보트에 태우기
        if ((people[startIndex] + people[endIndex]) <= limit) {
            startIndex += 1;
            endIndex -= 1;
        } else {
            // 아니라면 무거운 사람만 태우기
            endIndex -= 1;
        }
        // 보트 카운트
        boatCount += 1;
    }
    return boatCount;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

