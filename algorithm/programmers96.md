# [프로그래머스] 2016년 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(a, b) {
    var answer = '';
    // 진행된 일수
    let date = 0;
    // a월 1일까지의 일수 구하기
    for (let i = 1; i < a; i++) {
        // i가 7이하일 대
        if (i <= 7) {
            // 2월이면 29일(윤년)
            if (i === 2) {
                date += 29;
                continue;
            }
            // 홀수이면 31일
            if (i % 2 === 1){
                date += 31;
                continue;
            } else if (i % 2 === 0) {
                date += 30;
                continue;
            }
        } else if (i >= 8) {
            // 홀수이면 30일
            if (i % 2 === 1) {
                date += 30;
                continue;
            } // 짝수이면 31일
            else if ( i % 2 === 0) {
                date += 31;
                continue
            }
        }
    }
    // 주어진 일수 b를 date에 더하기
    date += b;
    // 주어진 일수를 1을 빼고 7을 나눈 나머지를 요일에 넣기
    const day = (date - 1) % 7;
    switch (day) {
        case 0:
            answer = "FRI";
            break;
        case 1:
            answer = "SAT";
            break;
        case 2:
            answer = "SUN";
            break;
        case 3:
            answer = "MON";
            break;
        case 4:
            answer = "TUE";
            break;
        case 5:
            answer = "WED";
            break;
        case 6:
            answer = "THU";
            break;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

