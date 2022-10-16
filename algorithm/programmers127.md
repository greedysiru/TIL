# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 대문자와 소문자

```JavaScript
const solution = (my_string) => {
    return my_string.split('').map((string) => {
    const ASCII = string.charCodeAt();
    if (65 <= ASCII && ASCII <= 90) {
        return string.toLowerCase();
    }
        return string.toUpperCase();
    }).join('');
}
```



## 2. 배열 두 배 만들기

```JavaScript
const solution = numbers => numbers.map(number => number * 2);
```



## 3. 숫자 찾기

```JavaScript
const solution = (num, k) => {
    const index = num.toString().indexOf(k.toString());
    return index !== -1 ? index + 1 : index;
}
```



## 4. 가위 바위 보

```JavaScript
function solution(rsp) {
    return rsp.split('').map(r => {
        if (r === '0') {
            return '5'
        } else if (r === '2') {
            return '0'
        } else if (r === '5') {
            return '2';
        }
    }).join('');
}
```



## 5. 인덱스 바꾸기

```JavaScript
const solution = (my_string, num1, num2) =>  `${my_string.slice(0, num1)}${my_string[num2]}${my_string.slice(num1 + 1, num2)}${my_string[num1]}${my_string.slice(num2 + 1)}`;
```





## Reference

[프로그래머스](https://programmers.co.kr)

