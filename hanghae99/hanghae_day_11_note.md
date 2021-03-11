# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (8) (2021.3.11)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**

# 1. 트리

* 뿌리와 가지로 구성되어 거꾸로 세워놓은 나무처럼 보이는 계층형 비선형 자료 구조
* 비선형구조: 표현에 초점을 맞춘 자료구조
  * cf) 선형구조: 자료를 저장하고 꺼내느 것에 초점이 맞춰져 있다.



## 1.1 용어 정리

* **Node**: 트리에서 데이터를 저장하는 기본 요소
* **Root Node**: 트리 맨 위에 있는 노드
* **Level**: 최상위 노드를 Level 0으로 하였을 때, 하위 Branch로 연결된 노드의 깊이를 나타냄
* **Child Node**: 어떤 노드의 하위 레벨에 연결된 노드
* **Leaf Node**: Child Node가 하나도 없는 노드
* **Sibling**: 동일한 Parent Node를 가진 노드
* **Depth**: 트리에서 Node가 가질 수 있는 최대 Level



## 1.2 이진 트리

* Binary Tree
* 각 노드가 **최대 두 개의 자식**을 가진다.
  * 자식노드가 0, 1, 2개
* 이진트리의 높이는 최대 **O(log(N))**



## 1.3 완전 이진 트리

* Complete Binary Tree
* 노드를 삽입할 때 최하단 왼쪽 노드부터 차례대로 삽입



## 1.4 완전 이진트리를 배열로 표현하기

* 트리 구현시 0번째 인덱스는 사용하지 않는다.

> ​                          **8**
>
> ​           **6                           3**
>
> **4                  2            5**

```python
binary_Tree = [None, 8, 6, 3, 4, 2, 5]
# 1. 현재 인덱스 * 2 -> 왼쪽 자식의 인덱스
# 2. 현재 인덱스 * 2 + 1 -> 오른쪽 자식의 인덱스
# 3. 현재 인덱스 // 2 -> 부모 인덱스
```



# 2. 힙

* 최대값과 최소값을 빠르게 찾기 위해 고안된 완전 이진 트리(Complete Binary Tree)
* 최대의 값들이 필요한 연산이 있을 때 사용
* 항상 큰 값이 상위 레벨, 작은 값이 하위 레벨에 있는 자료구조
* Max heap: 최댓값이 맨 위인 힙
* Min heap: 최솟값이 맨 아래인 힙
* **부모노드 > 자식노드**

> ​                  **8**
>
> ​           **6              3**
>
> **4                2                 1**

## 맥스힙에 원소 추가, 제거

```python
class MaxHeap:
    def __init__(self):
        self.items = [None]

    def insert(self, value):
        # 값 추가하기
        self.items.append(value)
        # 현재 인덱스
        cur_index = len(self.items) - 1
        # 현재 인덱스가 1과 같으면 루트노드이므로 그 전까지 실행
        while cur_index > 1:
            # 부모인덱스는 현재 인덱스의 //2
            parent_index = cur_index // 2
            # 부모노드가 현재 노드보다 작으면 스와핑
            if self.items[parent_index] < value:
                self.items[parent_index], self.items[cur_index] = (
                    self.items[cur_index],
                    self.items[parent_index],
                )
                # 현재 인덱스는 부모노드의 인덱스 값이므로 바꾼다.
                cur_index = parent_index
            else:
                break
        return

    def delete(self):
        # 루트 노드와 맨 끝 노드 바꾸기
        self.items[1], self.items[-1] = self.items[-1], self.items[1]
        # 맨 끝 노드 삭제
        delete_node = self.items.pop()
        # 현재 인덱스
        cur_index = 1
        # 마지막 인덱스
        end_index = len(self.items) - 1
        # 마지막 자식 노드까지 확인하기
        while cur_index <= end_index:
            # 왼쪽 자식 인덱스
            left_index = cur_index * 2
            # 오른쪽 자식 인덱스
            right_index = (cur_index * 2) + 1
            # 둘 중 큰 자식 인덱스
            max_index = cur_index
            # 왼쪽 자식이 큰 경우, 인덱스 번호가 넘지 않을 때
            if (
                left_index <= end_index
                and self.items[left_index] > self.items[right_index]
            ):
                max_index = left_index
            # 오른쪽 자식이 큰 경우
            if (
                left_index <= end_index
                and self.items[right_index] > self.items[left_index]
            ):
                max_index = right_index
            # 더 이상 큰 자식 노드가 없으면 break
            if max_index == cur_index:
                break

            # 큰 자식노드와 스와핑
            self.items[cur_index], self.items[max_index] = (
                self.items[max_index],
                self.items[cur_index],
            )
            # 인덱스 최신화
            cur_index = max_index
        # 삭제된 노드 리턴
        return delete_node

max_heap = MaxHeap()
max_heap.insert(8)
max_heap.insert(7)
max_heap.insert(6)
max_heap.insert(2)
max_heap.insert(5)
max_heap.insert(4)
print(max_heap.items)
print(max_heap.delete())
print(max_heap.items)
```





