# [프로그래머스] 연속된 수의 합 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num, total) => {
    let result = [];
    let endNumber = total > num? total : num;
    while (true) {
        const startNumber = endNumber - num + 1;
        for (let i = startNumber; i <= endNumber; i++) {
            result.push(i);
        }
        const sum = result.reduce((acc, cur) => acc + cur);
        if (sum === total) {
            break;
        } else {
            result = [];
            endNumber -= 1;
        }
    }
    return result;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

