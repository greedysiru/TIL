# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 문자열 정렬하기 (2)

```JavaScript
const solution = (my_string) => {
    return my_string.toLowerCase().split('').sort().join('');
}
```



## 2. 피자 나눠 먹기 (1)

```JavaScript
const solution = (n) => {
    return Math.ceil(n / 7);
}
```



## 3. 배열 원소의 길이

```JavaScript
const solution = (strlist) => {
    return strlist.map((str) => str.length);
}
```



## 4. 제곱수 판별하기

```JavaScript
const solution = (n) => Number.isInteger(Math.sqrt(n))? 1 : 2;
```



## 5. 특정 문자 제거하기

```JavaScript
const solution = (my_string, letter) => my_string.replaceAll(letter, '');
```





## Reference

[프로그래머스](https://programmers.co.kr)

