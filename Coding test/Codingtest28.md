# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (9)(2021.1.30)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 이분검색

## 문제 해설

* **이분검색**
  * 오름차순 정렬된 상황에서목표로하는 값을 찾을 때 리스트를 반으로 나눈 뒤에 검색한다.
  * 목표값보다 중간점이 작은경우 시작점을 중간점 +1에 두고 다시 검색
  * 목표값보다 중간점이 큰 경우 끝점을 중간점 -1에 두고 다시 검색
  * 목표값과 중간점이 같을 때까지 위를 반복한다.

## 문제 풀이

```python
n, m = map(int, input().split());
arr = list(map(int, input().split()));
s = 0; # 시작점
e = n; # 끝점


arr.sort(); # 오름차순 정렬

while s <= e: # 이분 탐색
    mid = (s + e) // 2; # 중간점
    if arr[mid] == m: # 목표값 찾은 경우 탐색 완료
        print(mid + 1);
        break;
    elif arr[mid] < m : # 중간점보다 목표값이 큰 경우
        s = mid + 1;
    elif arr[mid] > m : # 중간점보다 목표값이 작은 경우   
        e = mid - 1;
```



## 문제 답안

```python
n, m = map(int, input().split());
a = list(map(int, input().split()));
a.sort() # 오름차순 정렬
lt = 0;
rt = n - 1;
while lt < rt: # 이분탐색
    mid = (lt + rt) // 2
    if a[mid] == m:
        print(mid + 1);
        break
    elif a[mid] > m:
        rt = mid - 1;
    else:
        lt = mid + 1;
```



## 풀이와 답안 비교

잘 풀었는데 나는 끝 점을 n으로 두었는데도 답이 전부 잘 나왔다. 왜지 ....??????????????????



# 2. 랜선 자르기 (결정 알고리즘)

## 문제 해설

* 이분검색 : 특정 범위 내에 답이 있는 것을 알 수 있는 경우

  * 좋은 답을 좁히며 찾아간다.

  

## 문제 풀이

```python
import sys
sys.stdin = open("in1.txt", "rt")
k, n = map(int, input().split());
arr = [0]* k;
for i in range(k):
    arr[i] = int(input());

arr.sort(reverse=True); # 내림차순 정렬
s = 0; # 시작점
e = arr[0]; # 끝점

while s <= e: # 이진 탐색
    mid = (s + e) //2; # 중간점
    cnt = 0; # 카운트
    for x in arr: # 나눈 값을 카운트
        cnt += x // mid;
        print(mid)
    if cnt == n:       # 목표값을 찾으면 출력 후 중단
        print(mid);
        break
    elif cnt < n:
        e = mid - 1;
    elif cnt > n:
        s = mid + 1;
```



## 문제 답안

```python
def Count(len): # 개수 세는 함수
    cnt = 0;
    for x in Line:
        cnt += (x//len);
    return cnt;

k, n = map(int, input().split());
Line = [];
res = 0;
largest = 0; # 가장 긴 전선
for i in range(k):
    tmp=int(input());
    Line.appen(tmp);
    largest=max(largest, tmp);
    
lt = 1;
rt = largest
while lt <= rt: # 이분검색
    mid = (lt + rt)//2
    if Count(mid) >= n:
        res = mid
        lt = mid + 1;
    else:
        rt = mid - 1;

print(res)    
    
```



## 풀이와 답안 비교

내 코드는 3개의 케이스에서 답을 맞추지 못했다. 그 이유는, 최대의 해를 구하기 전에 카운트가 문제의 주어진 갯수를 만족하면 반복문을 끊어버리기 때문에 다 탐색을 마치기전에 끝나버렸기 때문이었다.



# 3. 뮤직비디오(결정알고리즘)

## 문제 해설

* 이분검색
  * **최소가 되는 용량을 구할 것**

## 문제 풀이

```python
def Count(mid): # 카운트 함수
    D = 0; # DVD
    cnt = 1; # DVD 카운트
    for x in song:
        if D + x < mid:
            D += x;
        else:
            cnt += 1;
            D = x;
    return cnt;

n, m = map(int, input().split());
song = list(map(int, input().split()));
s = song[0]; # 시작점
e = sum(song); # 끝점

while s <= e: # 이분탐색
    mid = (s + e) // 2;
    if Count(mid) <= m:
        e = mid - 1;
    elif Count(mid) > m:
        s = mid + 1;
print(mid);
```



## 문제 답안

```python
n, m = map(int, input().split());
Music = list(map(int, input().split()));

def Count(capacity): # 용량 체크 함수
      cnt = 1;
      sum = 0;
      for x in Music:
          if sum + x > capacity:
              cnt += 1
              sum = x;
          else:
              sum += x;
      return cnt;

maxx = max(Music);
lt = 1;
rt = sum(Music);
res = 0
while lt <= rt:  # 이분 검색
    mid = (lt + rt) // 2;
    if mid >= maxx and Count(mid) <= m: # 한곡은 들어가야 한다.
        res = mid;
        rt = mid - 1;
    else:
        lt = mid + 1;
print(res);
```



## 풀이와 답안 비교

내코드는 3번에서 결과 +1 더 나왔다. 원인 불명.... 시간 나면 자세히 찾아보자