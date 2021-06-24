


# [프로그래머스] 약수의 개수와 덧셈- JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 약수의 개수와 덧셈

// 약수를 세는 함수
function countMeasure(number) {
  let count = 0
  // 1부터 number까지 number를 나누어떨어지게하면 약수이므로 카운트
  for (let i = 1; i < number + 1; i++) {
    if (number % i === 0) {
      count += 1
    }

  }
  // 약수가 짝수인 경우 양수 리턴
  if (count % 2 === 0) {
    return number
  }
  // 약수가 음수인 경우 음수 리턴
  else {
    return -number
  }
}

function solution(left, right) {
  let answer = 0;
  // left부터 right까지 약수의 개수 세기
  for (let i = left; i < right + 1; i++) {
    answer += countMeasure(i)
  }
  return answer;
}
```



## Comment

주어진 `left`에서`right`까지의 약수 개수를 세기 위해서 약수의 개수를 세는 함수 `countMeasure`를 정의하였다. 이 함수는 1부터 주어진 숫자까지 하나씩 접근한다. 그리고 주어진 숫자를 나누어 떨어지도록 하면 약수이므로 카운트한다. `for문`을 마치면, `count`의 짝수, 홀수 여부를 판별하여 짝수이면 양수, 홀수이면 음수를` return`한다.

정의된 countMeasure를 이용해서`left `부터  `right`까지 함수를 호출하여 누적합을 구한다.



## 프로그래머스 풀이

```JavaScript
function solution(left, right) {
    var answer = 0;
    for (let i = left; i <= right; i++) {
        if (Number.isInteger(Math.sqrt(i))) {
            answer -= i;
        } else {
            answer += i;
        }
    }
    return answer;
}
```



## Comment

제곱근이 정수면 약수의 갯수가 홀수이다. 예를 들어서, 9의 경우 제곱근이 3이다. 9의 약수는 1, 3, 9이므로 홀수이다. 이것을 이용하여 더 간단하게 답을 구할 수 있다.

# Reference

[프로그래머스](https://programmers.co.kr)

