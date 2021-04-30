


# [프로그래머스] 예상 대진표 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 2 x n 타일링

# 메모이제이션
memo = {
    1: 1,
    2: 2,
}

def solution(n):
    # memo에 있는 경우
    if n in memo:
        return memo[n]
    # memo에 없는 경우
    else:
        for i in range(3, n + 1):
            # 3부터 해당 수까지 메모이제이션하여 찾기
            memo[i] = (memo[i - 1] + memo[i - 2]) % 1000000007
    return memo[n]
```



## Comment

n이 1, 2, 3, 4, 5 일 때 각각 직접 그려보면서 점화식을 도출하였다. 길이가 n일 때의 경우의 수는 n - 2, n - 1일 때 경우의 수의 합과 같으므로 이것을 for문을 통하여 n까지 메모이제이션하며 구하면 된다. 메모이제이션을 할 때, 문제에서 주어진 수로 나눈 나머지 값을 넣는다.

# Reference

[프로그래머스](https://programmers.co.kr)