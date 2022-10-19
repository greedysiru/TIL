# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 개미 군단

```JavaScript
const solution = (hp) =>  [5, 3, 1].reduce((obj, attack) => {
        let {hp, ea} = obj;
        curEa = Math.floor(hp / attack);
        ea += curEa;
        hp -= attack * curEa;
        return {hp, ea};
    }, {hp, ea: 0}).ea;
```



## 2. 배열 회전시키기

```JavaScript
function solution(numbers, direction) {
    switch (direction) {
        case 'right':
            numbers.unshift(numbers.pop());
            return numbers;
        case 'left':
            numbers.push(numbers.shift());
            return numbers;
    }
}
```



## 3. A로 B 만들기

```JavaScript
const countString = (obj, string) => {
    if (obj[string] === undefined) {
        obj[string] = 1;
    } else {
        obj[string] += 1;
    }
    return obj;
}

const solution = (before, after) => {
    let isPassed = 1;
    const beforeStringsEA = before.split('').reduce(countString, {});
    const afterStringsEA = after.split('').reduce(countString, {});
    for (const key in beforeStringsEA) {
        if (beforeStringsEA[key] !== afterStringsEA[key]) {
            isPassed = 0;
        }
    }
    return isPassed;
}
```



## 4. 영어가 싫어요

```JavaScript
const numberToString = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];

const solution = (numbers) => {
    let convertedNumbers = numbers;
    numberToString.forEach((item, index) => {
      convertedNumbers = convertedNumbers.replaceAll(item, index)
    })
    return Number(convertedNumbers);
}
```



## 5. 잘라서 배열로 저장하기

```JavaScript
const solution = (my_str, n) => {
    const answer = [];
    let start = 0;
    let end = n;
    while (start < my_str.length) {
        const str = my_str.slice(start, end);
        answer.push(str);
        start += n;
        end += n;
    }
    return answer;
}
```





## Reference

[프로그래머스](https://programmers.co.kr)

