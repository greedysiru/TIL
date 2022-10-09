# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 1. 문자열 안에 문자열

```JavaScript
const solution = (str1, str2) => str1.includes(str2) ? 1 : 2;
```



## 2. 짝수의 합

```JavaScript
const solution = (n) => {
    let answer = 0;
    for (let i = 2; i <= n; i += 2) {
        answer += i;
    }
    return answer;
}
```



## 3. 배열의 평균값

```JavaScript
const solution = (numbers) => numbers.reduce((acc, cur) => acc + cur, 0) / numbers.length;
```





```JavaScript
const solution = (num1, num2) => num1 - num2;
```



## 2. 두 수의 곱

```JavaScript
const solution = (num1, num2) => num1 * num2;
```



## 3. 두 수의 합

```JavaScript
const solution = (num1, num2) => num1 + num2;
```



## 4. 숫자 비교하기

```JavaScript
const solution = (num1, num2) => num1 === num2 ? 1 : -1; 
```



## 5. 몫 구하기

```JavaScript
const solution = (num1, num2) => parseInt(num1 / num2);
```



## 6. 나머지 구하기

 ```JavaScript
const solution = (num1, num2) => num1 % num2;
 ```



## 7. 나이 출력

```JavaScript
const solution = (age) => 2022 - age + 1;
```





## Reference

[프로그래머스](https://programmers.co.kr)

