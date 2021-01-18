# [동빈나]이코테 2021 강의 몰아보기 (15)(2021.1.18)



**본 내용은 해당 [강의](https://www.youtube.com/watch?v=AjFlp951nz0&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=11) 토대로 작성**



# 자료구조: 우선순위 큐(Priority Queue)와 힙(Heap)



## 1. 우선순위 큐(Priority Queue)

* **우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조**
* **우선순위에 따라** 처리하고 싶을 때 사용

| 자료구조                    | 추출되는 데이터             |
| --------------------------- | --------------------------- |
| 스택(Stack)                 | 가장 나중에 삽입된 데이터   |
| 큐(Queue)                   | 가장 먼저 삽입된 데이터     |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |



### 우선순위 큐 구현 방법

1. 단순히 **리스트를 이용하여 구현**
2. **힙(Heap)을 이용**하여 구현

* 데이터의 개수가 N개일 때, 구현 방식에 따른 시간 복잡도

| 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| --------------------- | --------- | --------- |
| 리스트                | O(1)      | O(N)      |
| 힙(Heap)              | O(logN)   | O(logN)   |



## 2. 힙(Heap)의 특징

* 완전 이진 트리 자료구조의 일종

  * 항상 루트 노드(root node)를 제거

  * **최소 힙(min heap)**

    * 루트 노드가 가장 작은 값을 가진다.
    * 따라서, 가장 작은 데이터가 우선적으로 제거

  * **최대 힙(max heap)**

    * 루트 노드가 가장 큰 값을 가진다.
    * 따라서, 가장 큰 데이터가 우선적으로 제거

    

### 완전 이진 트리 (Complete Binary Tree)

* 루트(root) 노드부터 시작하여 왼쪽 자식 노드, 오른쪽 자식 노드 순서대로 데이터가 차례대로 삽입되는 트리(Tree)



### 최소 힙 구성 함수: Min-Heapify()

* (상향식) 부모 노드로 거슬러 올라가며, 부모보다 자신이 값이 더 작은 경우에 위치를 교체



### 힙에서 새로운 원소가 삽입될 때

* **O(logN)**의 시간 복잡도로 힙 성질 유지



### 힙에서 원소가 제거될 때

* **O(logN)**의 시간 복잡도로 힙 성질 유지
  * 가장 마지막 노드가 루트 노드의 위치에 오도록 한다.
  * 하향식으로 더 작은 노드로 Heapify()를 진행



### 구현 예제

```python
import sys                       # 우선순위 큐 라이브러리 활용
import heapq
input = sys.stdin.readline

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value) # min heap
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result                        # max heap 사용시 입력과 출력시 -1를 붙인다.

n = int(input())
arr = []

for i in range(n):
    arr.append(int(input()))

res = heapsort(arr)

for i in range(n):
    print(res[i])
```