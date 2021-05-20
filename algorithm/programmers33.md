


# [프로그래머스] 삼각 달팽이 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 삼각 달팽이
def solution(n):
    # n을 변으로 가지는 이등변직각삼각형 만들기
    triangle = [[0 for i in range(0, j)] for j in range(1, n + 1)]
    # 숫자 채우기
    # 행
    x = -1
    # 열
    y = 0
    # 넣을 수
    k = 1
    # 행 접근
    for a in range(n):
        # 열 접근
        for b in range(a, n):
            if a % 3 == 0:
                x += 1
            elif a % 3 == 1:
                y += 1
            elif a % 3 == 2:
                x -= 1
                y -= 1
            triangle[x][y] = k
            k += 1
    # 1차원 리스트로 변환        
    answer = sum(triangle, [])
    return answer
```



## Comment

인덱스에 번호에따라 숫자가 어떻게 적혀지는지 분석하여 풀어야 한다.

# Reference

[프로그래머스](https://programmers.co.kr)