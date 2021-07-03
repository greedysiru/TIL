# [프로그래머스] 최대공약수와 최소공배수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 최대공약수와 최소공배수
// 유클리드 호제법으로 최대공약수를 구하는 함수
function findGcd(n, m) {
  if (n % m === 0) {
    return m;
  } else {
    return findGcd(m, n % m)
  }
}

function solution(n, m) {
  let answer = [];
  // 최대공약수
  const gcd = findGcd(n, m);
  // 최대공배수 구하기
  const lcm = n * m / gcd;
  answer.push(gcd);
  answer.push(lcm);
  return answer;
}
```



## Comment

최대공약수를 유클리드 호제법으로 구한다. 

**유클리드 호제법**

* 두 자연수 A,B에 대하여 (A > B) A를 B로 나눈 나머지를 R이라고 한다.
* 이때, A와 B의 최대공약수는 B와 R의 최대공약수와 같다.

최소공배수는 아래와 같은 공식으로 구한다.

> LCM =  A * B / GCD

## Reference

[프로그래머스](https://programmers.co.kr)

