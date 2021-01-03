# [동빈나]이코테 2021 강의 몰아보기(6)(2021.1.4)



**본 내용은 해당 [강의](https://www.youtube.com/watch?v=7C9RgOcvkvo&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=3) 토대로 작성**



# 그래프 탐색 알고리즘: DFS/ BFS

* 탐색(Search)이란 **원하는 데이터를 찾는 과정**
* DFS, BFS
  * 자주 출제되는 유형



## 1. DFS (Depth-First Search)

* 깊이 우선 탐색
* 그래프에서 **깊은 부분을 우선적으로 탐색**하는 알고리즘
* **스택 자료 구조(혹은 재귀함수)**를 이용
* 동작 과정
  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
  2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
  3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복

![Codingtest6-1](images/Codingtest6-1.gif)



### DFS 소스코드 예제

```python
# DFS 메서드 정의
def dfs(graph, v, visited): # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    for i in graph[v]: # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
        if not visited[i]: # 해당 노드가 방문하지 않은 상태
            dfs(graph, i, visited)
# 각 노드가 연결된 정보를 표현 (2차원 리스트)
graph = [
  [], # 0번 인덱스는 비워두기
  [2, 3, 8], # 각 인덱스에 노드의 번호대로 입력, 노드가 연결되어 있는 번호들 쓸 것
  [1,7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 표현 (1차원 리스트)
visited = [False] * 9 # 하나도 방문하지 않은 것처럼 처리

# 정의돈 DFS 함수 호출
dfs(graph, 1, visited)
```

* 실행 결과 : 1 2 7 6 8 3 4 5

## 2. BFS (Bread-First Search)

* 너비 우선 탐색
* 그래프에서 **가까운 노드부터 우선적으로 탐색**하는 알고리즘
* **큐 자료구조** 이용
* 동작 과정
  1. 탐색 시작 노드를 큐에 삽입 후 방문 처리
  2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입 후 방문 처리
  3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복
* 최단 거리 문제 해결 가능

![Codingtest6-2](images/Codingtest6-2.gif)



### BFS 소스코드 예제

```python
from collections import deque # 라이브러리 불러오기

# BFS 메서드 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력하기
        v = queue.popleft()
        print(v, end = " ")
        # 아직 방문하지 않은 인접한 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] =True
                
 # 각 노드가 연결된 정보를 표현 (2차원 리스트)
graph = [
  [],
  [2, 3, 8],
  [1, 7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 표현 (1차원 리스트)
visited = [False] * 9

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)
```

* 실행 결과 : 1 2 7 6 8 3 4 5



## 3. DFS & BFS 기초 문제 풀이

## <문제> 음료수 얼려 먹기

### 문제 설명

>N x M 크기의 얼음 틀이 있다. 구멍이 뚫려 있는 부분은 0, 칸막이가 존재하는 부분은 1로 표시된다. 구멍이 뚫린 부분끼리 상, 하, 좌, 우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주한다. 얼음 틀의 모양이 주어졌을 때 , 생성되는 총 아이스크림의 개수를 구하는 프로그램 을 작성하라



### 문제 조건

* 풀이 시간 : 30분
* 시간 제한 : 1초
* 메모리 제한 : 128MB
* 입력 조건 : 
  * 첫 번째 줄에 얼음 틀의 세로 길이 N과 가로 길이 M이 주어진다.
  * 두 번째 줄부터 N + 1번째 줄까지 얼음 틀의 형태가 주어진다.
  * 구멍이 뚫린 부분은 0, 그렇지 않은 부분은 1이다.
* 출력 조건 : 
  * 한 번에 만들 수 있는 아이스크림의 개수를 출력



### 문제 해결 아이디어

* DFS 혹은 BFS로 해결
* 연결된 구멍이 뚫린 부분을 노드로 표현
* 이동 가능한 모든 경로에 대해서 방문처리
* 모든 노드의 지점에 대해 DFS, BFS를 수행해서 방문처리가 이루어지는 지점에서만 카운트를 한다.
* DFS를 활용하는 알고리즘
  1. 특정 지점의 주변 상, 하, 좌, 우를 살펴본 뒤에 지점 중에서 값이 '0'이면서 아직 방문하지 않은 지점이 있다면 해당 지점 방문
  2. 방문 지점에서 다시 상, 하, 좌, 우를 살펴보고 방문 진행 과정 반복 -> 연결된 모든 지점을 방문 가능
  3. 모든 노드에 대해 1~2번 과정 반복



### 답안 예시

```python
# N, M을 공백을 기준으로 구분하여 입력 받기
n, m = map(int, input().split())

# 2차원 리스트의 맵 정보 입력 받기
graph = []
for i in range(n):
  graph.append(list(map(int, input())))

# DFS로 특정 노드를 방문하고 연결된 모든 노드를 방문
def dfs(x, y):
  # 주어진 범위를 벗어나는 경우에는 즉시 종료
  if x <= -1 or x >= n or y <= -1 or y >= m:
    return False
  # 현재 노드를 아직 방문하지 않았다면
  if graph[x][y] == 0:
    # 해당 노드 방문 처리
    graph[x][y] = 1
    # 상, 하, 좌, 우의 위치들도 모두 재귀적으로 호출
    dfs(x -1, y) # 단순히 방문 처리만 한다. return 값 사용하지 않는다.
    dfs(x, y - 1)
    dfs(x + 1, y)
    dfs(x, y + 1)
    return True
  return False

  # 모든 노드(위치)에 대하여 음료수 채우기
result = 0
    for i in range(n):
      for j in range(m):
      # 현재 위치에서 DFS 수행
          if dfs(i, j) == True:
              result += 1 # 처음 방문하고 상하좌우가 비어있을 경우 카운트
print(result) # 정답 출력
```



## <문제> 미로 탈출

### 문제 설명

> N x M 크기의 직사각형 형태의 미로에서 괴믈을 피해 탈출한다. 처음 위치는 (1,1)이며, 미로의 출구는 (N,M)에 위치에 있다. 한번에 한 칸씩 이동하여 괴물이 있는 0을 피해 1을 통해서 탈출한다. 이 때, 최소 칸의 개수를 구하여라.



### 문제 조건

* 풀이 시간 : 30분
* 시간 제한 : 1초
* 메모리 제한 : 128MB
* 입력 조건 : 첫째 줄에 두 정수(4<=N, M<=200)이 주어진다. 다음 N개의 줄에는 각각 M개의 정수(0 혹은 1)로 미로의 정보가 주어진다. 각각의 수들은 공백없이 붙어서 입력으로 제시. 시작과 마지막칸은 1이다.
* 출력 조건: 첫째 줄에 최소 이동 칸의 개수를 출력



### 문제 해결 아이디어

* BFS를 사용하여 해결
  * 최단거리 문제를 풀 수 있다.
* 상, 하, 좌, 우로 연결된 모든 노드로의 거리가 1로 동일
  * 모든 노드의 최단 거리 값을 기록하면 해결



### 답안 예시

```python
rom collections import deque

# N, M을 공백을 기준으로 구분하여 입력 받기
n, m = map(int, input().split())
# 2차원 리스트의 맵 정보 입력 받기
graph = []
for i in range(n):
    graph.append(list(map(int, input())))

# 이동할 네 가지 방향 정의 (상, 하, 좌, 우)
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

# BFS 소스코드 구현
def bfs(x, y):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque()
    queue.append((x, y))
    # 큐가 빌 때까지 반복하기
    while queue:
        x, y = queue.popleft()
        # 현재 위치에서 4가지 방향으로의 위치 확인
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            # 미로 찾기 공간을 벗어난 경우 무시
            if nx < 0 or nx >= n or ny < 0 or ny >= m:
                continue
            # 괴물인 경우 무시
            if graph[nx][ny] == 0:
                continue
            # 해당 노드를 처음 방문하는 경우에만 최단 거리 기록
            if graph[nx][ny] == 1:
                graph[nx][ny] = graph[x][y] + 1
                queue.append((nx, ny))
    # 가장 오른쪽 아래까지의 최단 거리 반환
    return graph[n - 1][m - 1]

# BFS를 수행한 결과 출력
print(bfs(0, 0))
```



# Reference

DFS (https://ko.wikipedia.org/wiki/깊이_우선_탐색)

BFS (https://ko.wikipedia.org/wiki/너비_우선_탐색)