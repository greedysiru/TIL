


# [프로그래머스] 소수 찾기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 소수 찾기
from itertools import permutations
import math


def solution(numbers):
    # numbers를 리스트화
    numbers = list(numbers)
    # numbers의 길이
    numbers_len = len(numbers)
    # numbers의 순열
    number_per = set()
    # 주어진 수로 만들 수 있는 순열
    for i in range(1, numbers_len + 1):
        # 만들어진 순열을 하나의 문자열로 합쳐서 반환
        # -> 정수화
        # -> set 자료형으로 중복 제거
        number_per |= (
            set(map(int, map(''.join, permutations(numbers, i)))))
    # 만들어진 순열에서 0, 1을 제외 (소수가 아니므로)
    number_per = number_per - {0, 1}
    # 가장 큰 수의 제곱근
    number_per_max_sqrt = int(math.sqrt(max(number_per)))
    for j in range(2, number_per_max_sqrt + 1):
        # j를 제외한 j의 배수가 number_per에있으면 소수가 아니다.
        number_per -= set(range(j * 2, max(number_per) + 1, j))
    return len(number_per)
```



## Comment

순열을 변환할 때 join메소드와 map을 사용해서 원하는 자료형을 바꾸는 것을 알게 되었다. 그 다음에는 에라토스 테네스의 체로 소수를 판별하는 부분에서 계속 시간 초과가 나왔다. 영 풀리지 않아서 검색을 해봤는데, set을 사용해서 중복을 제거하여 효율적으로 푸는 방법이 있었다. 나는 이 전에는 while문으로 매번 일일이 탐색하였기에 시간초과가 나왔던 것이다.

# Reference

[프로그래머스](https://programmers.co.kr)

