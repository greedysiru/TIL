# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (21)(2021.2.14)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1 . 순열 구하기

## 문제 해설

* **체크리스트 만들기**
  * 중복 순열 방지
* **DFS함수 호출의 밑 지점 : 명령을 하고 난 후 적용한다.**



## 문제 풀이

```python
def DFS(L):
    global cnt; # 글로벌 변수
    if L == m: # 종료
        for i in range(m):
            print(a[i], end = " ");
        print();
        cnt += 1;
        return;
    else:
        for i in range(1, n + 1): # 순열 만들기
            if ch[i] == 0:
                ch[i] = 1;
                a[L] = i; 
                DFS(L + 1);
                ch[i] = 0;

if __name__ == "__main__":
    n, m = map(int, input().split());
    a = [0] * m;
    ch = [0] * (n + 1); # 중복 방지 체크리스트
    cnt = 0; # 카운트
    DFS(0);
    print(cnt);
```



## 문제 답안

```python
def DFS(L):
    global cnt;
    if L == m:
        for j in range(L):
            print(res[j], end =" ");
        print()
        cnt += 1;
    else:
        for i in range(1, n + 1):
            if ch[i] == 0:
                ch[i] = 1;
                res[L] = i;
                DFS(L + 1);
                ch[i] = 0; # 되돌아온 시점에서 다시 0(출력 후)


if __name__ == "__main__":
    n, m = map(int, input().split());
    res = [0] * n;
    ch = [0] * (n + 1); # 중복 방지 체크리스트
    cnt = 0; # 카운트
    DFS(0);
    print(cnt);
```



## 풀이와 답안 비교

체크리스트를 다시 0으로 바꾸는 것에서 많이 헷갈렸다.

**DFS호출 후, 체크리스트를 0으로 되돌려줌에따라, 정상적으로 적용되었다.**



# 2.  순열 추측하기

## 문제 해설

* 주어진 조건을 만족할 수 있는 순열을 찾는다.

  * 가능한 순열 중 만족하는 것을 찾기

* 시간복잡도를 낮출 수 있는 방법 찾기

* **규칙 찾기**

  * 구한 순열이 각각 몇 번 더해지는지?

* **이항계수**

  * 별도의 리스트 만들 것

  

## 문제 풀이

```python
import sys
def DFS(L):
    global totalSum;
    if L == n:
        for j in range(n):
            totalSum += p[j] * b[j];
        if totalSum == f:
            print(p);
            sys.exit(0);
        else:
            totalSum = 0;
        return;
    else:
        for i in range(1, n + 1):
            if ch[i] == 0:
                ch[i] = 1;
                p[L] = i;
                DFS(L + 1);
                ch[i] = 0;

if __name__ == "__main__":
    n, f = map(int, input().split());
    p = [0] * n; # 순열
    b = [1] * n; # 이항계수
    ch = [0] * (n + 1);
    for i in range(1, n):
        b[i] = b[i - 1]*(n - i) // i;
    ch = [0] * (n + 1); # 체크리스트
    a = [0] * n; # 순열
    totalSum = 0; # 총합
    DFS(0);
```





## 문제 답안

```python
import sys
def DFS(L, sum):
    if L == n and sum == f: # 종료지점
        for x in p:
            print(x, end=" ");
        sys.exit(0); # 만족하는 순열 출력 후 프로그램 종료
    else:
        for i in range(1, n + 1):
            if ch[i] == 0:
                ch[i] = 1;
                p[L] = i;
                DFS(L + 1, sum + (p[L] * b[L]));
                ch[i] = 0;


if __name__ == "__main__":
    n, f = map(int, input().split());
    p = [0] * n; # 순열
    b = [1] * n; # 이항계수
    ch = [0] * (n + 1);
    for i in range(1, n):
        b[i] = b[i - 1]*(n - i) // i;
    DFS(0, 0);
```



## 풀이와 답안 비교

이항계수를 몰라서 얼마나 걸렸는지... 한 번 제대로 배워야할 것 같다. DFS에서 합계 관련된 문제가 나오면 sum인자를 따로 만드는 것이 더 효율적인 코드가 될 것 같다.







