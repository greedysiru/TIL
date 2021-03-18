# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (16) (2021.3.18)

**풀었던 문제들을 복습**



# 01. 재귀함수

* 정의할 때 자기 자신을 참조하는 함수
* Recursion 오류를 방지하기 위해서 빠져나가는 지점을 만들어야 한다.
  * if문을 사용해서 특정 지점을 정해 return을 시켜준다.
* 호출될 때마다 메모리에 스택이 쌓인다.



## 예제: 하노이의 탑

```python
# 디스크의 수
N = int(input())

# 디스크를 옮기는 재귀함수
# N: 디스크, s: 시작 장대, m: 중간 장대, e: 도착 장대
def moveDisk(N, s, m, e):
    # 옮길 디스크가 없을 때
    if N == 0:
        return
    else:
        # N - 1 개의 디스크를 중간 장대로 옮긴다.
        moveDisk(N - 1, s, e, m)
        # 옮긴 디스크와 시작 장대, 도착 장대를 출력
        print(N, s, e)
        # 중간 장대에 옮긴 디스크를 도착 장대로 옮긴다
        moveDisk(N - 1, m, s, e)

moveDisk(N, 1, 2, 3)
```



# 02. 이진 탐색

* 순차 탐색과 달리 반씩 후보를 줄이면서 탐색



## 예제: 백준 2805

```python
# 자르는 높이를 이진 탐색하기
# n: 나무의 수, m: 가지고 갈 나무의 길이
n, m = map(int, input().split())
# 나무의 높이
trees = list(map(int, input().split()))
# 자르는 높이의 시작점
start = 1
# 결과값
res = 0
# 자르는 높이의 끝점
end = max(trees)

def sumCut(mid):
    # 잘린 나무의 높이
    cut = 0
    for tree in trees:
        if tree > mid:
            cut += tree - mid
    return cut

while start <= end:

    # 자르는 높이의 중간점(절단기의 현재 높이)
    mid = (start + end) // 2
    cut = sumCut(mid)
    # 더 잘렸거나 맞게 잘랐을 때
    if cut >= m:
        start = mid + 1
        # 최댓값 구하기
        if res < mid:
            res = mid
    # 덜 잘렸을 때
    elif cut < m:
        end = mid - 1
print(res)
```



# 03. 동적 계획법

* 복잡한 문제를 여러 개의 문제로 나누어 푸는 방법
* 하위 문제의 결과를 기록, 그것을 이용 -> 메모이제이션



## 예제: 백준 11053

**가장 긴 증가하는 부분 수열**

```python
n = int(input())
arr = list(map(int, input().split()))
arr.insert(0, 0)
# 1번 ~n번 리스트
dy = [0] * (n + 1)
# 각 인덱스에서의 부분수열 길이
dy[1] = 1
# 첫번째 인덱스의 부분 수열 길이
res = 0
# 답
for i in range(2, n + 1):  # 각 인덱스 부분 수열 길이 구하기
    max = 0
    for j in range(i - 1, 0, -1):  # i번째 인덱스 앞 탐색
        if arr[j] < arr[i] and dy[j] > max:
            max = dy[j]
    dy[i] = max + 1
    if dy[i] > res:
        res = dy[i]
print(res)
print(dy)
```



# 04. DFS, BFS

* DFS: 깊이 우선 탐색
  * 끝까지 파고드는 것
  * 공간을 적게 쓰지만 최단 경로를 탐색하기 쉽지 않다.
  * 갈 수 있는 만큼 계속 탐색하다가 갈 수 없을 때 다른 방향으로 다시 탐색
  * 재귀함수, 스택으로 구현
* BFS: 넓이 우선 탐색
  * 모든 분기되는 수를 다 보는 것
  * 최단경로를 쉽게 찾는다.
  * 공간을 많이 쓰고 시간이 오래걸릴 수 있다.
  * 큐로 구현



## 예제: 백준 1260

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



# 05. 최단경로

## 다익스트라 알고리즘

* 특정 노드 -> 다른 모든 노드로 가는 최단 경로 계산

* 음의 간선이 없을 때

* 그리디 알고리즘

  * 매 상황에서 가장 비용이 적는 노드 선택

* 출발 노드 -> 최단 거리 테이블 초기화 -> 미방문 노드 중 최단거리 가장 짧은 노드 선택 -> 해당 노드를 거쳐 다른 노드로 가는 비용을 계산 후 최단거리 갱신

  * 위를 반복

  

### 예제: 백준 1753

```python
import sys
import heapq

# 우선순위 큐 사용
import heapq
INF = float('inf')  # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
V, E = map(int, sys.stdin.readline().split())
# 시작 노드 번호를 입력받기
start = int(sys.stdin.readline().split()[0])
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(V + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (V + 1)

# 모든 간선 정보를 입력받기
for _ in range(E):
    u, v, w = map(int, sys.stdin.readline().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[u].append((v, w))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, q에 삽입
    # 힙정렬 사용 -> 오름차순 정렬
    # 방문하지 않은 노드 중에서 최단거리가 가장 짧은 노드를 선택할 수 있다.
    # O(NlogN)
    # 큐는 맨 앞의 값을 기준으로 정렬되므로 기존의 순서와바꾸어 입력한다.
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:  # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        # 거리값이 테이블의 거리값보다 크면 방문처리가된 정점으로 간주
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, V + 1):
    # 도달할 수 없는 경우, INF출력
    if distance[i] == INF:
        print("INF")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```



## 플로이드 워셜 알고리즘

* 모든 노드에서 다른 모든 노드까지의 최단 경로 계산
* 단계별로 거쳐가는 노드를 기준으로 알고리즘 수행
* 다이나믹 프로그래밍 유형



### 구현

```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    # 가장 짧은 간선 정보만 저장
    if c < graph[a][b]:
        graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        # 도달할 수 없는 경우, 무한(INFINITY) 출력
        if graph[a][b] == INF:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()
```

