# [프로그래머스] 줄 서는 방법 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 줄 서는 방법
import math


def solution(n, k):
    # 줄서는 사람
    people = [_ for _ in range(1, n + 1)]
    # 답을 넣을 리스트
    answer = []
    while (n != 0):
        # 한 사람이 앞에 줄을 섰을 때의 경우의 수
        each_first_cases = math.factorial(n) // n
        # k번째를 구하기 위해 한 사람이 앞에 줄을 섰을 때의 경우의 수를 지나간 수
        passed = k // each_first_cases
        # 나머지를 k에 넣기
        k = k % each_first_cases
        if k == 0:
            answer.append(people.pop(passed - 1))
        else:
            answer.append(people.pop(passed))
        n -= 1
    return answer
```



## Comment

처음에는 순열로 푸는 것이라 생각되어서 DFS를 사용하여 중복을 제외한 순열을 만들었으나, 시간초과가 발생하였다.

혼자서 생각해도 풀리지 않아서 구글링으로 여러 답을 찾아보았는데 DFS, 순열에 관한 문제가 아니라 수학적 규칙을 찾는 문제였다. 반복문으로 k번째 줄 서는 방법을 찾는다. 이 때, 각 루프에서 팩토리얼을 사용하여 한 사람이 줄을 섰을 때의 경우의 수를 구한다. 그리고 그 수를 이용하여 목표로하는 경우가 얼마나 지났는지  // 연산을 사용하여 구한다. 그리고 그 나눈 나머지를 k에 넣는다. 

개인적으로 이렇게 수학적인 규칙을 찾아내 푸는 문제가 DFS와 같은 알고리즘 문제보다 더 어려운 것 같다. 

# Reference

[프로그래머스](https://programmers.co.kr)

