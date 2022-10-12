# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 머쓱이보다 키 큰 사람

```JavaScript
const solution = (array, height) => {
    // 키큰 사람 수를 필터링
    return array.filter(friendsHeight => friendsHeight > height).length;
}
```



## 2. 짝수 홀수 개수

```JavaScript
const solution = (num_list) => {
    // reduce로 짝수, 홀수 개수를 담은 배열 return
    return num_list.reduce((arr, num) => {
        if (num % 2 === 0) {
            arr[0] += 1;
        } else {
            arr[1] += 1;
        }
        return arr;
    }, [0, 0])
}
```



## 3. 배열 뒤집기

```JavaScript
const solution = (num_list) => {
    return num_list.reverse();
}
```



## 4. 세균 증식

```JavaScript
const solution = (n, t) => {
    return n * (2 ** t)
}
```



## 5. 배열 자르기

```JavaScript
const solution = (numbers, num1, num2) => {
    return numbers.slice(num1, num2 + 1);
}
```





## Reference

[프로그래머스](https://programmers.co.kr)

