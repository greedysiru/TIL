# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (22)(2021.2.15)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 조합 구하기(DFS)

* **매우 중요!**

## 문제 해설

* **매개변수를 두 개로 할 것**
  * D(L, s)
  * s : 가지가 뻗기 시작하는 번호




## 문제 답안

```python
def DFS(L, s):
    global cnt;
    if L == m:
        for j in range(L):
            print(res[j], end=" ");
        cnt +=1;
        print();
    else:
        for i in range(s, n + 1):
            res[L] = i;
            DFS(L + 1, i + 1);    

if __name__ == "__main__":
    n, m = map(int, input().split());
    res = [0] * (n + 1); # 조합을 넣을 리스트
    cnt = 0; # 카운트
    DFS(0, 1);
    print(cnt);
```

* DFS를 호출하는 곳에서 막혔다. s에 더하는 것이 아닌, **i에 더해야 적절한 상태트리가 만들어진다.**



# 2. 수들의 조합(DFS)

## 문제 해설

* 부분집합을 만들어낸다.
  * 각 부분집합의 합을 구하기
* DFS(L, s, sum) 
  * L: 레벨
  * s: for문이 시작하는 곳
  * sum: 합계

## 문제 풀이

```python
def DFS(L, s, sum): # 레벨, for문이 시작하는 곳, 합
    global cnt;
    if L == k: # 종료 지점
        if (sum % m) == 0: # 주어진 수의 배수인 경우
            cnt += 1;
        return;
    else:
        for i in range(s, n):
          DFS(L + 1, i + 1, sum + a[i]);


if __name__ == "__main__":
    n, k = map(int, input().split());
    a = list(map(int, input().split()));
    m = int(input());
    cnt = 0; # 카운트
    DFS(0, 0, 0);
    print(cnt);
```



## 문제 답안

```python
def DFS(L, s, sum):
    global cnt;
    if L == k:
        if sum % m == 0:
            cnt += 1;
    else:
        for i in range(s, n):
            DFS(L + 1, i + 1, sum + a[i]);

if __name__ == "__main__":
    n, k = map(int, input().split());
    a = list(map(int, input().split()));
    m = int(input());
    cnt = 0; # 카운트
    DFS(0, 0, 0);
    print(cnt);
```



## 풀이와 답안 비교

많이 참고하긴 했지만 잘 풀었다.



# 3. 라이브러리를 이용한 순열(수열 추측하기)

## 문제 해설

* 이전의 수열 추측하기 문제를 파이썬의 라이브러리를 사용하여 풀어본다. (21번 정리에 있음)



