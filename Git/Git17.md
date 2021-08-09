

#  [노마드코더] 모두를 위한 깃 & 깃허브 - CLI(2)

**본 내용은 10분 노마드코더 모두를 위한 깃 & 깃허브 강의를 토대로 작성하였습니다.**



## CLI 명령어 정리

### 	브랜치 생성 후 이동

```shell
git checkout -b <new-branch-name>
```

* 생성 후 바로 생성 브랜치로 이동
* 생성 후 push를 해야 Github에 올라간다.



### 과거 커밋 이동 후 브랜치 생성, 이동

```shell
git checkout <커밋주소> -b <new-branch-name>
```

* 과거 시점의 커밋에서 branch를 생성하는 것도 가능



### 브랜치 목록 조회

```shell
git branch
```



### 브랜치 삭제

```shell
git branch -d <branch-name>
```



### 마지막 커밋 수정

```shell
git commit --amend --no-edit
```

* 커밋 메시지는 수정하지 않고 커밋 수정(추가)



### 파일 상태 조회

```shell
git status
```



### stage에서 제거하기

```shell
git rm <file-name>
```

* 해당 파일을 stage에서 제거
* 디렉토리인 경우 **-r** 옵션 사용
* 캐시가 된 경우 **--cached** 옵션 사용



### remote 조회

```shell
git remote -v
```

* remote: 컴퓨터와 Github 사이의 커뮤니케이션



### remote 추가

```shell
git remote add <new-remote-name> <new-remote>
```



### remote 삭제

```shell
git remote remove <remote
```



### clone

```shell
git clone <repository-url> <directory-name>
```



### .gitignore

* 파일 명을 적으면 해당 파일을 git이 추적하지 않는다.

# Reference

[[노마드코더] 모두를 위한 깃 & 깃허브](https://nomadcoders.co/git-for-beginners/lobby)

