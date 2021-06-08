# [프로그래머스] 땅따먹기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 땅따먹기
def solution(land):
    answer = 0
    # land의 행 길이
    land_len = len(land)
    # 주어진 2차원 리스트 land의 한 행씩 접근
    # 다음 행의 해당 열에는 현재 행의 해당 열을 제외한 요소들 중 최댓값 구하기
    # 그 이후, 다음 행의 해당 열의 값을 더한 후, 메모이제이션 (누적합)
    for i in range(land_len - 1):
        land[i + 1][0] = max(land[i][1], land[i][2],
                             land[i][3]) + land[i + 1][0]
        land[i + 1][1] = max(land[i][0], land[i][2],
                             land[i][3]) + land[i + 1][1]
        land[i + 1][2] = max(land[i][0], land[i][1],
                             land[i][3]) + land[i + 1][2]
        land[i + 1][3] = max(land[i][0], land[i][1],
                             land[i][2]) + land[i + 1][3]
    answer = max(land[land_len - 1])
    return answer
```



## Comment

DFS로 접근하려고 하였다가 많은 시간을 소요하였다.

다이나믹 프로그래밍 문제로, 주어진 land 리스트를 이용한다. 다음 행의 각 열의 요소와 이전 행의 최댓값(다음 행에서 접근하고 있는 열번호와 다른 요소들 중)을 더하여 메모이제이션하면 된다.

처음에는 별도의 memo 리스트를 만들어 메모이제이션을 하려 했으나, 기존의 주어진 리스트에서 메모이제이션하는 것이 다음 루프에서도 접근하기 용이하므로 memo리스트를 생략하였다.



# Reference

[프로그래머스](https://programmers.co.kr)

