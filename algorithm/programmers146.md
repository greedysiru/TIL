# [프로그래머스] OX퀴즈 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (quiz) => quiz.reduce((answer, cur) => {
    let [expression, result] = cur.split('=');
    let curAnswer = 0;
    if (expression.includes(' +' )) {
        curAnswer = expression.split(' + ').map(num => Number(num)).reduce((acc, cur) => acc += cur);
    } else if (expression.includes(' - ')) {
        curAnswer = expression.split(' - ').map(num => Number(num)).reduce((acc, cur) => acc -= cur);
    }
    return Number(result) === curAnswer? [...answer, 'O'] : [...answer, 'X'];
}, []);
```



## Reference

[프로그래머스](https://programmers.co.kr)

