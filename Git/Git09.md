

#  Git 브랜치 전략

**본 내용은 10분 테코톡 웨지님의 강의를 토대로 작성하였습니다.**



## 브랜치 전략이란?

* 여러 개발자가 협업하는 과정에서 git 저장소를 효과적으로 활용하기 위한 work-flow
* 브랜치의 생성, 삭제, 병합이 자유로운 git의 유연한 구조를 활용하여 다양한 방식으로 소스관리를 할 수 있다.



## 자주 쓰이는 브랜치 전략

* git-flow: 5가지의 브랜치를 이용해 운영하는 브랜치 전략
* github-flow: master 브랜치와 Pull Request를 활용한 단순한 브랜치 전략



## git-flow

* 항상 유지되는 2개의 메인 브랜치와 역할을 완료하면 사라지는 3개의 보조 브랜치로 구성
* main: 항상 유지
  * master: 제품으로 출시될 수 있는 브랜치
  * develop: 다음 출시 버전을 개발하는 브랜치
* 보조 브랜치: merge되면 사라짐
  * feature: 기능을 개발하는 브랜치
  * release: 이번 출시 버전을 준비하는 브랜치
  * hot fix: 출시 버전에서 발생한 버그를 수정하는 브랜치



### git-flow 개발 프로세스

* 개발자는 develop 브랜치로부터 본인이 개발할 기능을 위한 feature 브랜치를 만듦
* feature 브랜치에서 기능을 만들다가, 기능이 완성되면 develop 브랜치에 merge



### git-flow의 특징

* 주기적으로 배포를 하는 서비스에 적합
* 가장 유명한 전략인 만큼 많은 IDE가 지원



## github-flow

* 제품이 릴리즈되는 최신버전인 master 브랜치만이 존재



### GitHub-flow 개발 프로세스

* 기능 개발, 버그 픽스, 혹은 어떠한 이유로든 branch를 생성
* github처럼 체계적인 분류가 없으므로 의도가 드러나도록 브랜치 이름을 잘 작성
* pull-request 생성
* 리뷰와 토의
* 실제 서버(테스트환경) 배포
* master에 push, 배포



### github-flow의 특징

* 브랜치 전략이 단순하여 git을 처음 접하는 사람에게도 유용
* CI(지속적 통합), CD(지속적 배포)가 자연스럽게 이루어짐



## 전략 선택

* 한달 이상의 긴 호흡으로 개발하여 주기적 배포, QA, hot fix 등을 수행할 수 있으면 git-flow가 적합
* 항상 릴리즈되어야 할 필요가 있는 서비스와 지속적으로 테스트하고 배포한다면 github-flow와 같은 간단한 workflow가 적합



# Reference

[[10분 테코톡] 웨지의 Git 브랜치 전략](https://www.youtube.com/watch?v=jeaf8OXYO1g&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=23)