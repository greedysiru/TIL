# [동빈나]이코테 2021 강의 몰아보기 (10)(2021.1.12)



**본 내용은 해당 [강의](https://www.youtube.com/watch?v=acqm9mM1P6o&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=7) 토대로 작성**



# 최단 경로 알고리즘

## 1. 최단 경로 알고리즘 개요

* **가장 짧은 경로**를 찾는 알고리즘
* 다양한 문제 상황
  * 한 지점 -> 다른 한 지점
  * 한 지점 -> 다른 모든 지점
  * 모든 지점 -> 다른 모든 지점
* 각 지점은 **노드**로 표현
* 지점 간 연결된 도로는 **간선**으로 표현



## 2. 다익스트라 최단 경로 알고리즘

### 다익스트라 최단 경로 알고리즘 개요

* **특정 노드**에서 출발하여 **다른 모든 노드**를 가는 최단 경로 계산
* **음의 간선**이 없을 때 정상적으로 동작
  * 현실 길찾기 문제에서 사용
* 그리디 알고리즘으로 분류
  * **매 상황에서 가장 비용이 적은 노드를 선택**해 임의의 과정 반복



### 알고리즘 동작 과정

1. 출발 노드 설정
2. 최단 거리 테이블 초기화
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드 선택
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신
5. 3번과 4번 반복



### 알고리즘 특징

* 그리디 알고리즘 : **매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택**
* 한 번 처리된 노드의 최단 거리는 고정
  * 한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는다.
* 테이블에 각 노드까지의 최단 거리 정보가 저장
  * 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가적인 기능을 더 넣는다.



### 간단한 구현 방법

```python
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값 10억

# 노드의 개수, 간선의 개수를 입력ㅂ다기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 만들기
graph = [[] for i in range(n + 1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False] * (n + 1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n + 1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
      # 시작 노드에 대해서 초기화
      distance[start] = 0
      visited[start] = True
      for j in graph[start]:
          distance[j[0]] = j[1]
      # 시작 노드를 제외한 전체 n - 1 개의 노드에 대해서 반복
      for i in range(n - 1):
          # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
          now = get_smallest_node()
          visited[now] = True
          # 현재 노드와 연결된 다른 노드를 확인
          for j in graph[now]:
              cost = distance[now] + j[1] # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
              if cost < distance[j[0]]:
                  distance[j[0]] =cost

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY) 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```



### 간단한 구현 방법 성능 분석

* 시간 복잡도 **O(V<sup>2</sup>)**
* 노드의 개수가 많으면 시간 초과 판정



## 3. 우선 순위 큐(Priority Queue)

* **우선 순위가 가장 높은 데이터를 가장 먼저 삭제**하는 자료 구조
* 대부분의 프로그래밍 언어에서 **표준 라이브러리 형태로 지원**

| 자료구조                    | 추출되는 데이터             |
| --------------------------- | --------------------------- |
| 스택(Stack)                 | 가장 나중에 삽입된 데이터   |
| 큐(Queue)                   | 가장 먼저 삽입된 데이터     |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |



### 힙(Heap)

* 우선 순위 큐를 구현하기 위해 사용하는 자료 구조
* **최소 힙**과 **최대 힙**이 있다.
* 다양한 알고리즘에서 사용

| 우선 순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| ---------------------- | --------- | --------- |
| 리스트                 | O(1)      | O(N)      |
| 힙(Heap)               | O(logN)   | O(logN)   |

 

#### 힙 라이브러리 사용 예제 : 최소 힙

```python
import heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```



#### 힙 라이브러리 사용 예제 : 최대 힙

```python
import heapq

# 내림차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```



## 4. 다익스트라 알고리즘 : 개선된 구현 방법

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
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
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```

* 시간 복잡도는 **O(ElogV)**



## 5. 플로이드 워셜 알고리즘

### 플로이드 워셜 알고리즘 개요

* 모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산
* 다익스트라 알고리즘과 마찬가지로 단계별로 **거쳐 가는 노드를 기준으로 알고리즘 수행**
  * 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않다.
* 2차원 테이블에 최단 거리 정보를 저장
* 다이나믹 프로그래밍 유형에 속한다.
* 각 단계 마다 **특정한 노드 k를 거쳐 가는 경우를 확인**
  * a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사
* **점화식**
  * D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)



### 플로이드 워셜 알고리즘 구현

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

* 시간 복잡도는 **O(N<sup>3</sup>)**
* 노드의 개수가 작을 때 사용할 것



# 최단 경로 알고리즘 기초 문제 풀이

## <문제> 전보

### 문제 설명

> N개의 도시에서 각각 다른 도시로 전보를 보낼 수 있다. 단, X라는 도시에서 Y라는 도시로 전보를 보낸다면, 서로간의 통로가 설치되어 있어야 한다. 예를 들어, X에서 Y로 향하는 통로가 있지만, 그 반대의 통로가 없다면 전보를 보낼 수 없다. 또, 전보를 보낼 때는 일정 시간이 소요된다. 도시 C에서 위급 상황이 발생하여 최대한 많은 도시로 전보를 보낼 때 전보를 받는 도시는 몇 곳이며, 소요되는 시간을 계산하여라.



### 문제 조건

* 풀이 시간 : 60분
* 시간 제한 : 1초
* 메모리 제한 : 128MB
* 입력 조건
  * 첫째 주에 도시의 개수 N, 통로의 개수 M, 메시지를 보내는 도시 C가 주어진다. (1 <= M <= 30,000, 1 <= M <= 200,000, 1 <= C <= N)
  * 둘째 줄부터 M + 1번째 줄에 걸쳐서 통로에 대한 정보 X, Y, Z 가 주어진다. 이는 특정 도시 X에서 다른 특정 도시 Y로 이어지는 통로가 있으며, 메세지가 전달되는 시간이 Z라는 의미이다. (1 <= X, Y <= N, 1 <= Z <= 1,000)
* 출력 조건
  * 첫째 줄에 도시 C에서 보낸 메시지를 받는 도시의 총 개수와 총 걸리는 시간을 공백으로 구분하여 출력



### 문제 해결 아이디어

* 최단 거리 문제
* 우선 순위 큐를 활용한 다익스트라 알고리즘 구현



### 답안 예시

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수, 시작 노드를 입력받기
n, m, start = map(int, input().split())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    x, y, z = map(int, input().split())
    # X번 노드에서 Y번 노드로 가는 비용이 Z라는 의미
    graph[x].append((y, z))

def dijkstra(start):
   q = []
   # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
   heapq.heappush(q, (0, start))
   distance[start] = 0
   while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보를 꺼내기
        dist, now = heapq.heappop(q)
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

# 도달할 수 있는 노드의 개수
count = 0
# 도달할 수 있는 노드 중에서, 가장 멀리 있는 노드와의 최단 거리
max_distance = 0
for d in distance:
    # 도달할 수 있는 노드인 경우
    if d != 1e9:
        count += 1
        max_distance = max(max_distance, d)

# 시작 노드는 제외해야 하므로 count - 1을 출력
print(count - 1, max_distance)
```

* 위의 다익스트라 알고리즘과 같다.



## <문제> 미래 도시

### 문제 설명

> 1번부터 N번까지의 회사가 있는데 특정 회사끼리는 서로 도로를 통해 연결되어 있다. 방문 판매원 A는 현재 1번 회사에 위치해 있으며, X번 회사에 방문해 물건을 판매하고자 한다.
>
> 미래 도시에서 특정 회사에 도착하기 위한 방법은 회사끼리 연결되어 있는 도로를 이용하는 방법이 유일하다. 또한 연결된 2개의 회사는 양방향으로 이동할 수 있다. 공중 미래 도시에서 특정 회사와 다른 회사가 도로로 연결 되어 있다면, 정확히 1만큼의 시간으로 이동할 수 있다.
>
> 방문 판매원 A는 소개팅에도 참석하고자 한다. 소개팅의 상대는 K번 회사에 존재한다. 방문 판매원 A는 X번 회사에 가서 물건을 판매하기 전에 먼저 소개팅 회사에 찾아가서 함께 커피를 마실 예정이다. 따라서, 1번 회사에서 출발하여 K번 회사를 방문한 뒤에 X번 회사로 가는 것이 목표다.
>
> 이때의 최소 시간을 구하여라



### 문제 조건

* 풀이 시간 : 40분
* 시간 제한 : 1초
* 메모리 제한 : 128MB
* 입력 조건
  * 첫째 줄에 전체 회사의 개수 N과 경로의 개수 M이 공백으로 구분되어 차례대로 주어진다. (1 <= N,M <= 100)
  * 둘째 줄부터 M + 1번째 줄에는 연결된 두 회사의 번호가 공백으로 구분되어 주어진다.
  * M + 2번쨰 줄에는 X와 K가 공백으로 구분되어 차례대로 주어진다. (1 <= K <= 100)
* 출력 조건
  * 첫째 줄에 방문 판매원 A가 K번 회사를 거쳐 X번 회사로 가는 최소 이동 시간을 출력하낟.
  * 도달 할 수 없다면 -1 출력



### 문제 해결 아이디어

* 최단 거리 알고리즘으로 해결
* N이 작은 편이므로 플로이드 워셜 알고리즘 이용



### 답안 예시

```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n, m = map(int, input().split())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A와 B가 서로에게 가는 비용은 1이라고 설정
    a, b = map(int, input().split())
    graph[a][b] = 1
    graph[b][a] = 1

# 거쳐 갈 노드 X와 최종 목적지 노드 K를 입력받기
x, k = map(int, input().split())

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
distance = graph[1][k] + graph[k][x]

# 도달할 수 없는 경우, -1을 출력
if distance >= 1e9:
    print("-1")
# 도달할 수 있다면, 최단 거리를 출력
else:
    print(distance)
```

