# [프로그래머스] 삼총사 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (number) => {
    let answer = 0;
    const endIndex = number.length - 1
    for (let i = 0; i <= endIndex - 2; i++) {
        const first = number[i];
        for (let j = i + 1; j <= endIndex - 1; j++ ) {
            const second = number[j];
            for (let k = j + 1; k <= endIndex; k++) {
                const third = number[k];
                const sum = first + second + third;
                if (sum === 0) {
                    answer += 1;
                }
            }
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

