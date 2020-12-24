# Codeup: 기초 100제 (91~100) (2020.12.24) 

**사용 언어는 Python입니다.**

-폰트14

## 1. 1093

첫 번째 줄에 출석 번호를 부른 횟수인 정수 n이 입력

두 번째 줄에 무작위로 부른 n개의 번호가 공백을 두고 입력

1 번부터 번호가 불린 횟수를 순서대로 공백으로 구분하여 한 줄로 출력

```python
n = int(input());
a = input().split();
d = {}
for i in range(1,24):
  d[str(i)] = 0;
for i in range(n):
  if str(a[i]) in d:
    d[str(a[i])] = d[str(a[i])] + 1;
for i in range(1,24):
  print(d[str(i)], end = ' ');
```

빈 딕셔너리 `d`를 생성 후 1부터 23까지 `key`를 만든다. `key`의 데이터 형식은 `str`

부른 횟수 `n` 만큼 번호 리스트`a`를 부르면, 각각의 숫자가 나온다.

나온 숫자를 `d`에 `key` 와 비교해서 1씩 더한다.

`value`를 나란히 출력



## 2. 1094

첫 번째 줄에 출석 번호를 부른 횟수인 정수 n이 입력

두 번째 줄에 무작위로 부른 번호가 공백을 두고 입력

불린 출석 번호를 반대로 출력

```python
n = int(input());
a = input().split();
for i in reversed(range(n)):
  print(a[i], end=" ");
```



## 3. 1095

첫 번째 줄에 출석 번호를 부른 횟수인 정수 n이 입력

두 번째 줄에 무작위로 부른 번호가 공백을 두고 입력

출석 번호 중 가장 빠른 것을 1개만 출력

```python
n = int(input());
a = map(int,input().split());
print(min(a));
```

`map` : 리스트의 요소를 지정된 함수로 처리



## 4. 1096

첫 번째 줄에 바둑판에 올려 놓을 흰 돌의 개수(n)가 입력

둘 번째 줄부터 n+1번째 줄까지 흰 돌을 놓을 좌표(x,y)가 n줄 입력

흰돌이 올려진 바둑판의 상황을 있는 위치는 1, 없는 위치는 0으로 출력(바둑판은 19 * 19)

```python
n = int(input());
location = [[0]*19 for i in range(19)];
for j in range(n):
  x,y = map(int,input().split());
  location[x-1][y-1] =1;
for a in range(19):
  for b in range(19):
    print(location[a][b], end=' ');
  print();  
```

바둑판은 19 * 19 이므로 , `location = [[0]*19 for i in range(19)];` 

돌이 있는 위치를 x,y 리스트 형식으로 받는다.

행렬은 0부터 세므로, `[x-1][y-1]`

문제에 제시한 대로, 대괄호를 제외하고 숫자만 한 줄씩 출력해야한다. 한 행씩 숫자간 공백을 가지고 출력하므로 `for` 문을 위와 같이 두 번 사용



## 5. 1097

바둑알이 깔려 있는 상황이 19*19 크기의 정수값으로 입력

십자 뒤집기 횟수(n)가 입력

십자 뒤집기 좌표가 횟수(n)만큼 입력

십자 뒤집기 결과를 출력

```python
baduk = []
for _ in range(19):
  matrix = list(map(int, input().split()))
  baduk.append(matrix)
n = int(input())
for _ in range(n): 
  x, y = map(int, input().split()) 
  for i in range(19): 
    baduk[i][y-1] = 1 if baduk[i][y-1] == 0 else 0 
    baduk[x-1][i] = 1 if baduk[x-1][i] == 0 else 0 
for i in range(19):
  print(*baduk[i])
```



## 6.  1098

첫 줄에 격자판의 세로(h), 가로(w) 가 공백을 두고 입력

두 번째 줄에 놓을 수 있는 막대의 개수(n) 입력

세 번째 줄부터 막대의 길이(l), 방향(d), 좌표(x,y)가 입력

모든 막대를 놓은 격자판의 상태를 출력

```python
h, w = map(int, input().split())
shape = [[0 for _ in range(w)] for _ in range(h)]
n = int(input())
for _ in range(n) :
  l, d, x, y = map(int, input().split())
  x, y = x-1, y-1
  if d == 0 :
    for i in range(l) :
      shape[x][y+i] = 1
  else :
    for i in range(l) :
      shape[x+i][y] = 1
for s in shape :
  print( *s )
```

![55](../../../../../Library/Application Support/typora-user-images/55.png)

## 7.  1099

10*10 크기의 미로 상자의 구조와 먹이 위치가 입력(2,2에서 출발)

성실한 개미가 이동한 경로를 9로 표시해 출력

```python
ant_house = [
         [1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
         [1, 0, 0, 1, 0, 0, 0, 0, 0, 1],
         [1, 0, 0, 1, 1, 1, 0, 0, 0, 1],
         [1, 0, 0, 0, 0, 0, 0, 1, 0, 1],
         [1, 0, 0, 0, 0, 0, 0, 1, 0, 1],
         [1, 0, 0, 0, 0, 1, 0, 1, 0, 1],
         [1, 0, 0, 0, 0, 1, 2, 1, 0, 1],
         [1, 0, 0, 0, 0, 1, 0, 0, 0, 1],
         [1, 0, 0, 0, 0, 0, 0, 0, 0, 1],
         [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
]
x,y = 1,1
while ant_house[x][y] != 2 :
  if ant_house[x][y] == 0 :
    ant_house[x][y] = 9
    y = y+1
  else :
    x = x+1
    y = y-1
ant_house[x][y] = 9
for house in ant_house :
  print( *house )

```



# Reference

https://codeup.kr/problemsetsol.php

https://colab.research.google.com/drive/1j41zX9Z4atBC5jzzerAfkfLizkIoS-2N#scrollTo=hCC2CIZ8imeU