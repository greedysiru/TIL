# [프로그래머스] 거스름돈 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 거스름돈
def solution(n, money):
    # 메모이제이션
    # 각 인덱스에 해당하는 수를 만들 수 있는 가짓수를 기록
    memo = [0] * (n + 1)
    memo[0] = 1
    # 주어진 동전에 하나씩 접근
    for coin in money:
        for price in range(coin, n + 1):
            memo[price] += memo[price - coin]
    answer = memo[n] % 10000000007
    return answer
```



## Comment

메모이제이션을 통해서, 동전의 가치에 따라 발생하는 경우의 수를 구한다. 주어진 money로부터 가장 작은 동전 단위부터 접근하며 경우의 수를 기록한다. 경우의 수를 기록할 때,  `memo[price] += memo[price - coin]` 이다.

money가 1, 2, 5가 주어지고, n이 5라면 n+1 만큼의 memo 리스트를 만든다. memo리스트의 각 인덱스의 수를 각 동전으로 만들 수 있는 가짓수를 메모이제이션한다. 동전 1로 메모이제이션하면 아래와 같다.

[1, 1, 1, 1, 1, 1]

동전 2로 메모이제이션하면 아래와 같다. 5번 인덱스는 1,2원으로 5원을 만들 수 있는 방법의 수이다. 점화식에 의해서 1원 동전만으로 5원을 만드는 방법의 수 + 1원 동전만으로 3원(price - coin)을 만드는 방법의 수이기 때문이다.

[1, 1, 2, 2, 3, 3]

동전 3으로 메모이제이션하면 아래와 같다.

[1, 1, 2, 2, 3, 4]

가장 작은 동전으로부터 하나씩 접근하여 n원까지 메모이제이션을 하면, memo[n]에는 모든 동전을 사용하여 n원을 만들 수 있는 가짓수가 입력되게 된다.

# Reference

[프로그래머스](https://programmers.co.kr)

