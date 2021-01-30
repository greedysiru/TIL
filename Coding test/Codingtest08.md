# [동빈나]이코테 2021 강의 몰아보기(8) (2021.1.6)



본 내용은 해당 [강의](https://www.youtube.com/watch?v=94RC-DsGMLo&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=5) 토대로 작성



# 이진 탐색

## 1. 이진 탐색 개요

* 순차 탐색 : 리스트 안에 있는 특정한 **데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인**
* 이진 탐색 : 정렬되어 있는 리스트에서 **탐색 범위를 절반씩 좁혀가며 데이터를 탐색**하는 방법
  * 시작점, 끝점, 중간점을 이용하여 탐색 범위 설정



## 2. 이진 탐색의 시간 복잡도

* 연산 횟수는 **log<sub>2</sub>N에 비례**
* 시간 복잡도는 **O(logN)**보장



## 3. 이진 탐색 소스코드 : 재귀적 구현

```python
def binary_search(array, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    elif array[mid] > target:
        return binary_search(array, target, start, mid - 1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else:
        return binary_search(array, target, mid + 1, end)

# n(원소의 개수)과 target(찾고자 하는 값)을 입력 받기
n, target = list(map(int, input().split()))
# 전체 원소 입력 받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)
```



## 4. 이진 탐색 소스 코드 : 반복문 구현

```python
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # 찾은 경우 중간점 인덱스 반환
        if array[mid] == target:
            return mid
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid - 1
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid + 1
    return None

# n(원소의 개수)과 target(찾고자 하는 값)을 입력 받기
n, target = list(map(int, input().split()))
# 전체 원소 입력 받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)
```



## 5. 파이썬 이진 탐색 라이브러리

* bisect_left(a, x) : 정렬된 순서를 유지, 배열 a에 x를 삽입할 가장 왼쪽 인덱스 반환
* bisect_right(a, x) : 정렬된 순서를 유지, 배열 a에 x를 삽입할 가장 오른쪽 인덱스 반환

```python
from bisect import bisect_left, bisect_right

a = [1, 2, 4, 4, 8]
x = 4

print(bisect_left(a, x))          # 2 출력
print(bisect_right(a, x))         # 4 출력
```



## 6. 값이 특정 범위에 속하는 데이터 개수 구하기

```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 배열 선언
a = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9]

# 값이 4인 데이터 개수 출력
print(count_by_range(a, 4, 4))

# 값이 [-1, 3] 범위에 있는 데이터 개수 출력
print(count_by_range(a, -1, 3))
```



## 7. 파라메트릭 서치(Parametric Search)

* 최적화 문제를 결정 문제(예 또는 아니오)로 바꾸어 해결하는 기법
  * 조건의 값을 빠르게 찾는 최적화 문제
* 일반적으로 코딩 테스트에서는 **이진 탐색으로 해결 가능**



## 8. 이진 탐색 기초 문제 풀이

## <문제> 떡볶이 떡 만들기

### 문제 설명

> 떡볶이를 만들기 위해 떡을 만든다. 절단기에 높이(H)를 지정하면, 줄지어진 떡을 한 번에 절단한다. 높이가 H보다 긴 떡은 H위의 부분이 잘리고 낮은 떡은 잘리지 않는다. 잘려간 부분은 손님에게 줄 수 있다.
>
> 손님이 왔을 때, 요청한 길이가 M일 때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하여라.



### 문제 조건

* 풀이 시간 : 40분

* 시간 제한 : 2초

* 메모리 제한 : 128MB

* 입력 조건 :
  * 첫째 줄에 떡의 개수 N과 요청한 떡의 길이 M이 주어진다.( 1 <= N <= 1,000,000, 1 <= M <= 2,000,000,000)
  * 둘째 줄에 떡의 개별 높이가 주어진다. 떡 높이의 총합은 항상 M 이상이므로, 필요한 양만큼 떡을 사갈 수 있다. 높이는 10억보다 작거나, 같은 양의 정수 또는 0 이다.
* 출력 조건 : 
  * 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력



### 문제 해결 아이디어

* 적절한 높이를 찾을 때까지 이진 탐색을 수행하여 높이 H를 반복하여 조정
* 조건의 만족 여부에 따라 탐색 범위를 좁혀서 탐색
* 큰 탐색 범위를 보면 가장 먼저 **이진 탐색**을 떠올리기
* 중간점의 값은 시간이 지날수록 **최적화 된 값**



### 답안 예시

```python
# 떡의 개수(N)와 요청한 떡의 길이(M)을 입력
n, m = list(map(int, input().split(' ')))
# 각 떡의 개별 높이 정보를 입력
array =list(map(int, input().split()))

# 이진 탐색을 위한 시작점과 끝점 설정
start = 0
end = max(array)

# 이진 탐색 수행 (반복적)
result = 0
while(start <= end):
    total = 0
    mid = (start + end) // 2
    for x in array:
        # 잘랐을 때의 떡의 양 계산
        if x > mid:
            total += x - mid
    # 떡의 양이 부족한 경우 더 많이 자르기 (왼쪽 부분 탐색)
    if total < m:
        end = mid - 1
    # 떡의 양이 충분한 경우 덜 자르기 (오른쪽 부분 탐색)
    else:
        result = mid # 최대한 덜 잘랐을 때가 정답이므로, 여기에서 result에 기록
        start = mid + 1
      
# 정답 출력
print(result)
```



## <문제> 정렬된 배열에서 특정 수의 개수 구하기

### 문제 설명

>  N개의 원소를 포함하고 있는 수열이 오름차순으로 정렬되어 있다. 이 수열에서 x가 등장하는 횟수를 계산하여라
>
> 시간 복잡도 **O(logN)**으로 알고리즘을 설계할 것



### 문제 조건

* 입력 조건 : 
  * 첫째 줄에 N과 x가 정수 형태로 공백으록 구분되어 입력된다. (1 <= N <= 1,000,000),(-10<sup>9</sup> <= x <= 10<sup>9</sup>)
  * 둘째 줄에 N개의 원소가 정수 형태로 공백으로 구분되어 입력 (-10<sup>9</sup><= 각 원소의 값 <= 10 <sup>9</sup>)
* 출력 조건 :
  * 수열의 원소 중에서 값이 x인 원소의 개수를 출력. 단, 값이 x인 원소가 하나도 없다면 -1을 출력.



### 문제 해결 아이디어

* 시간 복잡도 **O(logN)**으로 동작하는 알고리즘
  * 데이터가 정렬되어 있고 빠르게 수행하여야 하므로 **이진 탐색 수행**
* 특정 값이 등장하는 첫 번째 위치와 마지막 위치를 찾아 위치 차이를 계산하고 문제 해결 가능



### 답안 예시

```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

n, x = map(int, input().split()) # 데이터의 개수 N, 찾고자하는 값 x 입력받기
array = list(map(int, input().split())) # 전체 데이터 입력받기

# 값이 [x, x] 범위에 있는 데이터의 개수 계산
count = count_by_range(array, x, x)

# 값이 x인 원소가 존재하지 않는다면
if count == 0:
    print(-1)
# 값이 x인 원소가 존재한다면
else:
    print(count)
```