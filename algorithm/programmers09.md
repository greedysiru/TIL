
# [프로그래머스] 내적 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 내적
def solution(a, b):
    # 내적을 담을 변수
    dot_product = 0
    # 내적 구하기
    # a, b는 길이가 같은 배열
    # 길이만큼 주어진 식대로 구하기
    for i in range(len(a)):
        dot_product += a[i] * b[i]

    answer = dot_product
    return answer
```



## Comment

문제에 주어진 내적의 식 대로 풀면 된다. 

# Reference

[프로그래머스](https://programmers.co.kr)

