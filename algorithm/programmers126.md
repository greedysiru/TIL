# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 배열의 유사도

```JavaScript
const solution = (s1, s2) => s1.filter(e => s2.includes(e)).length;
```



## 2. 짝수는 싫어요

```JavaScript
const solution = (n) => Array.from({length: n + 1}, (_, i) => i).filter((number) => number % 2 === 1);
```



## 3. 옷가게 할인 받기

```JavaScript
const solution = (price) => {
    if (price >= 500000) {
        price *= 0.80;
    } else if (price >= 300000) {
        price *= 0.90;
    } else if (price >= 100000) {
        price *= 0.95;
    }
    return parseInt(price);
};
```



## 4. 모음 제거

```JavaScript
const solution = (my_string) => my_string.replace(/[aeiou]/g, '');
```



## 5. 문자 반복 출력하기

```JavaScript
const solution = (my_string, n) => my_string.split('').map(string => string.repeat(n)).join('');
```





## Reference

[프로그래머스](https://programmers.co.kr)

