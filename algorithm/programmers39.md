# [프로그래머스] 더 맵게 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
import heapq
# 더 맵게
def solution(scoville, K):
    # 최소힙으로 변환
    heapq.heapify(scoville)
    # 섞은 횟수
    cnt = 0
    # 가장 작은 스코빌 지수가 K 이상이 될 때까지 실행
    while scoville[0] < K:
        cnt += 1
        # 가장 작은 스코빌 지수의 음식
        first_scovile = heapq.heappop(scoville)
        # 두번째로 작은 스코빌 지수의 음식
        second_scovile = heapq.heappop(scoville)
        # 두 음식 섞기
        mix_scovile = first_scovile + (second_scovile * 2)
        # 섞은 음식 포함시키기
        heapq.heappush(scoville, mix_scovile)
        # 모든 음식을 섞은 후에도 K미만인 경우
        if len(scoville) == 1 and scoville[0] < K:
            return -1
    return cnt
```



## Comment

최소힙을 사용하여 푼다. 주어진 스코빌 지수들 중에서 가장 작은 스코빌과 두 번째로 작은 스코빌을 매번 뽑아 섞어야하는데, 시간복잡도에서 힙 자료형은 삽입 시간과 삭제 시간이 O(logN)을 보장하기 때문이다. 그리고, 코드를 작성하는 측면에서도 간편하다. 매번 정렬할 필요 없이 heappop을 사용하면 가장 작은 값을 우선적으로 뽑을 수 있기 때문이다.d

# Reference

[프로그래머스](https://programmers.co.kr)

