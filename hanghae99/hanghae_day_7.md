# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (3) (2021.3.7)



# 01. Array vs. LinkedList

| 경우             | Array                                   | LinkedList                   |
| ---------------- | --------------------------------------- | ---------------------------- |
| 특정 원소 조회   | O(1)                                    | O(N)                         |
| 중간에 삽입 삭제 | O(N)                                    | O(1)                         |
| 데이터 추가      | 데이터 추가시 새로운 메모리 공간을 할당 | 맨 뒤의 노드만 동적으로 추가 |
| 정리             | 데이터에 접근하는 경우가 빈번한 경우    | 삽입과 삭제가 빈번한 경우    |



# 02. 클래스

* 클래스: 분류, 집합, 속성과 기능을 가진 객체를 총칭하는 개념
* 객체: 세상에 존재하는 유일무이한 사물

> 클래스가 동물이면, 객체는 강아지 또는 고양이가 될 수 있다.



## 클래스 만들기

* 객체를 생성할 때 데이터를 넣어주거나, 내부적으로 원하는 행동을 실행하게 할 수 있다.
* **self**를 사용해서 객체에 데이터를 쌓을 수 있다.
* **메소드(method)**: 클래스 내부의 함수

```python
class Cat:
    def __init__(self, param_name): # __init__ 생성자 함수 이름(고정)
        print("hello", self)
        self.name = param_name # 해당 객체의 name 변수에 저장
    
    def talk(self):
        print(self.name ,"야옹")
        
cat_1 = Cat("siru") # hello __main
print(cat_1.name) # siru
cat_1.talk() # siru 야옹
```



# 03. 링크드 리스트 구현 예시

* 클래스를 이용하여 링크드 리스트를 구현할 수 있다.

```python
class LinkedList:
    def __init__(self, value):
        self.head = Node(value) # head에 시작하는 Node 연결
        
    def append(self, value): # LinkedList 가장 끝에 있는 노드에 새로운 노드 연결
        cur = self.head
        while = cur.next is not None: # cur 다음이 끝에 갈 때까지 이동
            cur = cur.next
        cur.next = Node(value)
        
    def print_all(self): # LinkedList의 모든 원소 출력하기
       cur = self.head
        while = cur.next is not None: # cur 다음이 끝에 갈 때까지 이동
            print(cur.data)
            cur = cur.next
            
    def get_node(self, index): # LinkedList의 원소 찾기
          node = self.head
          count = 0
          while count < index:
              node = node.next
              count += 1
          return node
    
    def add_node(self, index, value): # LinkedList에 원소 추가하기
        new_node = Node(value) # 새로운 노드
        
        if index == 0:  # 0번째에 노드를 넣는 경우
            new_node.next = self.hdead
            self.head = new_node
            return
        
        node = self.get_node(index - 1) # 넣을 index의 -1인 index 접근
        next_node = node.next # 다음 노드
        node.next = new_node # 해당 index의 다음 노드에 새 노드 넣기
        new_node.next = next_node # 원래의 다음 노드는 새 다음 노드의 다음 노드가 된다.
        
        
    def delete_node(self, index): # 링크드 원소 삭제
        if index == 0:
            self.head = self.head.next
            return
        node = self.get_node(index - 1)
        node.next = node.next.next
```



# 04. 이진 탐색

* **범위의 절반을 나누며 탐색하는 방식**
* 최솟값과 최댓값, 시돗값을 정의
  * **시돗값은 절반**
* 시돗값이 찾을 값보다 작다면 최솟값에 **시돗값 +1 대입**
* 시돗값이 찾을 값보다 크다면 최댓값에 **시돗값 -1 대입**
* 이에 맞춰 **시돗값을 최신화**
* **이를 최솟값 <= 최댓값 까지 반복**
* **시간 복잡도 O(log n)**



## 예시

```python
# 이진 탐색 함수
def binary_search(target, array):
    start = 0
    end = len(array) - 1
    mid = (start + end) // 2 # 소수 방지
    while start <= end:
        if array[mid] == target: # 찾은 경우
            return True
        elif array[mid] < target:
            start = mid + 1
        elif array[mid] > target:
            end = mid - 1
        mid = (start + end) // 2
    return False
```