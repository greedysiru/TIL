# 데브옵스 핸드북(1부 1장 - 애자일, 지속적인 전달 그리고 세 가지 방법

**본 내용은 진 킴, 제즈 험블, 패트릭 드부아, 존 윌리스, 『이펙티브 타입스크립트』, 김영기, 김나리 옮김, 에이콘출판주식회사(2018년)를 토대로 작성하였습니다.**



## 생산 가치 흐름

### 가치 흐름이란

* 가치 흐름(value stream): 린의 가장 근본적인 개념
* 조직이 고객의 요구에 맞춰 출시에 착수하는 일련의 활동

* 정보와 자재의 이중 흐름을 포함하는 상품, 서비스를 설계하고 생산해 고객에게 전달하는 일련의 활동
* 빠르고 예층 가능한 리드타임을 가능하게 하려면
  * 작은 배치 크기(small batch size) 기법 사용
  * WIP(Work In Process) 축소
  * 다운스트림 워크센터로 결함이 전달되지 않도록 하기 위한 재작업 방지
  * 지속적 시스템 최적화를 통한 균형잡힌 작업 흐름



## 기술 가치 흐름

* **가치는 서비스가 프로덕션 서버에서 동작할 때만 생성**
* **배포가 빠르고 안정적으로 진행될 수 있도록 해야 함**
  * 서비스 중단, 보안 실패, 규정 위반 등의 혼란이 없어야 함

* 데브옵스에서의 기술 가치 흐름
  * **고객에게 가치를 전달하기 위해 비즈니스 가설을 개발 가능한 서비스로 전환하는 프로세스**
  * 이 프로세스에는 비즈니스 목표, 개념, 아이디어, 가설 수립이 입력되고 작업들을 업무 백로그에 추가해 개발 상태로 인정하면 작업이 시작
* 개발 작업 시작 이후
  * 애자일 또는 반복(이터레이션 또는 스프린트)적인 프로세스를 따르는 팀들은 아이디어들을 사용자 스토리나 기능 명세로 변형
  * 애플리케이션이나 코드로 구현
  * 코드는 버전 관리 저장소에 체크인



### 배포 리드타임에 집중하기

* **배포 리드타임: 가치 흐름의 한 부분**
* 가치 흐름은 가치 흐름 내에 있는 엔지니어가 버전 관리 시스템에 변경 사항을 체크인할 때 시작되고 프로덕션 서버에 성공적으로 반영될 때 종료
  * 엔지니어: 개발, QA, IT 운영, 정보 보안
* 빠른 흐름이 가능하게 하고 높은 품질을 얻어야 함
* 설계, 개발, 테스트, 운영 가치 흐름 순서의 대규모 배치 작업은 목표 달성에 적합하지 않음
  * 폭포수 개발, 오래 지속하는 기능 브랜치
* **테스트, 운영 작업이 디자인 및 개발 작업과 동시에 진행되는 소규모 배치 작업이 목표 달성에 적합**
  * 더해서, 가치 흐름내 모든 부분의 품질을 높여야 함



#### 리드타임 vs. 프로세스 타임 정의하기

* **리드타임: 린 커뮤니티에서 가치 흐름의 성과를 측정하는 데 사용하는 일반적인 방법**
  * 요청 생성 ~ 작업 완료
  * 고객이 경험하는 것
* 프로세스 타임
  * **요청에 따른 착수(작업 시작) ~ 작업 완료**
  * 작업 처리 대기중인 큐(queue) 상태가 생략
* 리드타임에 대한 프로세스 타임의 비율은 **효율성의 중요한 척도**
  * 높을 수록 효율적
  * **큐 상태에서 대기하는 시간을 감소시켜야 함**



#### 일반적인 시나리오: 몇 달씩 소요되는 배포 리드타임

* 일반적인 비즈니스 상황에서는 배포 리드타임이 몇 달씩 걸림
* 원인
  * 긴밀하게 결합된 단일 애플리케이션
  * 흔치 않은 통합 테스트 환경
  * 긴 테스트 및 프로덕션 환경 리드타임
  * 수동 테스트의 높은 의존도
  * 복수의 승인 프로세스
* **복잡한 대형 조직에서 흔히 발생**
* 막바지에서 형편 없는 결과물이 나올 수 있음



#### 이상적인 데브옵스: 몇 분이면 충분한 배포 리드타임

* 개발자는 자신의 작업에 대해 신속한 피드백을 받음
  * 빠르고 독립적인 코드 실행과 통합
  * 코드의 유효성 검증
* 버전 관리 저장소에서 지속적으로 작은 코드 변경 사항을 체크. 자동화와 탐색적 테스트 수행
* **변경 사항이 프로덕션에서 의도한 대로 동작하고 문제를 인식하여 수정할 수 있다는 자신감을 얻을 수 있음**
* 느슨한 결합 구조를 갖는 모듈러에 쉽게 구현
* 소규모 팀들은 자율성을 얻고 작업의 실패 가능성이 작아짐
* (자동화된) 커밋 단계 -> 자동화된 테스트 -> 탐색적 테스트 -> 프로덕션 환경 배포



### 재작업 척도로서 %C/A 관찰

* %C/A: 기술 가치 흐름의 세 번째 핵심 지표
  * percent complete and accurate
  * **기술 가치 흐름의 각 단계 산출물에 대한 품질을 반영**
* 다운스트림의 고객에게 작업 시간 중 그대로 작업할 수 있는 일을 받는 것이 몇 퍼센트인지
  * **일을 시작하기 전에 정보를 다듬는 작업 없이 일을 시작할 수 있는 비율**



## 데브옵스를 뒷받침하는 세 가지 원칙

* 기존에 관찰된 모든 데브옵스 행동과 패턴에서 도출된 데브옵스 원칙의 집합
* 첫 번째: 개발(Dev)에서 운영(Ops), 고객에 이르기까지 신속한 좌-우 작업 흐름을 만드는 것
* 두 번째: 기술 가치 흐름의 모든 단계에서 우측에서 좌측으로 빠르고 지속적인 피드백 제공
* 세 번째: 생성적인 높은 신뢰 문화를 만드는 것



## 용어 정리

1. 다운스트림 워크센터: 고객과 공감대를 형성하는 고객 접점 업무 영역
2. 사용자 스토리: 최종 사용자 관점에서 작성한 소프트웨어 기능에 대한 일반적인 비공식 설명
   * **"저는 [페르소나]로서, [하고 싶은 일]을 하여 [목적]을 이루고 싶습니다.”**
3. 탐색적 테스팅: 이전 테스트 경험에 기반해 다음 테스트를 설계하는 테스트 설계와 실행이 동시에 이루어지는 경험기반 테스팅



# Reference

[데브옵스 알아가기(5) : 3Ways - 제2방법](https://engineering-skcc.github.io/devops/DevOps5-3Ways-2/)

[[Atlassian] 예제 및 템플릿을 포함한 사용자 스토리](https://www.atlassian.com/ko/agile/project-management/user-stories)

[탐색적 테스팅](http://jidum.com/jidums/view.do?jidumId=586)