# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (30)(2021.2.23)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 가방문제 (냅색 알고리즘)

## 문제 해설

* 다이나믹 프로그래밍
  * dy: 0으로 초기화한 배열 만들기
  * dy[ j ]: 가방에 j라는 무게까지 담을 수 있을 때 가방에 담을 수 있는 보석들의 최대 가치
* 보석이 한 종류만 있다는 가정하에 dy 테이블 기록하기
  * w: 보석의 무게, v:  보석의 가치
  * dy[ j ] = dy[j - w] + v
  * dy[ j ] 에 값이 있으면 넣을 값과 비교하여 그 중 최댓값을 넣는다.



## 문제 풀이

```python
n, L = map(int, input().split()); # 보석의 종류, 가방 무게 한도
dy = [0] * (L + 1); # 각 인덱스 기준 보석의 최대 가치
for _ in range(n):
    w, v = map(int, input().split());
    for i in range(w, L + 1):
        dy[i] = max((dy[i - w] + v), dy[i]); # 기존의 있는 값과 비교하여 큰 값 입력
print(dy[L]);
```



## 문제 답안

```python
if __name__ == "__main__":
    n, m = map(int, input().split());
    dy = [0] * (m + 1);
    for i in range(n): # 보석의 개수만큼
        w, v = map(int, input().split());
        for j in range(w, m + 1):
            dy[j] = max(dy[j], dy[j - w] + v);
print(dy[m]);
```



## 풀이와 답안 비교

완.벽!



# 2. 동전교환 (냅색 알고리즘)

## 문제 해설

* 냅색 알고리즘 적용

* dy[ j ]: j원을 거슬러주는데 사용된 동전의 최소 개수

  * dy[ j ] = dy[j - 사용한 동전] + 1 **or** dy[ j ] 중 작은 값

  

## 문제 풀이

```python
if __name__ == "__main__":
    n = int(input());
    coinList = list(map(int, input().split()));
    change = int(input()); # 거슬러 줄 금액
    dy = [9999] * (change + 1); # 거술러 줄 수 있는 최소 개수
    dy[0] = 0;
    for i in range(n):
        for j in range(coinList[i], change + 1):
            dy[j] = min(dy[j - coinList[i]] + 1, dy[j]);
    print(dy[change]);
```



## 문제 답안

```python
if __name__ == "__main__":
    n = int(input());
    coin = list(map(int, input().split())); # 동전의 종류
    m = int(input());
    dy = [1000] * (m + 1);
    dy[0] = 0; # 0원을 거스른데에 사용된 개수
    for i in range(n):
        for j in range(coin[i], m + 1):
            dy[j] = min(dy[j], dy[j - coin[i]] + 1);
    print(dy[m]);
```



## 풀이와 답안 비교

냅색 알고리즘으로 코드를 짜는 것은 어렵지 않은데, 문제를 푸는 로직을 도출하는 것이 좀 어렵다. 직접 손을 써보면서 해봐야할 것 같다.



# 3. 최대 점수 구하기 (냅색 알고리즘)

## 문제 해설

* **주어진 문제는 하나만을 풀 수 있다.**
* 2차원  dy 리스트 만들기
  * dy[ i ] [ j ]: i번째 문제까지 15분일 때 얻을 수 있는 최대 점수
  * **다음행을 넘어갈 때 전의 행을 복사할 것**
  * dy[ i ] [.j ] = dy[i - 1] [ j - 문제 푸는 시간 ] +  해당 문제 점수 or dy[.i ] [ j ] 중 큰 값
* 1차원으로 푸는 것이 더 효율적
  * dy는 0으로 초기화
  * dy[ j ]: j분에 얻을 수 있는 최대 점수
  * 뒤에서부터 진행 (주어진 시간 ~ 문제 푸는 데 걸리는 시간), **중복이 되지 않는다.**
  * dy[ j ] = dy[ j - 푸는데 걸리는 시간 ] + 문제 점수 or dy[ j ]

## 문제 풀이

```python
if __name__ == "__main__":
    n, m = map(int, input().split());
    dy = [0] * (m + 1); # 인덱스 분만큼 주어졌을 때의 최대점수
    for _ in range(n):
        s, t = map(int, input().split());
        for i in range(m, t - 1, -1):
            dy[i] = max(dy[i], (dy[i - t] + s));
print(dy[m]);
```



## 문제 답안

```python
if __name__ == "__main__":
    n, m = map(int, input().split());
    dy = [0] * (m + 1); # 인덱스 분만큼 주어졌을 때의 최대점수
    for i in range(n):
        ps, pt = map(int, input().split());
        for j in range(m, pt - 1, -1):
            dy[j] = max(dy[j], (dy[j - pt] + ps));
print(dy[m]);
```



## 풀이와 답안 비교

잘 풀었다. 이제 강의도 끝나간다!