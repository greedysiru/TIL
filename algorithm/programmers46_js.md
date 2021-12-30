# [프로그래머스] 부족한 금액 계산하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 부족한 금액 계산하기
function solution(price, money, count) {
    // 부족한 금액
    let answer = 0;
    // count만큼 반복
    for (let i = 1; i <= count; i++) {
        // money - 현재 회차 x price
        money -= i * price;
    }
    // money가 음수이면 부족분 출력
    if (money < 0) {
        answer = -money;
    } 
    // money가 양수이면 0을 리턴
    else {
        answer = 0;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

