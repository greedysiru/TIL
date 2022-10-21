# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 약수 구하기

```JavaScript
const solution = (n) => Array.from({length: n}, (_, index) => index + 1).filter(number => n % number === 0);
```



## 2. 숨어있는 숫자의 덧셈(1)

```JavaScript
const solution = (my_string) => my_string.match(/[0-9]/g).reduce((acc, cur) => acc + Number(cur), 0);
```



## 3. 문자열 정렬하기(1)

```JavaScript
const solution = (my_string) => my_string.match(/[0-9]/g).map((string) => Number(string)).sort((a, b) => a - b);
```



## 4. 최댓값 만들기(2)

```JavaScript
const solution = (numbers) => {
    numbers.sort((a, b) => a - b);
    return Math.max(numbers[0] * numbers[1], numbers[numbers.length - 2] * numbers[numbers.length - 1]);
}
```



## 5. 피자 나눠 먹기(2)

```JavaScript
const solution = (n) => {
    // 유클리드 호제법으로 최대공약수 구하기
    const getGCD = (a, b) => {
        if (a % b === 0) {
            return b;
        } else {
            return getGCD(b, a % b);
        }
    }
    const GCD = getGCD(6, n);
    return n / GCD;
}
```





## Reference

[프로그래머스](https://programmers.co.kr)

