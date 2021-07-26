# 실전 Git 명령어 정리



## Git 사용 환경 최초 설정

* Git 사용자 이름(username)

```shell
git config --global user.name "greedysiru"
```

* Git 사용자 이메일

```shell
git config --global user.email "greedyisru@g.com"
```



## Git 저장소 초기화

```shell
git init
```



## 원격 저장소 복제

```shell
git clone
```



## Git staging

* 해당 파일 올리기

```shell
git add [파일 명]
```

* 해당 디렉토리의 모든 파일 올리기

```shell
git add .
```



## 스냅샷

```shell
git commit -m "메시지"
```

* add와 동시에 하는 옵션

```shell
git commit -a -m "메시지"
```



## Git 상태, 로그 확인

* Git 상태 확인

```shell
git status
```

* Git 목록 확인

```shell
git log
```

* 한줄 로그 확인

```shell
git log --oneline
```



## 코드 버전 전환

```shell
git checkout
```



## 원격 저장소로 업로드

```shell
git push
```



## 원격 저장소 관리 및 체크

```shell
git remote
```



## 원격 저장소 복제

```shell
git clone [프로젝트의 원격 저장소]
```

* brach를 orgin으로 가서 push하는 명령

 ```shell
 git push [origin] [브랜치 이름]
 ```



## branch

* 현재 repo의 branch들 조회

```shell
git branch
```

* 새 branch 생성

```shell
git branch [새 브랜치 이름]
```

* branch 이동

```shell
git checkout [브랜치 명]
```

* branch 생성 후 이동
  * 현재 branch 기반으로 새 분기 생성

```shell
git checkout -b [새 브랜치 이름]
```

* 기존 branch 기반으로 새 branch 생성

```shell
git checkout -b [새 브랜치 이름] [기존 브랜치 이름]
```

* branch 삭제

```shell
git branch -d [삭제 브랜치 이름]
```





## merge

* branch 병합

```shell
git merge [브랜치 이름]
```

