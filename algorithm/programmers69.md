# [프로그래머스] 큰 수 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

### 실패 코드

* 이중 for문으로 인해, 시간복잡도가 높아 오답처리가 되었음

```javascript
function solution(number, k) {
    let answer = '';
    // 아래의 로직을 k번 반복
    for (let i = 1; i <= k; i++) {
        // 현재 숫자의 자릿수
        const numberLength = number.length;
        let maxNumber = 0;
        // 현재 숫자에서 한 자리씩 빼기
        for (let j = 0; j <= numberLength - 1; j++) {
            // 한자리를 뺀 수
            const removedNumber = number.replace(number[j], '');
            // 가장 큰수로 최신화
            maxNumber = maxNumber < removedNumber ? removedNumber : maxNumber;
        }
        // 가장 큰수를 넣기
        number = maxNumber;
    }
    answer = number;
    return answer;
}
```



### 풀이 코드

* 스택 자료구조(LIFO)로 해결

```JavaScript
function solution(number, k) {
    // 스택 자료 구조로 답을 구하기
    const numberStack = [];
    // 주어진 number를 배열로 변환
    const numberArray = number.split('');
    // 스택 초기화
    numberStack.push(numberArray.shift());
    // numberArray 순회
    for (const number of numberArray) {
        // 스택의 마지막 요소가 현재 접근한 number 보다 작은 경우 숫자 버림처리
        while(numberStack[numberStack.length - 1 ] < number && k > 0) {
            // 버림
            numberStack.pop();
            // k를 빼줌으로, 버림 카운트
            k -= 1;
        }
        numberStack.push(number);
    }
    // 버릴 수가 더 있는 경우 뒤로부터 삭제
    if (k > 0) {
        numberStack.splice(-k)
    }
    return numberStack.join('');
}
```



## Comment

그리디 알고리즘 문제였다. 그리디 알고리즘이란, 현재 상황에서 좋은 것만 고르는 방법이다.

스택이라는 자료구조를 사용하였다. 주어진 숫자를 하나하나 접근하여 높은 자리수부터 채우게 된다. 이때 이전에 넣은 수와 접근한 수를 비교하여 더 큰수가 높은 자리에 위치하도록 해야한다.

## Reference

[프로그래머스](https://programmers.co.kr)

