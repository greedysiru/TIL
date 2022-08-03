# [프로그래머스] JadenCase 문자열 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(s) {
 return s.split(' ')
            .map(word =>  
            typeof word[0] === 'string' ?
            `${word[0].toUpperCase()}${word.slice(1).toLowerCase()}`
            : word.toLowerCase()
            ).join(' ');
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