# 3. 그래프

* 연결되어 있는 정점과 정점간의 관계를 표현할 수 있는 자료구조
* **연결 관계**에 초점을 맞춘다.
* 유방향 그래프(Directed Graph): 방향이 있는 간선을 가진다. 간선은 단방향 관계를 나타내고 한 방향으로만 진행
* 무방향 그래프(Undirected Graph): 방향이 없는 간선을 가진다.



### 표현 방법

* 인접 행렬(Adjacency Matrix): 2차원 배열로 그래프의 연결 관계를 표현

```python
graph = [
    [False, True, False, False],
    [True, False, True, False],
    [False, True, False, True],
    [False, False, True, False]
]
```



* 인접 리스트(Adjacnecy List): 링크드 리스트로 그래프의 연결 관계를 표현

```python
graph = {
    0: [1],
    1: [0, 2]
    2: [1, 3]
    3: [2]
}
```



# 4. DFS & BFS

* 자료의 검색, 트리나 그래프를 탐색하는 방법
* **한 노드를 시작으로 인접한 다른 노드를 재귀적으로 탐색해가고 끝가지 탐색하면 다시 위로 와서 다음을 탐색**
* 모든 경우의 수를 **전부 탐색해야 하는 경우**
* DFS: 끝까지 파고들기
  * 공간을 적게쓴다.
  * 최단 경로를 탐색하기 쉽지 않다.
* BFS: 갈라진 모든 경우의 수 탐색하기
  * 최단 경로를 쉽게 찾는다.
  * 공간을 많이 쓴다.
  * 시간이 오래 걸린다.



## 4.1 DFS 구현해보기

* Depth First Search
* 갈 수 있는 만큼 계속 탐색하다가 갈 수 없게 되면 다른 방향으로 다시 탐색하는 구조

> **노드를 방문하고 깊이 우선으로 인접한 노드를 방문**
>
> **도 그 노드를 방문해서 깊이 우선으로 인접한 노드를 방문**
>
> **만약 끝에 도달하면 리턴**

* 재귀함수로 구현한다.

> **루트 노드부터 시작**
>
> **현재 방문한 노드를  visited에 추가**
>
> **현재 방문한 노드와 인접한 노드 중 방문하지 않은 노드에 방문**
>
> **2부터 반복**



### DFS 구현

```python
graph = {
    1: [2, 5, 9],
    2: [1, 3],
    3: [2, 4],
    4: [3],
    5: [1, 6, 8],
    6: [5, 7],
    7: [6],
    8: [5],
    9: [1, 10],
    10: [9],
}
visited = []

def dfs_recursion(adjacent_graph, cur_node, visited_array):
    # 방문한 노드 체크
    visited_array.append(cur_node)
    # 인접 노드에서 미방문 노드 찾기
    for x in adjacent_graph[cur_node]:
        # 방문 안했을 경우 재귀함수 호출
        if x not in visited:
            dfs_recursion(adjacent_graph, x, visited_array)

    return

dfs_recursion(graph, 1 visited)
print(visited)                 # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 출력
```



