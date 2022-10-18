# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 외계행성의 나이

```JavaScript
const solution = (age) => age.toString().split('').map(number => String.fromCharCode(Number(number) + 97)).join('');
```



## 2. 암호 해독

```JavaScript
const solution = (cipher, code) => cipher.split('').filter((_, index) => (index + 1) % code === 0).join('');
```



## 3. 중복된 문자 제거

```JavaScript
const solution = (my_string) => [...new Set(my_string.split(''))].join('');
```



## 4. k의 개수

```JavaScript
const solution = (i, j, k) => {
    let answer = 0;
    const searchNum = k.toString();
    for (let num = i; num <= j; num++) {
        const match = num.toString().match(new RegExp(searchNum, "g"))?.length;
        answer += match !== undefined? match : 0;
    }
    return answer;
}
```



## 5. 가까운 수

```JavaScript
const solution = (array, n) => array.reduce((result, number) => {
    const diff = Math.abs(n - number);
    if (diff < result[1]) {
        result[1] = diff;
        result[0] = number;
    } else if (diff === result[1]) {
        result[0] = result[0] > number? number: result[0];
    }
    return result
}, [0, Infinity])[0];
```





## Reference

[프로그래머스](https://programmers.co.kr)

