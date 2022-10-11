# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 1. 점의 위치 구하기

```JavaScript
const solution = (dot) => {
    const [x, y] = dot;
    if (x > 0 && y > 0) {
        return 1;
    } else if (x < 0 && y > 0) {
        return 2;
    } else if (x < 0 && y < 0) {
        return 3;
    } else if (x > 0 && y < 0) {
        return 4;
    }
}
```



## 2. 아이스 아메리카노

```JavaScript
const solution = (money) => {
    const americanoCost = 5500;
    const glasses = parseInt(money / americanoCost);
    const change = money - glasses * americanoCost;
    return [glasses, change];
}
```



## 3. 편지

```JavaScript
const solution = (message) => message.length * 2;
```



## 4. 삼각형의 완성조건(1)

```JavaScript
const solution = (sides) => Math.max(...sides) * 2 < sides.reduce((acc, cur) => acc + cur)? 1 : 2;
```



## 5. 최댓값 만들기

```JavaScript
const solution = (numbers) => {
    numbers.sort((a, b) => b - a);
    return numbers[0] * numbers[1];
}
```



## 6. 문자열 뒤집기

```JavaScript
const solution = (my_string) => my_string.split('').reverse().join('');
```



## 7. 양꼬치

```JavaScript
const solution = (n, k) => (n * 12000) + (k * 2000) - (Math.floor(n / 10) * 2000);
```





## Reference

[프로그래머스](https://programmers.co.kr)

