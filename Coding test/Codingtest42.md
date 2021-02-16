# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (23)(2021.2.16)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 최대 점수 구하기(DFS)

## 문제 해설

* 부분집합
* 문제를 푸는 경우, 안 푸는 경우로 나누기
* 최대 점수가 나오면 갱신

## 문제 풀이

```python
def DFS(score, time, s):
    global maxScore;
    if time > m: # 시간초과한 경우 중단
        return;
    else:
        if maxScore < score:
            maxScore = score;
        for i in range(s, n):
            DFS(score + p[i][0], time + p[i][1], i + 1); # 푼 경우
            DFS(score, time, i + 1); # 풀지 않은 경우

if __name__ == "__main__":
    n, m = map(int, input().split()); # 문제의 개수, 제한 시간
    p = [];
    for i in range(n):
        s, t = map(int, input().split());
        p.append((s, t)); # 튜플
    maxScore = 0; # 최대 점수
    p.sort(reverse = True); # 내림차순 정렬
    DFS(p[0][0], p[0][1], 1);
    print(maxScore);
```



## 문제 답안

```python
def DFS(L, sum, time): # 문제, 점수, 사용시간
    global res; # 글로벌 변수
    if time > m:
        return;
    if L == n: # 종료지점
        if sum > res:
            res = sum;
    else:
        DFS(L + 1, sum + pv[L], time + pt[L]); # 문제를 푸는 경우
        DFS(L + 1, sum, time); # 문제를 풀지 않는 경우    

if __name__ == "__main__":
    n, m = map(int, input().split()); # 문제의 개수, 제한 시간
    pv = list(); # 문제 점수
    pt = list(); # 문제 푸는 데 걸리는 시간
    for i in range(n):
        a, b = map(int, input().split()); # 점수와 시간 각각 입력
        pv.append(a);
        pt.append(b);
    res = -2147000000; # 최대점수
    DFS(0, 0, 0);
    print(res);
```



## 풀이와 답안 비교

잘 푼 것 같다. 처음에는 체크리스트를 이용해서 풀려고 했으나 일부 case가 풀리지 않아 조합을 구해서 풀었다.

내 코드는 문제의 점수, 푸는데 걸리는 시간을 하나의 리스트에 튜플로 받아서 DFS의 매개변수에 점수, 푼 시간, 상태 트리 가지의 수를 받아서 for문을 사용하여 최대 점수를 구해냈다. 시간을 단축시키기 위해서 튜플로 받은 자료를 내림차순 정리하였다.

답안의 코드는 문제의 점수와 걸리는 시간을 별도의 리스트에 받았고 문제를 푸는 경우와 안 푸는 경우를 각각 재귀함수 호출하여 최대 점수를 구해냈다.

* 내 풀이는 풀지 않은 경우가 고려되지 않아 추가했는데 마지막 케이스에서 시간초과가 나온다...

# 2. 휴가(DFS)

## 문제 해설

* 상담에 걸리는 일수를 고려해야 한다.
* 상담을 하지 않은 경우는 다음날로

## 문제 풀이

```python
def DFS(T, P): # 걸리는 일수, 이익
    global res; # 글로벌 변수
    if T > n: # 걸리는 일수가 초과한 경우
        return;
    else:
        if res < P: # 최댓값 구하기
            res = P;
        for i in range(T, n): # T부터 n -1 까지 탐색
                DFS(i + s[i][0], P + s[i][1]); # 해당 일에 상담을 한 경우
                DFS(i + 1, P); # 해당일에 상담을 하지 않은 경우
                        

if __name__ == "__main__":
    n = int(input());
    s = []; # 스케쥴 받는 리스트
    for _ in range(n):
        t, p = map(int, input().split());
        s.append((t, p));
    res = 0; # 답
    DFS(0, 0);
    print(res);
```



## 문제 답안

```python
def DFS(L, sum): # 일수, 이익
    global res;
    if L == n + 1:
        if sum > res:
            res = sum;
    else:
        if L + T[L] <= n + 1: # 상담한 경우
            DFS(L + T[L], sum + P[L]);
        DFS(L + 1, sum) # 상담하지 않은 경우

if __name__ == "__main__":
    n = int(input()); # 날짜
    T = list(); # 걸리는 일수
    P = list(); # 이익
    for i in range(n):
        a, b = map(int, input().split());
        T.append(a);
        P.append(b);
    res =- 2147000000 # 최대 이익
    T.insert(0, 0); # 인덱스 번호 == 날짜
    P.insert(0, 0);
    DFS(1, 0);
    print(res);
```



## 풀이와 답안 비교

상담한 경우와 상담하지 않는 경우를 분류하고 for문은 자제하자



# 3. 양팔저울(DFS)

## 문제 해설

* 추의 총합 - 측정가능한 무게의 가짓수 = 측정 불가능한 물의 무게 가짓수
* **상태 트리**
  * 양팔저울의 왼쪽에 추를 올리는 경우 ->  + 추 무게
  * 양팔저울에 오른쪽에 추를 올리는 경우 -> - 추 무게
  * 추를 올리지 않는 경우
  * **대칭인 경우** 무게의 합이 -음수 = 양수 이므로 음수인 경우는 체크하지 않아도 된다.



## 문제 답안

```python
def DFS(L, sum): # 레벨, 무게
    global res;
    if L == n: # 종료 지점
        if 0 < sum <= s: # 음수는 제외
            res.add(sum);
    else:
        DFS(L + 1, sum + G[L]); # 왼쪽에 놓는 경우
        DFS(L + 1, sum - G[L]); # 추를 오른쪽에 놓는 경우
        DFS(L + 1, sum) # 추를 놓지 않는 경우
        
if __name__ == "__main__":
    n = int(input());
    G = list(map(int, input().split()));
    s = sum(G);
    res = set(); # 중복을 제거하고 값을 추가하는 자료구조
    DFS(0, 0);
    print(s - len(res));
```

* 너무 복잡하게 생각해서 파국으로 치닫고 못 풀었다 ... ㅠ



# 4. 동전 바꿔주기(DFS)

## 문제 해설

* DFS(L, sum) : L은 레벨이면서 인덱스
* **상태 트리**
  * 각 동전의 개수만큼 탐색 ( 사용하는 경우 ~ 전부 다 사용하는 경우)



## 문제 답안

```python
def DFS(L, sum): # 레벨, 합계
    global cnt;
    if sum > T:
        return;
    if L == k: # 종료 지점
        if sum == T:
            cnt += 1;
    else:
        for i in range(cn[L] + 1): # 동전의 갯수
            DFS(L + 1, sum + (cv[L]) * i);

if __name__ == "__main__":
    T = int(input());
    k = int(input());
    cv = list(); # 동전 금액
    cn = list(); # 동전 개수
    for i in range(k):
        a, b = map(int, input().split());
        cv.append(a);
        cn.append(b);
    cnt = 0; # 카운트
    DFS(0, 0);
    print(cnt);
```

* for문의 range를 동전의 갯수에 맞춰서 탐색

