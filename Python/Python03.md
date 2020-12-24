# [우리밋_woorimIT] Python 배열,리스트,2차원 배열 (2020.12.24)

**상세 내용 [블로그](https://greedysiru.tistory.com/59) 참고**



## Iterable

Python에서 데이터가 반복해서 나타나는 형태의 객체들은 `Iterable` 이라고 정의한다.

* List
* Tuple
* Set
* Dictionary

`Iterable` 안에 있는 데이터를 다루는 괄호에 따라 아래와 같이 분류 된다.

> 1차원 [1,2,3]
>
> 2차원 [ [1,2,3] , [4,5,6] ]



## 배열과 리스트

|     Array     |       List        |
| :-----------: | :---------------: |
|  순차적 주소  | 임의 주소, 포인터 |
|  같은 자료형  | 여러가지의 자료형 |
|   빠른 검색   |     느린 검색     |
| 메모리 비효율 |    메모리 효율    |



## 2차원 배열

2행 3열의 2차원 배열과 호출 형식은 아래와 같다.

|   0,0   |   0,1   |   0,2   |
| :-----: | :-----: | :-----: |
| **1,0** | **1,1** | **1,2** |



### Python 2차원 배열 선언

```python
array = [[0 for _ in range(5)]for _ in range(3)]
```

Python의 배열은 리스트 형식이므로 공간과 데이터를 같이 선언

### numpy 라이브러리

```python
import numpy
array = numpy.arange(15).reshape(3,5);
```

`arange`함수는 범위 지정 함수

`reshape` 행,열 지정

```python
array = numpy.zeros((3,5));
arraay = numpy.ones((3,5));
```

 `zeros`는 0을 채우고 `ones`는 1을 채운다.



## 2차원 배열 연습문제 - 내 미래

**문제**

> 훈련병인 철수는 교관의 지시에 따라야한다.
>
> 교관은 "좌로 1보, 하로 2보 가!"와 같이 좌,우,상,하로 이동할 것을 명령한다.
>
> 철수의 현재 위치가 입력으로 주어질 때 교관의 명령대로 이동한 위치는 어디일까?

**제한 조건**

> 철수의 현재 위치는 첫 입력 값으로 공백을 두고 입력
>
> 훈련소의 전체 공간 크기는 5*5
>
> 교관이 지시한 명령은 절대 훈련소 공간을 벗어나지 않음
>
> 좌는 왼쪽, 우는 오른쪽, 상은 위쪽, 하는 아래쪽
>
> 입력은 좌,우,상,하의 순서대로 공백을 두고 입력

**입력**

```
3 3
1 2 1 3
```

**출력**

```
0 0 0 0 0 
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 1 0 
```

**풀이**

```python
import numpy as np # numpy 호출
cur = tuple(int, input().split());  # 철수의 현재 위치, 변하지 않는 tuple 사용
lft, rgt, up, down = map(int, input().split()); # 좌우상하 입력
coords = np.zeros( (5,5), dtype = int ) # 5*5 2차원 배열 생성, int타입
move = ( cur[0] -up +down , cur[1] -lft + rgt )
coords[move[0] -1][move[1] -1] = 1 # 배열의 범위를 넘지 않도록 -1

for crd in coords:
  print( *crd) # Asterisk로 Unpacking
```



# Reference

https://www.youtube.com/watch?v=imEIUqquxzs

https://www.youtube.com/watch?v=qOS_Rcwk_VU&list=PLSK4WsJ8JS4dOszA7Zr8paqI81Mv27tNq&index=19