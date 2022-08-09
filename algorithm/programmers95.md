# [프로그래머스] 멀쩡한 사각형 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
// 최대 공약수를 구하는 함수
function gcd(a, b) {
    if (a % b === 0) {
        return b
    } else {
        return gcd(b, a % b);
    }
}

function solution(w, h) {
    // 두 수 w, h의 공약수
    const GCD = gcd(w, h);
    // 총 정사각형의 수
    const totalSquare = w * h;
    // 사용할 수 없는 정사각형의 수
    const unusableSquere = w + h - GCD;
    // 사용할 수 있는 정사각형의 수
    const usableSquere = totalSquare - unusableSquere;
    return usableSquere;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

