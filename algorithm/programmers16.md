# [프로그래머스] 두 정수 사이의 합 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 두 정수 사이의 합
def solution(a, b):
    # 둘 중 큰 수를 x에 넣기
    if a > b:
        x = a
        y = b
    else:
        x = b
        y = a
    answer = 0
    for i in range(y, x + 1):
        answer += i
    return answer
```



## Comment

if문으로 분기하여 풀었다.

# Reference

[프로그래머스](https://programmers.co.kr)

