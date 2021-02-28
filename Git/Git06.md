# [코드잇] Git으로 배우는 버전 관리 (2) (2021.3.1)



**상세 내용 [블로그](https://greedysiru.tistory.com/243?category=860703) 참고**  

# GitHub 시작하기

## 01. Remote Repository

* **원격 레포지토리 <-> 로컬 레포지토리: 내 컴퓨터의 레포지토리**



### 로컬 레포지토리 올리기

* 이미 로컬 레포지토리가 있고 커밋도 한 상태이면 터미널에 아래를 입력

```shell
git remote add origin 리모트 레포지토리 주소.git
git branch -M main
git push -u origin main
```



## 02. Local Repository에서 바뀐 내용을 Remote Repository에도 반영하기

* 새로운 커밋을 리모트 레포지토리에 반영하기 위해서 아래의 커맨드를 입력한다.

> **git push**

### git push 설정

* **리모트 레포지토리의 Settings -> Manage access -> Invite a collaborator**

  * 초대한 사용자가 해당 리모트 레포지토리에 git push 가능

  

## 03. Remote Repository에서 바뀐 내용을 Local Repository에도 반영하기

* 아래의 커맨드를 입력

> **git pull**



### 리모트 레포지토리를 만드는 이유

* 안정성
  * 컴퓨터의 물리적 훼손이나 도난에도 레포지토리를 잃지 않는다.
* 다른 개발자들과 협업을 할 수 있다.
  *  git push, git pull을 활용한다.
  * 리모트 레포지토리를 중심으로 협업 가능



## 04. 다른 프로젝트 가져오기

* 깃허브의 프로젝트를 컴퓨터로 복제

> **git clone github프로젝트주소**



## 05. 오픈 소스 프로젝트란

* GitHub에는 수많은 오픈 소스 프로젝트가 있다.
* **오픈 소스 프로젝트 (open source project)**
  * 자유 소프트웨어 재단(리차드 스톨만)으로부터 시작
  * 소스 코드가 공개
  * 누구나 코드를 자유롭게 가져다 사용
  * 원래의 코드를 자신이 원하는 대로 수정
  * 다양한 종류의 라이센스 존재
* 오픈 소스 프로젝트의 장점
  * 무료 사용
  * 여러 개발자들이 참여하므로 코드의 신뢰도가 높다.
  * 오픈 소스 프로젝트 참여 중이 다른 개발자들과 소통할 수 있다.
  * 어떤 프로그램을 개발할 때 특정 분야에서 표준처럼 사용되는 오픈 소스 프로그램을 많이 활용할수록 전체 개발 속도를 단축
* 오픈 소스 프로젝트의 단점
  * 참여자 수가 많지 않거나, 참여자의 실력이 좋지 않으면 신뢰성 보장이 어렵다.
  * 해당 오픈 소스를 사용해서 문제가 생겼을 시, 책임이나 보상을 할 주체가 없다.



## 06. 마크다운 

* GitGHub의 README.md 에서 사용하는 문법
  * README
  * 프로젝트에 대한 설명
  * 프로그램의 주요 사용법
  * 프로그램을 실행시키기 위해 어떤 사전 작업이 필요한지
* [마크다운 언어의 규칙](https://guides.github.com/features/mastering-markdown/)



## 07.Git 명령어 정리

`git push -u origin master`: 로컬 레포지토리의 내용을 처음으로 리모트 레포지토리에 올릴 때 사용

`git push`: 로컬 레포지토리의 내용을 리모트 레포지토리에 보내기

`git pull`: 리모트 레포지토리의 내용을 로컬 레포지토리로 가져오기

`git clone 프로젝트github주소`: GitHub에 있는 프로젝트를 내 컴퓨터로 가져오기



# Reference

[코드잇 -Git으로 배우는 버전 관리](https://www.codeit.kr/courses/version-control-with-git)