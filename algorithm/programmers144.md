# [프로그래머스] 최빈값 구하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (array) => {
    const parsedArray = array.reduce((acc, cur) => {
    const {max} = acc;
    if (!Object.keys(acc).includes(cur.toString())) {
        acc[cur] = 1;
    } else {
        acc[cur] += 1;
    }
    if (max < acc[cur]) {
        return {...acc, max: acc[cur]};
    } else {
        return acc;
    }
    }, {max: 0});
    const {max} = parsedArray;
    delete parsedArray.max;
    const answer = Object.entries(parsedArray).filter(([number, count]) => {
        if (count === max) {
            return number;
        }
    })
    return answer.length === 1? Number(answer[0][0]) : -1;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

