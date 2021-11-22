# Big O

**본 내용은 노마드 코더님의 강의를 토대로 작성하였습니다.**



## 1. 알고리즘 속도란

* 완료까지 걸리는 절차의 수로 결정
* 같은 작업을 수행할 때 적은 절차로 해결하는 알고리즘이 효율적인 알고리즘



## 2. Big O

* 알고리즘의 속도를 표현하는 방법
* input에 따라서 얼마의 절차가 필요한지를 표현
* 시간복잡도를 빠르게 설명
* 함수의 디테일은 관련 없음
  * 상수를 신경쓰지 않음




### Linear Search

* N개면 N개의 절차가 필요
* **O(N)** 시간 복잡도를 가짐



### O(1)

* input에 상관없이 동일한 수의 절차로 끝낼 수 있는 경우
  * **O(1)의 시간 복잡도를 가짐**
  * **input에 상관이 없이 200개의 절차로 끝내는 경우에도 O(1)의 시간 복잡도를 가짐**
* 항상 선호되는 알고리즘

```python
# input이 아무리 많아도 끝내는 절차는 하나
# 상수 시간
# O(1)
def print_first(arr):
  print(arr[0])
```



### O(N)

* input이 증가하는 만큼 절차수도 선형적으로 증가
  * **O(N)의 시간 복잡도를 가짐**

```python
# input의 수대로 절차수가 그만큼 필요
# O(N)
def print_all(arr):
  for n in arr:
    print(n)
```



### Quadratic Time(2차 시간)

* Nested Loops(중첩 반복)이 있을 때 발생
  * **O(N^2)**

```python
# 아래 함수는 배열의 각 아이템에 대하여 루프를 반복하여 실행
def print_twice(arr):
  for n in arr:
    for x in arr:
      print(x, n)
```



### Logarithmic Time(로그 시간)

* 이진 탐색의 경우의 시간복잡도
  * input이 2배로 커져도 검색을 하기 위한 절차는 1개만 증가
* **O(log N)**
* 선형 시간보다는 빠르고 상수 시간보다는 느림

# Reference

[[노마드코더] 개발자라면 이제는 알아야하는 Big O 설명해드림. 10분컷.](https://www.youtube.com/watch?v=BEVnxbxBqi8&list=PL7jH19IHhOLMdHvl3KBfFI70r9P0lkJwL&index=4)

