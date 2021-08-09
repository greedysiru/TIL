

#  [노마드코더] 모두를 위한 깃 & 깃허브 - CLI(1)

**본 내용은 10분 노마드코더 모두를 위한 깃 & 깃허브 강의를 토대로 작성하였습니다.**



## CLI 명령어 정리

### 커밋 내역 확인

```shell
git log
```

* 커밋 이력을 확인 가능
* HEAD: 마지막 커밋
  * 이전 커밋의 내용들이 다 합쳐진 것
  * 파일 정보가 어디에 있는지



### HEAD, Branch 이동

```Shell
git checkout [HEAD 커밋 주소 또는 Branch 명]
```

* master를 입력하여 이동시 현재 상태로 돌아감



### 	커밋 삭제(reset)

```shell
git reset --hard HEAD^
```

* --hard: 삭제 옵션
  * 완전히 과거로 돌아감
* ^: 한 커밋 이전
* 커밋 삭제 이후 origin(원격 저장소)에 삭제된 커밋이 아직 존재



### origin 강제 push

```shell
git push origin master --force
```

* git reset 커밋 삭제 이후 origin의 커밋 기록을 최신화



### Mixed Reset

```shell
git reset HEAD^
```

* 방금 커밋한 변경사항들을 다시 unstage 영역으로 옮김
* 강제 push로 컨플릭트를 무시하고 원격 저장소에 올릴 수 있음



### 원격 저장소 확인

```shell
git remote -v
```



### Soft Reset

```shell
git reset HEAD^ --soft
```

* 되돌릴 커밋의 변경사항을 unstage 영역에 추가하지 않는다.
  * 대신에 stage영역에 추가
  * unstage 영역에 작업중인 파일이 있을 때 섞이지 않고 싶을 때 사용한다.







# Reference

[[노마드코더] 모두를 위한 깃 & 깃허브](https://nomadcoders.co/git-for-beginners/lobby)

