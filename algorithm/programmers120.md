# [프로그래머스] 7의 개수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
function solution(array) {
    let answer = 0;
    // 주어진 array 순회
    array.forEach((number) => {
        // 순회를하기 위해 문자열로 변환
        const numberToString = number.toString();
        // 7의 개수를 새기
        answer += numberToString.split('').filter(num => num === '7').length;
    })
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

