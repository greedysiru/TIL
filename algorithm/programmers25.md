




# [프로그래머스] 기능 개발 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 기능 개발
from collections import deque


def solution(progresses, speeds):
    answer = []
    # 주어진 두 리스트를 deque로 변환
    progresses = deque(progresses)
    speeds = deque(speeds)
    # 모든 기능이 완료될 때 까지 반복
    while progresses:
        # 카운트
        cnt = 0
        # progresses의 길이
        progresses_len = len(progresses)
        # progresses에 하나씩 접근하여 speeds 더하기
        for i in range(progresses_len):
            # 100보다 큰 경우 넘어가기
            if progresses[i] >= 100:
                continue
            # speed 더하기
            progresses[i] = progresses[i] + speeds[i]
        # 맨 앞의 기능이 100 이상이면 완료 처리
        while progresses[0] >= 100:
            progresses.popleft()
            speeds.popleft()
            cnt += 1
            # progresses가 빈 경우 중단
            if not progresses:
                break
        # answer에 기록
        if cnt > 0:
            answer.append(cnt)
    return answer
```



## Comment

코드는 파이써닉 하지 않지만 무난하게 통과하였다. while문을 하나만 쓰고 통과할 수 있으므로 반복문을 조금 더 줄이는 노력을 해보자.

내 코드는 while문으로 progresses가 없어질 때 까지 내부의 for문으로 해당 하는 인덱스에 speed를 더해주고 100이 상인 경우 빼주는 방식이다.

# Reference

[프로그래머스](https://programmers.co.kr)