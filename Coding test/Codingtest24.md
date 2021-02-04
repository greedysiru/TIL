# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (5)(2021.1.25)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. K번째 큰 수

## 문제 풀이

```python
n, k = map(int, input().split()); # n, k 입력받기
arr = list(map(int, input().split())); # arr에 카드값 받기
arr.sort(reverse=True); # 내림차순으로 정렬
sumArr = arr[0] + arr[1] + arr[k+1]; # K번째로 큰 수 구하기
print(sumArr);
```



## 문제 해설

* 중복된 값은 카운트하지 않는다.
* 내침차순 정렬을 한다.
* 중복을 제거하기 위해서 **set 자료구조**를 사용한다.



## 문제 답안

```python
n, k = map(int, input().split()); # n, k 입력받기
a = list(map(int, input().split())); # a에 배열로 카드캆 저장
res = set() # 중복 제거 자료구조
for i in range(n): # 세 개의 숫자를 뽑아 더하기 중복을 방지하며 추출한다.
    for j in range(i+1, n):
        for m in range(j+1, n):
            res.add(a[i] + a[j] + a[m]) # set자료구조는 add사용
res = list(res) # 정렬을 위한 리스트화
res.sort(reverse=True);
print(res[k-1]);
```



## 풀이와 답안 비교

지난번에 코드를 효율적으로 쓰자고 다짐했는데, 이번에는 총체적 난국이다. 우선, 중복을 삭제하는 자료구조인 set을 몰랐고 모든 합을 구하기 위해 for문을 사용하지 않았다. 내 코드로 기적적으로 예제의 답을 맞춰서 맞는 줄 알았는데, 강사님의 코드를 보고 다시 다른 케이스도 돌려보니까 틀렸었다...



# 2. [선수지식] 최솟값 구하기



```python
arr = [5, 3, 7, 9, 2, 5, 2, 6];
arrMin = float('inf') # 가장 큰 값(무한대)으로 초기화
for i in range(len(arr)):
    if arr[i] < arrMin:
        arrMin = arr[i];
        
print(arrMin);

-------------------------------------------------------

arr = [5, 3, 7, 9, 2, 5, 2, 6];
arrMin = arr[0] # 처음값을 대입
for i in range(1, len(arr)): # 1부터 시작
    if arr[i] < arrMin:
        arrMin = arr[i];
        
print(arrMin);

--------------------------------------------------------

arr = [5, 3, 7, 9, 2, 5, 2, 6];
arrMin = float('inf') # 가장 큰 값(무한대)으로 초기화
for x in arr: # x를 이용한 for문
    if x < arrMin:
        arrMin = x;
        
print(arrMin);
```

* 첫 번째 숫자의 경우에서 참이 되도록, 최솟값을 넣을 변수에 무한대로 초기화 한다.
* armin에 배열의 처음값을 두는 방법도 있다.



# 3. 대표값

## 문제 풀이

```python
n = int(input()); # n 입력 받기
score = list(map(int, input().split())); # 점수 리스트 형태로 저장
average = round((sum(score)/len(score))); # 평균 점수 구하기
```



## 문제 해설

* 평균은 첫째 자리에서 반올림

  * round는 round_half_even 방식이다.
  * 절반의 값을 가질 때 짝수 값으로 근사하는 방식 (4.5000 -> 4, 4.5111 -> 5)
  * round 함수가 아닌, 다른 방식을 사용할 것 

* **튜플과 enumerate 함수**를 사용하기

  

## 문제 답안

```python
n = int(input());
a = list(map(int, input().split()));
ave = int((sum(a)/n)+ 0.5); # 평균 구하기
min = 2147000000 # 정수형 데이터에서 가장 큰 값
for idx, x in enumerate(a): # 학생 번호와 점수 탐색 idx에는 index를 x에는 점수를 반환
    tmp = abs(x-ave) # 평균과 점수의 거리값
    if tmp < min: # 최소 거리를 대입하기
        min = tmp 
        score = x # 가까운 거리의 점수 대입하기
        res = idx + 1 # 학생 번호
    elif tmp == min: # 거리가 같은 경우
        if x > score: # 점수가 큰 것을 선택
            score = x;
            res = idx + 1;
print(ave, res);
```



## 풀이와 답안 비교

평균 점수 구하는 것까지는 작성할 수 있었으나, 평균과 가까운 점수들을 추리는 것에서 막혔었다. enumerate를 사용하여, index와 value를 각각 뽑아내서 최소 거리가 같은 점수 중에서 문제에서 제시한 우선순위대로 답을 도출해낼 수 있다는 것을 배웠다.



# 4. 정다면체

## 문제 풀이

```python
n, m = map(int, input().split()); # 입력 받기

arr = [0]*(m + n + 1); # 정다면체의 합의 개수만큼 값이 0인 배열 만들기
for i in range(1, n+1): # 배열의 인덱스 == 합, 카운트하기
    for j in range(1, m+1):
        arr[i + j] += 1;
maxCnt = 0;

for sum, cnt in enumerate(arr): # 최대 반복수 구하기
    if maxCnt < cnt:
        maxCnt = cnt;

for sum, cnt in enumerate(arr): # 최대 반복수가 value인 index 뽑아내기
    if maxCnt == cnt:
        print(sum, end=" ");
```



## 문제 해설

* 합계의 경우의 수만큼 길이를 가지는 배열을 생성한다.
* 생성한 리스트에서, 합계를 index number로 두고 value로 count한다.



## 문제 답안

```python
n, m = map(int, input().split());
cnt=[0]*(n + m + 3); # 리스트 넉넉하게 만들어 놓기
max = -2147000000 # 가장 작은 값으로 초기화
for i in range(1, n + 1): # 다면체의 합 구하기
    for j in range(1, m + 1):
        cnt[i + j] += 1; # 해당하는 index 카운트하기
for i in range(n + m+1): # 최대 반복수 구하기
    if cnt[i]>max:
        max = cnt[i]
for i in range(n + m+1): # 최대 반복수의 index(합계) 구하기
    if cnt[i] == max:
        print(i, end=' ');
```



## 풀이와 답안 비교

정상적으로 문제를 잘 풀었으나, 아직 비효율적이다. 굳이 enumerate를 사용할 필요가 없었다.

