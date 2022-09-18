# [프로그래머스] 올바른 괄호 - JavaScript 풀이(개선된 풀이)

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
function solution(s){
    const braketArray = [];
    for (let i = 0; i < s.length; i++) {
        if ( s[i] === ')' && braketArray[braketArray.length - 1] === '(') {
            braketArray.pop();
        } else {
            braketArray.push(s[i]);
        }
    }
    return braketArray.length === 0? true : false;
}
```



## Comment

이전에 구현했을 때는 중복코드가 많았었다. 이번에는 중복코드를 최소화하는 방식으로 구현하였다.

1. 주어진 문자열(괄호)을 하나씩 접근
2. 현재 접근한 괄호가 배열에 들어가 있는 괄호화 짝이 맞추어 진다면, pop
3. 그렇지않다면, 배열에 넣기



## Reference

[프로그래머스](https://programmers.co.kr)

