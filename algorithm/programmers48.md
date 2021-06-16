# [프로그래머스] 최고의 집합 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 최고의 집합
def solution(n, s):
    # 자연수의 개수 n보다 s의 크기가 작은 경우는 불가능
    if n > s:
        return [-1]
    # 합이 s가 되는 자연수들의 리스트
    s_sum_list = []
    # 각 자연수 간의 차이를 최소화할 최적의 수
    optimized_number = s // n
    # s_sum_list에 최적의 수를 n 만큼 넣었을 때의 나머지
    optimized_left = s % n
    # 최적의 수를 n만큼 넣기
    for i in range(n):
        s_sum_list.append(optimized_number)
    # optimized_left가 0보다 큰 경우 optimized_number의 요소에 더하기
    for j in range(optimized_left, 0, -1):
        s_sum_list[-j] += 1

    return s_sum_list
```



## Comment

합이 s가 되는 자연수 n개의 집합 중에서 곱이 최대가 되기 위해서는 집합을 이루는 각 숫자의 차이가 최소화 되어야 한다. 

예를 들어서, 합이 10이 되는 4개의 자연수가 곱이 최대가 되기 위해서는 2, 2, 3, 3 이다. 여기서 10을 4로 나눈 몫은 2이고 나머지는 2이다. 몫을 4개의 자연수 기본값으로 두면 [2, 2, 2, 2]가 되고 나머지를 맨 뒤의 원소부터 1씩 더하면 [2, 2, 3, 3]이 된다. 이 집합은 각자의 차이가 최소이므로 최고의 집합이다.

# Reference

[프로그래머스](https://programmers.co.kr)

