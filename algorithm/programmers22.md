



# [프로그래머스] 프린터 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 프린터
from collections import deque

def solution(priorities, location):
    answer = 0
    # 인쇄를 요청한 문서의 위치를 체크하는 배열
    check = deque([0]) * len(priorities)
    # 주어진 대기목록을 deque 변환
    priorities = deque(priorities)
    # 인쇄를 요청한 문서의 위치를 표시
    check[location] = 1
    # 인쇄를 요청한 문서가 몇 번째 오는 지 찾기
    while True:
        # 현재 시점에서 가장 중요한 문서
        important = max(priorities)
        # 가장 앞에 있는 문서
        priorities_front = priorities.popleft()
        # check배열에서 가장 앞에 있는 것
        check_front = check.popleft()
        # 가장 앞에 있는 문서와 가장 중요한 문서가 같으면 출력
        if priorities_front == important:
            # 카운트 하기
            answer += 1
            # 출력된 것이 뽑을 문서이면 중단
            if check_front == 1:
                break
        # 같지 않으면 뒤로 보내기
        else:
            priorities.append(priorities_front)
            check.append(check_front)

    return answer

```



## Comment

주어진 문서 목록을 큐로 바꾼 후, 길이가 같은 별도의 check 덱을 만들었다. 목표로하는 인덱스의 요소를 다른 것과 판별하기 위해서이다. 가장 앞에 있는 요소가 목표로하는 문서인지 확인하며 이때 카운트를 하고 아닐 경우는 다시 뒤로 보냈다. 

# Reference

[프로그래머스](https://programmers.co.kr)

