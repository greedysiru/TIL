# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (4) (2021.3.8)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 2869

[문제 링크](https://www.acmicpc.net/problem/2869)

```python
import math

# a : 올라가는 미터, b :  미끄러지는 미터, v : 나무 막대
a, b, v = map(int, input().split())
# 걸린 일수
d = math.ceil(((v - b) / (a - b)))

print(d)
```



# 10250

[문제 링크](https://www.acmicpc.net/problem/10250)

```python
t = int(input())
# test 케이스 만큼 입력 받기
for i in range(t):
    h, w, n = map(int, input().split())
    # 호수의 층 번호
    f = n % h
    # 호수의 방 번호
    r = (n // h) + 1
    # 딱 나누어 떨어지는 경우
    if f == 0:
        f = h
        r -= 1

    print((f * 100) + r)
```



# 1929

[문제 링크](https://www.acmicpc.net/problem/1929)

```python
def isPrime(num):
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            return 0
    return 1 * (num != 1)


m, n = map(int, input().split())

for i in range(m, n + 1):
    if isPrime(i):
        print(i)
```

