# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 각도기

```JavaScript
const solution = (angle) => {
    if (angle < 90) {
        return 1;
    } else if (angle === 90) {
        return 2;
    } else if (angle === 180) {
        return 4;
    } else if (angle < 180) {
        return 3;
    }
}
```



## 2. 두 수의 나눗셈

```JavaScript
const solution = (num1, num2) => parseInt((num1 / num2) * 1000);
```



## 3. 중복된 숫자 개수

```JavaScript
const solution = (array, n) => array.filter(number => number === n).length;
```



## 4. 중앙값 구하기

```JavaScript
const solution = (array) => array.sort((a, b) => a - b)[parseInt(array.length / 2)];
```



## 5. 자릿수 더하기

```JavaScript
const solution = (n) => n.toString().split('').reduce((acc, cur) => acc + Number(cur), 0);
```



## 6. 피자 나눠 먹기(3)

```JavaScript
const solution = (slice, n) => Math.ceil(n / slice);
```





## Reference

[프로그래머스](https://programmers.co.kr)

