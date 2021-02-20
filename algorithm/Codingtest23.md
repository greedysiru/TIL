# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (4)(2021.1.24)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. K번째 약수

## 문제 풀이

```python
n, k = map(int, input().split()); # 두 개의 정수를 공백을 구분으로 입력 받기

arr = []; # 약수를 받을 배열 초기화

for i in range (1, n+1): # 1부터 n까지 약수 찾기
      if n % i == 0:
            arr.append(i) # 약수인 경우 배열에 넣기

if len(arr) < k : # 약수의 개수가 k보다 작으면 -1 출력
      print(-1);
else: # k번째 약수 출력하기
      print(arr[k-1]);
```



## 문제 해설

* 입력을 받으면 문자열로 들어오므로 정수화하기 (**map함수**)
* 약수를 찾았을 때 마다 **카운팅**하기



## 문제 답안

```python
n, k = map(int, input().split()); # 입력받기
cnt = 0; # 약수 갯수 세기
for i in range(1, n + 1): # 약수 찾기
    if n % i == 0:
        cnt +=1 # 약수일시 카운팅
    if cnt == k: # k번째 약수찾으면 출력
        print(i);
        break
else: # k번째 약수를 찾을 수 없을 때
    print(-1);
```



## 풀이와 답안 비교

내 코드는 빈 배열을 생성한 뒤, 주어진 정수의 모든 약수를 담아 k-1 index를 출력하는 방식이었고 강사님의 코드는 cnt 변수를 선언하여, 반복문에서 약수가 나왔을 시 카운팅을하고 k번째에서 약수를 출력 후 break를 하는 방식이었다. 내코드가 틀린 것은 아니었으나, 모든 약수를 구한다는 점에서는 불필요한 작업을 하므로 답안보다는 비효율적인 코드인 것 같다. **올바른 코드를 넘어서, 효율적인 코드를 만들 수 있도록 하자**.



# 2. K번째 수

## 문제 풀이

```python
case = map(int, input()); # test case 입력 받기
n, s, e, k = map(int, input().split()); # n, s, e, k 입력 받기
arr = input().split(); # 순자열 배열 입력 받기
arr = arr[s-1:e]; # 원하는 숫자열만 슬라이싱해서 다시 배열에 넣기
arr.sort() # 오름차순 정렬
print(arr[k - 1]); # k번째 숫자 출력
```



## 문제 해설

* case 입력받을 때는 맨 위에 **for문을 작성하여 그만큼 반복**한다.
* **슬라이싱할 때 index 번호 혼동에 주의**한다.
* **list입력 받을 때 list함수와 map함수를 사용**한다.



## 문제 답안

```python
T = int(input()); # test case 입력
for t in range(T): # case 별로 진행하기
  n, s, e, k = map(int, input().split()); # 입력받고 정수화
  a = list(map(int, input().split())) # 숫자열 입력받고 정수화 후 배열로 저장
  a = a[s-1:e]; # 원하는 숫자열 슬라이싱
  a.sort() # 오름차순 정렬
  print("#%d %d" %(t + 1, a[k-1])); # case와 숫자 출력하기   
```



## 풀이와 답안 비교

test case를 받는 반복문을 쓰지 않았다. 그리고, 리스트를 입력 받을 때 list와 map함수를 사용하지 않아서, 잘못 출력이 되었다. 배열이 짧을 때는 예제의 답을 잘 출력했는데 다른 테스트에서는 전혀 다른 값이 나왔다. 왜일까? 아무튼 map과 list는 잊지말자.