### DFS 스택 구현

> **루트 노드를 스택에 넣는다.**
>
> **현재 스택의 노드를 빼서 visited에 추가**
>
> **현재 방문한 노드와 인접한 노드 중 방문하지 않은 노드를 스택에 추가**
>
> **두 번째 단계부터 반복**
>
> **스택이 비면 탐색 종료**

```python
graph = {
    1: [2, 5, 9],
    2: [1, 3],
    3: [2, 4],
    4: [3],
    5: [1, 6, 8],
    6: [5, 7],
    7: [6],
    8: [5],
    9: [1, 10],
    10: [9],
}

def dfs_stack(adjacent_graph, start_node):
    # 스택
    stack = [start_node]
    # 방문한 노드
    visited = []
    # 스택이 빌 때까지
    while stack:
        # 마지막에 들어온 스택의 원소 빼기
        current_node = stack.pop()
        # 방문한 리스트에 넣기
        visited.append(current_node)
        # 인접 노드 방문하기
        for x in adjacent_graph[current_node]:
            # 방문하지 않은 노드 스택에 추가
            if x not in visited:
                stack.append(x)
    return visited

print(dfs_stack(graph, 1))
```



## 4.2 BFS 구현해보기

* 현재 인접한 노드 먼저 방문

> **루트 노드를 큐에 넣는다.**
>
> **현재 큐의 노드를 빼서 visited에 추가한다.**
>
> **현재 방문한 노드와 인접한 노드 중 방문하지 않은 노드를 큐에 추가한다.**
>
> **두 번째 부터 반복**
>
> **큐가 다 비면 탐색 종료**

```python
graph = {
    1: [2, 3, 4],
    2: [1, 5],
    3: [1, 6, 7],
    4: [1, 8],
    5: [2, 9],
    6: [3, 10],
    7: [3],
    8: [4],
    9: [5],
    10: [6],
}

def bfs_queue(adj_graph, start_node):
    queue = []
    # 현재 노드 큐에 넣기
    queue.append(start_node)
    # 방문한 노드
    visited = []
    # 큐가 빌 때까지 반복
    while queue:
        # 현재 노드
        cur_node = queue.pop(0)
        # 방문 체크
        visited.append(cur_node)

        # 현재노드의 인접 노드
        for x in adj_graph[cur_node]:
            # 방문하지 않은 경우 추가하기
            if x not in visited:
                queue.append(x)

    return visited

print(bfs_queue(graph, 1))

```



# 5. Dynamic Programming

## 5.1 재귀함수로 피보나치 수열 구하기

```python
input = 20

def fibo_recursion(n):
    if n == 1 or n == 2:
        return 1
    return fibo_recursion(n - 1) + fibo_recursion(n - 2)

print(fibo_recursion(input))  # 6765
```

* **단점**: 연산이 오래걸린다.



## 5.2 동적 계획법

* 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법
  * 하위문제의 결과를 기록하고 그것을 이용한다.
* **메모이제이션(Momoization)**: 결과를 기록 하는 것
* **겹치는 문제(Overlapping Subporblem)**: 문제를 쪼갤 수 있는 구조



### 피보나치 수열 - 동적 계획법

* 메모용 데이터에 피보나치 수열의 각 결과를 기록하과 그 값이 사용될 경우 즉시 반환

```python
input = 50

memo = {1: 1, 2: 1}

def fibo_dynamic_programming(n, fibo_memo):

    # n이 있는 경우
    if n in fibo_memo:
        return fibo_memo[n]

    # 없는 경우
    nth_fibo = fibo_dynamic_programming(n - 1, fibo_memo) + fibo_dynamic_programming(
        n - 2, fibo_memo
    )
    fibo_memo[n] = nth_fibo

    return nth_fibo

print(fibo_dynamic_programming(input, memo))
```

