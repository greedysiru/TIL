# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (13) (2021.3.15)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**

# 1260

[문제 링크](https://www.acmicpc.net/problem/1260)

```python
# BFS를 사용하기위해 deque 가져오기
from collections import deque
# N: 정점의 개수 , M: 간선의 개수, V: 탐색을 시작할  정점의 번호
N, M, V = map(int, input().split())
# 간선의 개수만큼 입력 받기
# 인접 리스트를 받을 리스트 선언
G = [[] for _ in range(N + 1)]
# 입력받은 정보를 인접 리스트로 변환하기
for _ in range(M):
    a, b = map(int, input().split())
    G[a].append(b)
    G[b].append(a)
# 이차원 리스트의 각 리스트를 오름차순 정렬
for x in G:
    x.sort()
# DFS 정의
# 방문한 노드를 기록할 리스트
visit_array_dfs = []

def DFS(cur_node, adj_array, visit_array):
    # 현재 노드를 방문 배열에 기록
    visit_array.append(cur_node)
    # 방문한 노드를 출력
    print(cur_node, end=" ")
    # 인접 리스트에서 하나씩 탐색
    for adj_node in adj_array[cur_node]:
        # 현재 노드의 인접 노드가 방문 하지 않았으면
        if adj_node not in visit_array_dfs:
            # DFS 호출
            DFS(adj_node, adj_array, visit_array_dfs)

# 방문한 노드를 기록할 리스트
visit_array_bfs = []

def BFS(satart_node, adj_array):
    # 방문할 곳을 기록하는 큐를 출발하는 노드로 초기화
    visit_Q = [satart_node]
    visit_Q = deque(visit_Q)
    # 방문할 곳이 기록된 큐가 빌 때까지 반복
    while visit_Q:
        # 큐에 가장 먼저 들어온 노드를 현재 노드로 빼기
        cur_node = visit_Q.popleft()
        # 방문 리스트에 기록
        visit_array_bfs.append(cur_node)
        # 방문 노드 출력하기
        print(cur_node, end=" ")
        # 인접 노드 탐색
        for adj_node in adj_array[cur_node]:
            # 인접 노드가 방문하지 않았으면 큐에 추가
            if adj_node not in visit_array_bfs and adj_node not in visit_Q:
                visit_Q.append(adj_node)

DFS(V, G, visit_array_dfs)
print()
BFS(V, G)
```



## Comment

나는 받은 데이터를 인접리스트로 변환하였는데, 여기서 꼭 정렬을 해야 올바른 정답이 나온다.  로직자체가 맞아도 입력으로 값이 뒤죽박죽 들어오게 되면 답또한 틀려지기 때문이다.



# 2108

[문제 링크](https://www.acmicpc.net/problem/2108)

```python
# 산술평균 : N개의 수들의 합을 N으로 나눈 값
# 중앙값 : N개의 수들을 증가하는 순서로 나열했을 경우 그 중앙에 위치하는 값
# 최빈값 : N개의 수들 중 가장 많이 나타나는 값
# 범위 : N개의 수들 중 최댓값과 최솟값의 차이
import sys
from collections import Counter
# 수의 개수 N, N은 홀수
N = int(input())
# 수 입력 받기
num_array = []
for _ in range(N):
    num_array.append(int(sys.stdin.readline()))
# 중앙값을 구하기 위해서 오름차순 정렬
num_array.sort()
# 산술 평균
sum_array = sum(num_array)
# 반올림
print(round(sum_array / N))

# 중앙값
mid = N // 2
print(num_array[mid])

# 최빈값
# Counter 사용, 각 수의 빈도수를 dict로 만든다.
cnt_dict = Counter(num_array)
# .most_common()은 빈도수가 높은 순으로 튜플 형태로 정리 (수, 빈도수), 빈도수가 같으면 해당 수 기준 오름차순으로 정리된다.
cnt = cnt_dict.most_common()
# 하나 밖에 없는 경우
if len(cnt) == 1:
    print(cnt[0][0])
# 최빈값이 여러개인 경우 최빈값 중 두 번째로 작은 값 출력
elif cnt[0][1] == cnt[1][1]:
    print(cnt[1][0])
else:
    # 같지 않다면 최빈값 출력
    print(cnt[0][0])

# 범위
print(num_array[-1] - num_array[0])
```



## Comment

Counter를 사용하지 않으려 했으나 시간초과가 떠서 어쩔 수 없이 사용했다.

