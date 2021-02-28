# [코드잇] Git으로 배우는 버전 관리 (1) (2021.2.28)



**상세 내용 [블로그](https://greedysiru.tistory.com/242?category=860703) 참고**



# Git 시작하기

## 01. Git이란?

* 코드 버전 관리 프로그램



### 버전관리

* 파일의 변화를 시간에 따라서 기록
* 특정 시점의 버전을 다시 꺼내올 수 있다.
* 지난 과정을 확인할 수 있다.
* 이전 버전으로 돌아갈 수 있다.



### git

* 버전 관리, 동시 협업을 가능하게 하는 툴



## 02. GitHub란?

* git으로 관리한 프로젝트를 올릴 수 있는 사이트
* 원격 저장소를 대신 제공해주는 서비스
* 다른 컴퓨터에 작업물을 보낼 수 있다.
* 다른 사람과의 협업 가능



# Git 써보기

## 01. repository와 commit

### 레포지토리 (Repository)

* 프로젝트 디렉토리: 프로젝트와 관련된 모든 디렉토리와 파일들을 담은 것
* **레포지토리: git이 프로젝트 디렉토리의 버전별 모습을 기록하는 곳**
  * **.git**이 레포지토리
* **커밋이 저장되는 곳**



### 커밋 (Commit)

* **프로젝트 디렉토리의 모습을 하나의 버전으로 남기는 동작**
* 사진처럼 레포지토리에 저장
* 그 **결과물 자체**를 커밋이라고도 함



## 02. commit에 관한 주의사항

* 커밋을 하기 전 **사용자의 이름**과 **이메일 주소**를 설정
* **커밋 메시지** 남기기 (**옵션 -m**)
* 커밋할 파일을 **git add**로 지정



## 03. Git의 3가지 작업 영역

* **working directory**
  * 작업을 하는 프로젝트 디렉토리
  * working tree라고 하기도 한다.
* **staging area**
  * **git add**를 한 파일들이 존재하는 영역
  * index라고도 하기도 한다.
* **repository**
  * working directory의 **변경 이력**들이 저장되어 있는 영역

즉,

> **working directory**에서 뭔가 작업을 하고,
>
> 작업한 파일들을 **git add** 하고,
>
> **커밋**을 하면 **staging area**에 있던 파일들의 모습이 스냅샷(snapshot)처럼 **repository에 저장**



### staging area가 필요한 이유

* 변경 사항을 선별적으로 커밋에 반영하기 위해서
* 세밀한 버전 관리를 할 수 있다.



## 04. Git이 보는 파일의 상태

* **Untracked 상태**: 파일의 변동사항이 전혀 추적되고 있지 않는 상태
* **Tracked 상태**: 파일의 변동사항이 추적되고 있는 상태
  * **Staged 상태**: 파일의 내용이 수정되고 나서 staging area에 올라와 있는 상태(git add)
  * **Unmodified 상태**: 현재 파일의 내용이 최신 커밋의 모습과 비교했을 때 전혀 바뀐 것이 없는 상태
  * **Modified 상태**: 최신 커밋의 모습과 비교했을 때 조금이라도 바뀐 내용이 있는 상태



## 05. 특정 git 커맨드의 사용법을 알고 싶다면

> **git help [알고 싶은 커맨드의 이름]**

또는

> **man git-[알고 싶은 커맨드]**



## 06. Git 명령어 정리

`git init`: 현재 디렉토리를 Git이 관리하는 프로젝트 디렉토리(=working directory)로 설정하고 그 안에 레포지토리(.git 디렉토리) 생성

`git config user.name 설정할이름`: 현재 사용자의 아이디를 설정

`git config user.email 설정할이메일`: 현재 사용자의 이메일을 설정

`git add 파일이름`: 수정사항이 있는 특정 파일을 staging area에 올리기

`git add 디렉토리명`: 해당 디렉토리 내에서 수정사항이 있는 모든 파일을 staging area에 올리기

`git reset 파일이름`: staging area에 올린 파일 다시 내리기

`git status`: Git이 현재 인식하고 있는 프로젝트 관련 내용들 출력(문제 상황이 발생했을 때 현재 상태를 파악하기 위해 활용하면 좋음)

`git commit -m "커밋 메시지"`: 현재 staging area에 있는 것들 커밋으로 남기기

`git help 커맨드이름`: 사용법이 궁금한 Git 커맨드의 공식 메뉴얼 내용 출력

# Reference

[코드잇 -Git으로 배우는 버전 관리](https://www.codeit.kr/courses/version-control-with-git)

