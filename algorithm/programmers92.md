# [프로그래머스] 예상 대진표 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n,a,b)
{
    let matchNumber = 0;

    while (true) {
        // 경기 수 더하기
        matchNumber += 1;
        // 각 선수가 이겼을 때 받게 되는 번호 넣기
        a = Math.ceil(a / 2);
        b = Math.ceil(b / 2);
        // 받게 되는 번호가 같으면 중단
        if (a === b) break;
    }

    return matchNumber;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

