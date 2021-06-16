# [프로그래머스] 디스크 컨트롤러 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 디스크 컨트롤러
import heapq

def solution(jobs):
    answer = 0
    # jobs의 최소힙
    jobs_heap = []
    # 시작 시간, 처음에는 -1 ~ 0 범위의 작업을 찾아야하므로 -1로 초기화
    start = -1
    # 현재 시간
    now = 0
    # 완료된 작업 수
    complited_jobs = 0
    # 작업의 수
    jobs_ea = len(jobs)
    # 모든 작업을 완료할 때 까지 실행
    while complited_jobs < jobs_ea:
        # 주어진 작업을 하나씩 접근
        for job in jobs:
            # 작업을 입력받은 시점이 시작 시간과 현재 시간의 사이인 경우
            if start < job[0] <= now:
                # jobs_heap에 push (최소힙)
                # 0번 인덱스를 기준으로 정렬되므로 0번 인덱스에 작업 처리 시간을 입력
                heapq.heappush(jobs_heap, [job[1], job[0]])
        # 최소힙에 작업이 들어와 있으면
        if jobs_heap:
            # 최소힙으로부터 최소 시간 작업 꺼내기
            min_job = heapq.heappop(jobs_heap)
            # 시작 시간에 현재 시간 입력
            start = now
            # 현재 시간에 최소 시간 작업을 처리한 시간 입력
            now += min_job[0]
            # answer에 현재 시간 - 최소 시간 작업을 입력받은 시점 입력
            answer += now - min_job[1]
            # 작업을 처리하였으므로 +1
            complited_jobs += 1
        # 최소힙에 아무것도 없어도 현재시간은 흘러야 하므로 +1
        else:
            now += 1

    return answer//jobs_ea
```



## Comment

최소힙으로 풀 수 있는 문제. 입력받은 작업을 순차적으로 실행하는 것이 아니라, 최소힙을 사용해서 매번 최소 처리 시간을 가지는 작업부터 수행하여 답을 구해낸다.

시작 시간과, 현재 시간을 기록하며 for문으로 입력 받은 작업 리스트를 하나씩 접근하면서 해당 작업이 시작 시간과 현재 시간의 사이에 들어오면 작업을 수행할 수 있는 것이므로 최소힙에 입력한다.

그 이후, 최소힙에 작업이 들어와 있으면 최소 시간을 꺼내어 시작 시간에는 현재 시간을, 현재 시간에는 최소 시간 작업을 처리한 시간을 입력하여 작업 처리를 한다. 이때, answer에는 현재 시간 - 해당 최소 시간을 입력받은 시점을 입력한다. 해당 작업이 들어온 시점부터 완료된 시점까지를 기록해야하기 때문이다.

모든 작업이 완료되면 answer를 총 작업의 수로 나누어 return한다.

# Reference

[프로그래머스](https://programmers.co.kr)

