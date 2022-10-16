# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. n의 배수 고르기

```JavaScript
const solution = (n, numlist) => numlist.filter(num => num % n === 0);
```



## 2. 가장 큰 수 찾기

```JavaScript
const solution = (array) => array.reduce((arr, item, index) => {
    if (arr[0] < item) {
        arr[0] = item;
        arr[1] = index;
    }
    return arr;
} , [0, 0]);
```



## 3. 369게임

```JavaScript
const solution = (order) => order.toString().match(/[369]/g)?.length || 0;
```



## 4. 순서쌍의 개수

```JavaScript
const solution = (n) => Array.from(new Array(n), (_, i) => i + 1).filter((num) => n % num === 0).length;
```



## 5. 주사위의 개수

```JavaScript
const solution = (box, n) =>  box.reduce((acc, cur) => acc * Math.floor(cur / n), 1);
```





## Reference

[프로그래머스](https://programmers.co.kr)

