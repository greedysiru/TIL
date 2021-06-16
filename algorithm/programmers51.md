# [프로그래머스] 숫자의 표현 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 숫자의 표현
def solution(n):
    answer = 0
    # 완전탐색으로 만족하는 방법의 수 구하기
    # 시작 수
    start = 1
    # 시작 수가 n을 이하일 때 반복
    while start <= n:
        # 누적합
        sum = 0
        # start부터 n까지 누적합 구하기
        for i in range(start, n + 1):
            sum += i
            # 누적합이 n과 같으면 카운트 후 중단
            if sum == n:
                answer += 1
                break
            # 누적합이 n을 초과하면 중단
            elif sum > n:
                break
        # start를 1 더하여 다음 숫자부터 완전탐색
        start += 1
    return answer
```



## Comment

완전탐색으로 자연수 n을 연속한 자연수들로 표현하는 방법을 구한다.

시작수를 1부터 n이 될때까지 연속되는 누적합을 각 경우에서 구하고 n이 되는 경우만 카운트하면 된다.

while을 사용하여, 시작수가 n이하일 때 실행하도록 하고 그 안의 for문에서 시작수로부터 n까지 i를 더하여 누적합을 구한다. 시간초과를 방지하기 위해서, 도중에 누적합이 n을 넘으면 반복문을 바로 중단한다.

# Reference

[프로그래머스](https://programmers.co.kr)

