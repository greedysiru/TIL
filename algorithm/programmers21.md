


# [프로그래머스] 다리를 지나는 트럭 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# deque
from collections import deque
# 다리를 지나는 트럭


def solution(bridge_length, weight, truck_weights):
    # deque 변환
    truck_weights = deque(truck_weights)
    answer = 0
    # 현재 다리위의 무게
    cur_weight = 0
    # 현재 다리위의 트럭을 나타내는 리스트
    cur_bridge = deque([0]) * bridge_length
    # 경과된 시간
    time = 0
    # 다리 건너기
    while truck_weights:
        # 매 반복시 시간 더하기 (초 경과)
        time += 1
        # 초 경과 시, 맨 끝의 트럭을 완주 처리
        completed_truck = cur_bridge.popleft()
        # 다리위의 무게 그만큼 빼기
        cur_weight -= completed_truck
        # 다리가 트럭을 수용할 수 있는 경우
        # 현재 다리 위 무게 + 다음 트럭 무게
        if cur_weight + truck_weights[0] <= weight:
            # 트럭
            truck = truck_weights.popleft()
            #  트럭 넣기
            cur_weight += truck
            cur_bridge.append(truck)
            # 마지막 트럭인 경우
            if not truck_weights:
                time += bridge_length
                break
        # 수용할 수 없을 때는 이동시키기
        else:
            cur_bridge.append(0)
    return time
```



## Comment

먼저 들어오는 것이 먼저 나가므로 deque를 collections 모듈로부터 불러와서 사용해야한다. while문으로 모든 트럭이 빠져 나갈 때까지 코드를 실행하고 트럭이 나갈때, 트럭이 들어올 수 있을 때, 트럭이 들어오지 못할 때를 분기하여 경과된 시간을 구해야한다. 또 여기에 더해서 다리의 길이를 염두해서 트럭이 다리에서 빠져나가는 것을 시뮬레이션해야 하는데, 나는 이 방법을 찾지 못해서 애먹었다. 다리의 길이만큼의 별도의 리스트를 만들어 트럭이 들어가는 분기에서 append, 매반복문에서 가장 앞의 요소를 빼기위해 popleft()메소드를 사용하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)

