# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (14)(2021.2.7)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 공주구하기(큐)

## 문제 해설

* **큐 자료구조**
  * 선입선출(First In Frist Out) 
    * 스택의 반대
  * 먼저 들어간 것이 먼저 빠지게 된다.
  * **파이썬에서는 deque 자료구조**
    * **append, pop** : 뒤 쪽에서 넣거나 뺀다.
    * **appendleft, popleft** :앞쪽에서 넣거나 뺀다.
* 문제의 조건에 따라 **popleft, append 하는 경우**, **popleft만 하는 경우**를 구분하자.

## 문제 풀이

```python
from collections import deque
n, k = map(int, input().split());
p = deque([]) # 왕자들을 담을 리스트

for x in range(1, n + 1): # 왕자들 리스트에 넣기
    p.append(x);

while len(p) != 1: # 왕자 찾기
    for i in range(k): 
        if i != k-1:
            p.append(p.popleft());
        else:
            p.popleft();        

print(p[0]);
```



## 문제 답안

```python
from collections import deque
n, k = map(int, input().split());
dq = list(range(1, n+1)); # 받은 데이터 리스트화
dq = deque(dq);
while dq: # 빌 때까지
    for _ in range(k - 1):
        cur = dq.popleft();
        dq.append(cur);
    dq.popleft() # 빠지는 경우
    if len(dq) == 1:
        print(dq[0]);
        dq.popleft(); # 반복문 종료
```



## 풀이와 답안 비교

리스트화할 때 for문 사용한 것 빼고는 잘 풀었다.