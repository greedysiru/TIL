

# 지속적 배포

**본 내용은 10분 테코톡 웨지님의 강의를 토대로 작성하였습니다.**



## 1. CI / CD

* 개발부터 배포까지의 과정을 자동화
* 개발된 내용이 사용자에게 빠르게 도달할 수 있게 해주는 방법론
* CI: Continuous integration(지속적 통합)
* CD: Continuous Delivery & Continuous Deployment



### CI란

* 새로 추가된 코드가 성공적으로 배포 브랜치의 프로젝트 코드에 통합되도록, 소스 관리 및 테스트 및 리포트 과정을 자동화하는 것



### CD란

* Continuous Delivery & Continuous Deployment
* CI를 통해 새롭게 추가된 코드를 유저에게 바로 제공할 수 있도록 배포 과정을 자동화



## 2. CD

### Continous Delivery

* 지속적 제공
* CI를 통해 이상없는 코드를 레포지토리(구성원들이 쉽게 접근할 수 있는 공간)에 자동으로 릴리즈 하는 것을 의미
* 바로 배포할 수 있는 코드베이스를 확보하는 것이 목적



### Continous Delivery에 해당하는 것

1. 빌드하기
2. 자동 배포 스크립트문을 실행 가능한 트리거 생성
3. 운영 환경에 필요한 매개 변수 설정
4. 운영 환경에서의 테스팅
5. 즉시 배포 가능한 환경에 스테이징
6. CI/CD 파이프라인 유지 관리



### Continuos Deployment

* 지속적 배포
* Continuous Delivery의 파이프라인을 통과 + 프로덕션에 자동 배포



### Continuos Delivery vs. Continuos Deployment

* Continuos Delivery
  * 프로덕션 배포 트리거는 수동으로(배포 과정은 자동화)
* Continuos Deployment
  * 프로덕션 배포까지 자동화
* CI/CD라고 하면, 일반적으로 자동 배포까지의 과정을 통칭하지만, 어디까지 자동화가 이루어져 있는지를 설명하기 위해서 별도로 구분
* 운영환경에서 QA팀을 동원한 테스팅을 하는 경우, 수동배포를 선택
* 충분한 테스트를 거쳤다고 여기면 바로 배포하는 경우, 자동배포를 선택
* team by team



# Reference

[[10분 테코톡] 웨지의 지속적 배포](https://www.youtube.com/watch?v=X6QGhg19Kqg)