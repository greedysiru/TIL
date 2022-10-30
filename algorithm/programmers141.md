# [프로그래머스] 직각삼각형 출력하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let input = [];

rl.on('line', function (line) {
    input = line.split(' ');
}).on('close', function () {
    for (let i = 1; i <= input; i++) {
        let astarisk = '';
        for (let j = 1; j <= i; j++) {
            astarisk += '*';
        }
        console.log(astarisk);
    }
});
```



## Reference

[프로그래머스](https://programmers.co.kr)

