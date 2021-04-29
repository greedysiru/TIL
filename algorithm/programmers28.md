


# [프로그래머스] 예상 대진표 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 예상 대진표
import math

def solution(n, a, b):
    answer = 0
    # 진행할 수 있는 경기 수가 1보다 크면 실행
    # 진행하는 경기 수가 1이면 서로 무조건 만나므로
    while True:
        # 현재 라운드 수
        answer += 1
        # 이겼을 때 부여되는 번호 입력
        a = math.ceil(a / 2)
        b = math.ceil(b / 2)
        # 이겼을 때 부여되는 번호가 같으면 중단
        if a == b:
            break
    return answer
```



## Comment

메모장에서 대진표를 직접 그려보고 시뮬레이션하여 빠르게 풀어낼 수 있었다! 어떠한 수도 이기고 나서 자기 자신을 나눈 것의 올림으로 번호가 부여된다는 아이디어를 가지고 코드로 구현하였다. 주어진 a, b 가 만나면 이기고 나서의 수는 같을 것이므로 그 사실을 이용하였다.

# Reference

[프로그래머스](https://programmers.co.kr)