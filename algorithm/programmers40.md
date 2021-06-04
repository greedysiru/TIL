# [프로그래머스] 단속카메라 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 단속카메라
def solution(routes):
    # 카메라의 갯수
    answer = 0
    # 차량이 나간 지점을 기준으로 정렬
    routes.sort(key=lambda x: x[1])
    # 카메라 위치 초기화 (가장 작은 값으로)
    camera = -30001
    # 경로를 하나씩 탐색하기
    for i in range(len(routes)):
        # 카메라의 위치가 진입 지점보다 작은 경우
        if camera < routes[i][0]:
            # 카메라의 갯수 +1
            answer += 1
            # 카메라의 최근 위치 갱신
            camera = routes[i][1]
    return answer
```



## Comment

그리디 알고리즘 문제. 람다식을 사용하여, 차량이 나간 지점을 기준으로 정렬한 뒤, 카메라의 지점이 최신화(진입 지점보다 작은 경우)하여 카메라의 최적의 위치와 갯수를 구할 수 있다.

나간 지점을 기준으로 정렬한다는 아이디어를 생각하지못해서 다른 분들의 풀이를 참고하였다.

# Reference

[프로그래머스](https://programmers.co.kr)

