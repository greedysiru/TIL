# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (14) (2021.3.16)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 2667

[문제 링크](https://www.acmicpc.net/problem/2667)

```python
# 큐 자료형 사용하기위해 deque import
from collections import deque
# 지도의 크기
N = int(input())
# 지도 정보 입력 받기
M = [list(input()) for _ in range(N)]

# 지도의 정보 정수형으로 변환
for i in range(N):
    M[i] = list(map(int, M[i]))

# 방향
# 상, 하
dx = [-1, 0, 1, 0]
# 좌, 우
dy = [0, -1, 0, 1]

# 집 수를 카운트할 리스트 선언
cnt_list = []
# 카운트를 저장할 변수 선언
cnt = 0

# 깊이 우선 탐색으로 지도의 단지를 탐색
# M: 탐색할 지도, S: 시작점의 행,열번호
def BFS(M, x, y):
    # 글로벌 변수 선언
    global cnt
    # 시작점이 1이므로 카운트
    cnt += 1
    # 방문했으므로 0으로 바꾸기
    M[x][y] = 0
    # 시작점
    start = [[x, y]]
    # 큐
    Q = deque(start)
    # 큐가 빌때까지 진행
    while Q:
        # 현재 진행할 지점
        cur = Q.popleft()
        # for문을 이용하여 dx, dy를 돌아가며 참조
        for j in range(4):
            # 이동할 행, 열번호
            xx = cur[0] + dx[j]
            yy = cur[1] + dy[j]
            # 이동할 좌표가 경계를 넘지 않고 집이 있는 곳(1)이면 이동
            if 0 <= xx < N and 0 <= yy < N and M[xx][yy] == 1:
                # 집의 수 카운트
                cnt += 1
                # 이동했으므로 0으로 바꾸기
                M[xx][yy] = 0
                # 큐에 append
                Q.append([xx, yy])
    # cnt를 리스트에 기록
    cnt_list.append(cnt)
    # 0으로 초기화
    cnt = 0

# M의 모든 좌표를 탐색
for x in range(N):
    for y in range(N):
        # 집이 있는 곳을 BFS 호출
        # BFS인해 근처에 1이 있다면 퍼져나가면서 단지의 집 수를 카운트
        if M[x][y] == 1:
            BFS(M, x, y)

# 카운트를 오름차순으로 정렬
cnt_list.sort()

# 단지 수 출력
# cnt_list의 원소수 == 단지 수
print(len(cnt_list))
# cnt_list의 원소를 각각 접근하며 출력
for count in cnt_list:
    print(count)
```



## Comment

퍼지게하는 것을 구현하는데에 힘들었다.



# 11054

[문제 링크](https://www.acmicpc.net/problem/11054)

```python
# 수열의 길이 N
N = int(input())
# 수열의 정보
S = list(map(int, input().split()))

# 메모이제이션
# 각 인덱스에서의 최대 증가 수열, 감소 수열의 길이를 넣기
# 증가수열
memo_i = [1] * N
# 감소수열
memo_d = [1] * N
# 바이토닉수열은 증가하는 수열과 감소하는 수열이 합쳐진 형태이다.
# 그러므로, 각 인덱스에서의 최대 증가하는 수열, 최대 감소하는 수열의 길이를 합하면 가장 긴 바이토닉 수열을 구할 수 있다.


# 각 인덱스 부분 수열 길이 구하기
# 증가수열
for i in range(N):
    # 인덱스 i번에서의 증가하는 수열의 최대 길이 구하기
    for j in range(i):
        # 이전값이 지금값보다 작으면
        if S[j] < S[i]:
            memo_i[i] = max(memo_i[j] + 1, memo_i[i])

# 수열을 뒤집고 다시 부분 수열 길이를 구한다.
# 뒤집어서 구하는 경우, 감소하는 부분수열을 구하는 것과 같다.
S.reverse()

for i in range(N):
    # 인덱스 i번에서의 증가하는 수열의 최대 길이 구하기
    for j in range(i):
        # 이전값이 지금값보다 작으면
        if S[j] < S[i]:
            memo_d[i] = max(memo_d[j] + 1, memo_d[i])

# 뒤집힌 상태를 기록한것이므로 결과를 다시 뒤집는다.
memo_d.reverse()

# 최댓값 구하기
res = 0
for k in range(N):
    merge = memo_i[k] + memo_d[k]
    if res < merge:
        res = merge

# 해당 인덱스가 두 번 더해졌으므로 -1한다.
print(res - 1)
```



## Comment

제일 어려웠던 문제. 복습해야할 것 같다.

# 1753

[문제 링크](https://www.acmicpc.net/problem/1753)

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



## Comment

다익스트라 알고리즘을 복습하여 풀 수 있는 문제였다.