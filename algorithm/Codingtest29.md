# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (10)(2021.1.31)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 마구간 정하기(결정알고리즘)

## 문제 해설

* 입력받은 마굿간을 **오름차순으로 정렬하기**

* **주어진 조건하에, 가장 가까운 두 말의 최대거리를 이분 검색으로 찾기**

  * 첫 번째 말은 무조건 첫 번째 마굿간에 넣기

  

## 문제 풀이

```python
def Count(mid):
    cnt = 1; # 카운트
    h = a[0]; # 말을 놓은 곳
    for i in range(1, n):
        if a[i] - h >= mid:
            cnt += 1; # 말 배치
            h = a[i];
    return cnt;
    
n, c = map(int, input().split());
a = [];
for _ in range(n):
    x = int(input());
    a.append(x);
a.sort();
s = 1;
e = a[n - 1];
while s <= e:
    mid = (s + e) // 2;
    if Count(mid) >= c:
        ans = mid;
        s = mid + 1;
    else:
        e = mid - 1;
print(ans);
```



## 문제 답안

```python
def Count(len):
    cnt = 1;
    ep = Line[0];
    for i in range(1, n):
        if Line[i] - ep >= len: # 말 사이의 거리
            cnt += 1; # 말을 배치
            ep = Line[i];
    return cnt;

n, c = map(int, input().split());
Line=[];
for _ in range(n):
    tmp = int(input());
    Line.append(tmp);
Line.sort();
lt = 1;        # 시작점
rt = Line[n - 1]; # 끝점
while lt <= rt: # 이분탐색
    mid = (lt + rt) // 2;
    if count(mid) >= c: # 말의 마리수를 리턴
        res = mid;
        lt = mid + 1;
    else:
        rt = mid - 1;
print(res);
```



## 풀이와 답안 비교

결정 알고리즘은 전체적으로 이분검색을 사용하고 아이디어가 비슷한 것 같다. 문제만 봤을 때는 숨이 턱 막히는 것 같지만 ... 많이 풀어보면 금방 익숙해질 것 같다.



# 2. 회의실 배정(그리디)

## 문제 해설

* **그리디 알고리즘**
  * **문제를 풀어나가는 과정에서 각 단계에서 가장 좋은 것을 판별하는 것**
  * **정렬**을 한 다음에 차근차근 할 것
* **끝나는 시간** 기준으로 정렬하기



## 문제 답안

```python
n = int(input());
meeting = [];
for i in range(n):
    s, e = map(int, input().split());
    meeting.append((s, e)); # 튜플로 넣기
meeting.sort(key=lambda x : (x[1], x[0])) # key를 람다함수로 설정 1이 우선순위를 가지도록한다.
et = 0; # 회의의 끝나는 시간
cnt = 0;
for s, e in meeting:
    if s >= et: # 끝나는시간이 시작시간과 같거나 크다면
        et = e;
        cnt += 1;
print(cnt)
```

* 튜플 정렬은 앞을 기준으로 정렬하는 것이 기본이다.
  * 위처럼 람다함수로 설정할 것

## 풀이와 답안 비교

튜플로 풀어야하는 것을 모르고 2차원 리스트로 헤메다가 결국 강의를 보았다...