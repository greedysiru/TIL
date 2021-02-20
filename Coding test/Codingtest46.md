# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (27)(2021.2.20)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 정렬

## 1. 병합 정렬

* 분할 정복
* 배열의 중간지점을 나누어 더이상 영역을 나눌 수 없을 때까지 재귀함수 호출
* 두 원소의 대소를 비교 후 임시의 공간에 원소를 넣으며 진행
* **후회순회**

### 병합 정렬 알고리즘

```python
def Dsort(lt, rt): # 왼쪽부터 오른쪽
    if lt < rt:
        mid = (lt + rt) // 2; # 중간
        Dsort(lt, mid); # 왼쪽
        Dsort(mid + 1, rt); # 오른쪽
        p1 = lt; # 정렬 시작
        p2 = mid + 1;
        tmp = [];
        while p1 <= mid and p2 <= rt: # 원소 비교
            if arr[p1] < arr[p2]:
                tmp.append(arr[p1]);
                p1 += 1;
            else:
                tmp.append(arr[p2]);
                p2 += 1;
        if p1 <= mid: # 왼쪽이 아직 끝나지 않았을 떄
            tmp = tmp + arr[p1: mid + 1] # 리스트 슬라이싱
        if p2 <= rt: # 오른쪽이 아직 끝나지 않았을 때
            tmp = tmp + arr[p2: rt + 1];
        for i in range(len(tmp)): # tmp를원래 배열에 넣기
            arr[lt + i] = tmp[i];

if __name__ == "__main__":
    arr = [23, 11, 45, 36, 15, 67, 33, 21];
    print("Before sort : ", end = " "); # 정렬 전
    print(arr);
    Dsort(0, 7);
    print("After sort : ", end = " ");
    print(arr);
```



## 2. 퀵 정렬

* 분할 정복
* **전위 순회**
* pivot 값을 정하여 정렬 진행
* 지점을 가르키는 변수를 설정(pos)
* pivot을 기준으로 값이 작으면 pos와 자리를 바꾸고 pos += 1
* pivot보다 크면 지나간다
* 우측 끝 전까지 돌면 우측 끝 값과 pivot의 자리를 바꾸고 두 영역으로 나누어 위의 함수를 다시 호출



### 퀵 정렬 알고리즘

```python
def Qsort(lt, rt):
    if lt < rt:
        pos = lt; # 정렬하고자하는 지점
        pivot = arr[rt]; # 가장 오른쪽
        for i in range(lt, rt):
            if arr[i] <= pivot: # 작으면 바꾸기
                arr[i], arr[pos] = arr[pos], arr[i];
                pos += 1; # pos 1 증가
        arr[rt], arr[pos] = arr[pos], arr[rt]; # rt, pos 바꾸기
        Qsort(lt, pos - 1); # 축을 중심으로 왼쪽, 오른쪽 재귀함수 호출
        Qsort(pos + 1, rt);

if __name__ == "__main__":
    arr = [45, 21, 23, 36, 15, 67, 11, 60, 20, 33];
    print("Before sort : ", end = " ");
    print(arr);
    Qsort(0, 9);
    print("After sort : ", end = " ");
    print(arr);
```

