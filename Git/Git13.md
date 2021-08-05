

#  [노마드코더] 모두를 위한 깃 & 깃허브 - Branches, Conflicts in Branches

**본 내용은 10분 노마드코더 모두를 위한 깃 & 깃허브 강의를 토대로 작성하였습니다.**



## 1. Branches

![83JeN](https://i.stack.imgur.com/83JeN.png)

* master(main) 브랜치로부터 분기되는 별도의 브랜치를 생성할 수 있다.
  * 브랜치: master의 마지막 커밋으로부의 다른 타임라인
* 각 브랜치는 별도의 커밋을 가질 수 있다.
  * 협업시 별도 작업을 할 때 유용
* master의 변경 사항을 파생된 브랜치로 받아올 수 있다.
  * 협업시 수시로 체크할 것
* 작업을 완료한 브랜치를 master에 merge할 수 있다.
* 작업을 완료한 브랜치를 삭제할 수 있다.



## 2. Conflicts in Branches

* 각 브랜치에서 같은 줄을 바꾸게 되면 발생
* Conflict 발생 시 IDE(VSC)에서 처리할 수있다.
  * current change: 현재 브랜치에서 갖고 있는 것
  * incoming change: merge하고 싶은 브랜치에서 가져온 것
  * Accept: 둘 중 하나를 선택 또는 둘다 적용 또는 비교
* Conflict를 해결해야 정상적으로 merge를 할 수 있다.

# Reference

[[노마드코더] 모두를 위한 깃 & 깃허브](https://nomadcoders.co/git-for-beginners/lobby)

[이미지 출처](https://stackoverflow.com/questions/55730292/how-git-maintains-commits-from-deleted-branch/55730465)

