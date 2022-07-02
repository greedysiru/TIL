# [프로그래머스] 소수 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(nums) {
    let answer = 0;
    
    // 1. nums의 요소를 처음부터 두 요소가 남을 때까지 순회(첫번째 숫자)
    for (let i = 0; i < nums.length - 2; i++) {
        // 2. 첫번째 숫자 다음 요소부터 한 요소가 남을 때까지 순회(두번째 숫자)
        for (let j = i + 1; j < nums.length - 1; j++) {
            // 3. 두번째 숫자 다음 요소부터 끝까지 순회(세번째 숫자) 
            for (let k = j + 1; k <nums.length; k++) {
              	// 4. 만들어진 세 숫자의 합을 구하기
                const sum = nums[i] + nums[j] + nums[k];
              	// 5. 세 숫자의 합이 소수인지 판별하기 위한 플래그
                let isPrime = true
                // 6. 2부터 세 숫자의 합의 제곱근까지 순회
                for (let l = 2; l * l <= sum; l++) {
                    // 7. 세 숫자의 합을 나누어떨어뜨리는 숫자가 있으면 소수가 아님
                    if (sum % l === 0) {
                      	// 7-1. 플래그를 변경하고 반복문을 종료
                        isPrime = false;
                        break;
                    }
                }
              	// 8. 소수인 경우의 갯수
                if (isPrime) {
                    answer += 1;
                }
            }
        }
    }
    
    return answer;
}
```



## Comment

무려 4중 반복문으로 푼 문제.

## Reference

[프로그래머스](https://programmers.co.kr)

