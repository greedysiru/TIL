# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (20)(2021.2.12)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 바둑이 승차(DFS, Cut Edge Tech)

## 나의 전략

* 주어진 바둑이의 무게들을 리스트로 정리
* 상태 트리를 사용하여 각각의 무게를 더한 경우와 안 더한 경우를 나눈다.
* DFS 재귀함수의 첫 번째 인자는 레벨, 두 번째 인자는 더한 무게를 기록
* 탐색 완료 후 별도의 리스트에 무게를 append
* max 함수를 사용하여 구한 무게 중 최댓값 출력



## 문제 풀이

```python
c, n = map(int, input().split());
b = []; # 바둑이의 무게 리스트
for _ in range(n): # 바둑이 무게를 입력 받기
    b.append(int(input()));

wList = [] # 바둑이를 실을 수 있는 무게 리스트

def DFS(L, w):
    if w > c: # 허용 무게 초과인 경우 중단
        return;
    if L == n: # 종료 지점에서 무게 기록
        wList.append(w);
        return;
    else:
        DFS(L + 1, w + b[L]); # 합 누적
        DFS(L + 1, w); # 합 누적 안 하는 경우

DFS(0, 0);
maxW = max(wList);
print(maxW);
```



## 문제 해설

* 부분집합 사용하기
  * 트럭에 태우는 경우
  * 부분집합의 총합이 주어진 무게를 넘지 않는 선에서의 최댓값을 구한다.
* **시간복잡도를 단축시킬 수 있는 방법을 사용 (Cut Edge Tech)**
  * 별도의 변수(**a**)에 재귀함수로 지나간 원소의 값을 무조건 누적
  * 그 값**(a)**으로 전체 바둑이의 무게의 합을 뺀다.-**(b)**
  * **(b)**를 부분집합의 합에 더하기 - **(c)**
  * 즉, 해당 부분집합의 시점에서, 앞으로 남은 노드들의 합을 더하는 것
  * 이때, 그 시점의 최댓값보다 **(c)**가 작다면, 중단한다.

## 문제 답안

```python
def DFS(L, sum, tsum): # 각 원소를 접근하는 인덱스 번호, 합계, 거쳐간 원소들의 합
    global result; # 전역변수
    if sum + (total - tsum) < result: # Cut Edge
        return;
    if sum > c: # 무게제한을 넘는 경우 중단
        return;
    if L == n: # 부분집합 완성된 경우
        if sum > result: # 최댓값 입력
            result = sum;
    else:
        DFS(L + 1, sum + a[L], tsum + a[L]);
        DFS(L + 1, sum, tsum + a[L]);


if __name__ == "__main__":
    c, n = map(int, input().split());
    a = [0] * n; # 바둑이 각각의 무게를 받을 리스트
    result = - 2147000000; # 가능한 바둑이 총 무게의 최댓값
    for i in range(n):
        a[i] = int(input());
    total = sum(a);
DFS(0, 0, 0);

print(result);
```



## 풀이와 답안 비교

내 코드는 case 3, 4, 5가 너무 오래 걸려 통과하지 못 했다. 시간을 단축하기위해 답안의 코드처럼 필요없는 재귀함수 호출을 줄여야 한다.



# 2. 중복순열 구하기(DFS)

## 문제 해설

* 상태트리 구성하기
  * n가닥씩
* for문 사용하기



##  문제 풀이

```python
def DFS(L):
    global cnt; # 전역변수
    if L == m: # 탐색 종료
        for j in range(m): # 중복순열 출력하기
            print(res[j], end = " ");
        print(); # 줄바꾸기
        cnt = cnt + 1;
    else:
        for i in range(1, n + 1):
            res[L] = i
            DFS(L+1)

if __name__ == "__main__":
    n, m = map(int, input().split());
    res = [0] * n;
    cnt = 0; # 갯수 출력
    DFS(0);
    print(cnt);
```



# 3. 동전 교환(DFS, Cut Edge Tech)

## 나의 전략

* 동전의 종류를 배열로 정리
* DFS로 동전을 선택하여 거술러 줄 금액 만들기
  * DFS 함수에 L, sum 인자
* 그 중, 동전의 개수가 최소가 되는 경우 찾아내기



## 문제 풀이

```python
def DFS(L, sum): # L: 레벨, sum: 선택된 동전 합
    global result;
    if sum > m: # 거슬러 줄 금액 초과
        return;
    if sum == m: # 거슬러 줄 금액 충족
        if result > L:
            result = L;
        return;
    if L > result: # Cut Edge
        return;
    else:
        for i in range(n): # 동전의 종류 수 만큼
            DFS(L + 1, sum + coin[i]);

if __name__ == "__main__":
    n = int(input());
    coin = list(map(int, input().split()));
    m = int(input());
    result = 2147000000; # 최솟값
    coin.sort(reverse = True); # 내림차순 정렬
    DFS(0, 0);
    print(result);
```



## 문제 해설

* 동전의 갯수만큼 for문
* 큰 동전부터 탐색하도록 내림차순 정렬한다.
* 레벨이 최소가 되는 것이 답이다.

## 문제 답안

```python
def DFS(L, sum):
    global res;
    if L > res:
        return;
    if sum > m:
        return;
    if sum == m:
        if L < res:
            res = L;
    else:
        for i in range(n):
            DFS(L + 1, sum + a[i]);

if __name__ == "__main__":
    n = int(input());
    a = list(map(int, input().split()));
    m = int(input());
    res = 2147000000; # 최솟값
    a.sort(reverse=True); # 큰 동전부터 탐색하도록
    DFS(0, 0);
    print(res);
```



## 풀이와 답안 비교

도중에 시간초과가 나와서 강의를 조금 참고하고  Cut Edge 를 적용하니 풀 수 있었다.