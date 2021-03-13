# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (6) (2021.3.10)

# 01. 정렬

* 데이터를 순서대로 내열하는 방법



## 버블 정렬

```python
arr = list(map(int, input().split()))

def bubble_sort(arr):
    n = len(arr)
    for i in range(n): # n번 반복
        for j in range(n - i - 1): # 마지막 원소까지 가지 않아도 됨
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                
bubble_sort(arr)
print(arr)
```

* 2차 반복문이 나오고 array의 길이 만큼 반복하므로
* **O(N<sup>2</sup>)**



## 선택 정렬

* 매번 가장 작은 숫자를 n번째 앞자리에 바꾼다.

```python
arr = list(map(int, input().split()))


def selection_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        min_index = i
        for j in range(n - i):
            if arr[i + j] < arr[min_index]:
                # 최솟값 인덱스
                min_index = i + j
        arr[i], arr[min_index] = arr[min_index], arr[i]


selection_sort(arr)
print(arr)
```

* **O(N<sup>2</sup>)**



## 삽입 정렬

* 하나씩 올바른 위치에 삽입

```python
arr = list(map(int, input().split()))

def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n): # 0 번째 인덱스는 정렬된 상태
        for j in range(i):
            if arr[i - j - 1] > arr[i - j]:
                arr[i - j - 1], arr[i - j] = arr[i - j], arr[i - j - 1]
            else:
                break


insertion_sort(arr)
print(arr)
```

* **O(N<sup>2</sup>)**
* 최선의 경우 N만큼의 시간 복잡도



## 병합 정렬

* 서로 다른 배열을 합쳐가면서 정렬하는 방법
* 분할 정복: 문제를 작은 2개의 문제를 분리하고 각각을 해결한 다음 결과를 모아서 원래의 문제를 해결하는 전략
  * 배열을 1개까지 쪼개고 다시 기준을 가지고 병합을 한다면 전체 배열도 정렬될 것이다.

```python
arr = list(map(int, input().split()))

# 병합정렬
def merge_sort(arr):
    # 배열의 요소가 하나이면 중단
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left_arr = arr[:mid]
    right_arr = arr[mid:]
    # 재귀함수
    return merge(merge_sort(left_arr), merge_sort(right_arr))


def merge(arr1, arr2):
    # O(N) 시간 복잡도
    result = []
    arr1_index = 0
    arr2_index = 0
    # 각 배열의 값들을 하나씩 비교후 더 작은 값 새로운 배열에 추가
    while arr1_index < len(arr1) and arr2_index < len(arr2):
        if arr1[arr1_index] < arr2[arr2_index]:
            result.append(arr1[arr1_index])
            arr1_index += 1
        else:
            result.append(arr2[arr2_index])
            arr2_index += 1
    # 한 배열이 끝나고 난 후 남은 배열의 모든 값을 새로운 배열에 추가
    if arr1_index == len(arr1):
        while arr2_index < len(arr2):
            result.append(arr2[arr2_index])
            arr2_index += 1

    if arr2_index == len(arr2):
        while arr1_index < len(arr1):
            result.append(arr1[arr1_index])
            arr1_index += 1

    return result


print(merge_sort(arr))

```

* merge: while문이 각 배열의 길이만큼 반복하고 있다.
  * **시간 복잡도 O(N)**
* merge_sort: 모든 단계에서 N만큼 비교를 한다.
  * **시간 복잡도 O(NlogN)**



# 02. 스택

* Last In First Out

  * LIFO
  * 넣은 순서가 필요한 경우

* 제공하는 기능

  * push(data): 맨 앞에 데이터 넣기

  ```python
  def push(self, value):
      new_head = Node(value)
      new_head.next = self.head
      self.head = new_head
  ```

  

  * pop(): 맨 앞의 데이터 뽑기

  ```python
  def pop(self):
      if self.is_empty():
          return "Stack is empty!"
      delete_head = self.head
      self.head = self.head.next
      return delete_head
  ```

  

  * peek(): 맨 앞의 데이터 보기

  ```python
  def peek(self):
      if self.is_empty():
          return "Stack is empty!"
      return self.head.data
  ```

  

  * isEmpty(): 스택이 비었는지 안 비었는지 여부 반환해주기

  ```python
  def is_empty(self):
      return self.head is None
  ```



# 03. 큐

* First in First Out

  * FIFO
  * 순서대로 처리되어야 하는 일에 사용
  * 끝과 시작의 노드를 전부 가지고 있어야 한다.
  * self.head와 self.tail을 가지고 시작

* 제공하는 기능

  * enqueue(data): 맨 뒤에 데이터 추가하기

  ```python
  def enqueue(self, value):
      new_node =Node(value)
      if self.is_empty(): # 비어있는 경우
          self.head = new_node
          self.tail = new_node
          return
      self.tail.next = new_node
      self.tail = new_node
  ```

  

  * dequeue(): 맨 앞의 데이터 뽑기

  ```python
  def dequeue(self):
      if self.is_empty():
          return "Queue is empty!" # 비어있으면 에러
      delete_head = self.head # 제거할 데이터
      self.head = self.head.next
      return delete_head.data
  ```

  

  * peek(): 맨 앞의 데이터 보기

  ```python
  def is_empty(self):
      return self.list.head is None
  ```

  

  * isEmpty(): 큐가 비었는지 여부

