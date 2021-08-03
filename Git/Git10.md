

#  Git Commands

**본 내용은 10분 테코톡   와일더님의 강의를 토대로 작성하였습니다.**



## 1. Branch

* 동일한 소스코드를 토대로 협업할 때, 독립적인 작업 영역을 생성



### 브랜치 생성

```shell
git branch step1
```



### 브랜치 이동

```shell
git switch step1
```



## 2. 브랜치 작업 내역 합치기(Merge)

* 합치는 과정이 history에 남음

```shell
git merge step1
```



### Rebase

* 새롭게 history를 씀
* 기록이 없어짐

```shell
git rebase step1
```



## 3. HEAD

* 현재  checkout된 branch
* 작업 트리의 최근 커밋을 가리킴



### 상대 참조

* HEAD에 ^(caret) 붙이기
  * 한 번 이전 커밋
  * ^(caret)의 갯수대로 이전 커밋으로 돌아감
* ~(tilde) 숫자만큼 이전 커밋으로 돌아감

```shell
git switch HEAD^
// step2 브랜치를 stemp1의 헤드로부터 2개 이전 커밋으로 위치
git branch -f step2 step1~2
```



## 4. 작업 되돌리기

* reset: 완전히 기록을 지움

```shell
git reset HEAD~1
```

* revert: 커밋을 취소, 새로운 커밋을 생성, 기존 커밋은 유지된다.

```shell
git revert HEAD
```



## 5. 삭제된 커밋, 브랜치 복구

* 모든 git 로그 확인

```shell
git reflog
```

* 삭제한 커밋의 해시를 입력하면 복구

```shell
git reset --hard 커밋의 hash
```

* 삭제된 브랜치의 해시를 입력하면 복구

```shell
git switch -c step3 커밋의 hash
```



# Reference

[[10분 테코톡] 와일더의 Git Commands](https://www.youtube.com/watch?v=JsRD2AWxxFg&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=24)

