# [항해99 1기] [Chapter6] 실전 프로젝트 (3) (2021.4.26)



**실전 프로젝트에 대한 일지**



# 오늘한 것

## 회의

### 프론트

* 디자인패턴 현상유지 할듯
  * 아톰 디자인과 기존 방식의 차이가 없다.
* 타입스크립트, pwa, s3를 S.A 피드백 시간에 질문할 것
* 디자인 우선사항: UI/UX, 와이어프레임



### 백엔드

* API 호출 최소화
* 오픈 API 서버, 오리진 API 서버 운용 방식을 정하는 중
* S.A 피드백 질문 사항
  * 비로그인 사용자에 대해서 선별 처리할 것인지
  * 오픈 API를 여기저기서 불러오는데, API를 한꺼번에 만들어서 보낼 지 아니면 각각 만들어서 할 지
  * ELK에 대해서



## SA 피드백

* 외출을 할 때 보는 것이다
  * 유저가 수동적으로 받아볼 수 있도록
  * 새벽 6시에 e-mail을 보내주는 방식 - 이것도 디자인이 필요할 듯
  * or 알림톡
  * 사업자 등록을 해야할 수도
* 오늘의 날씨 변화에 대한 정보
  * 비가 오거나 등
  * 기본적인 정보 알려주기
* 요즘도 pwa로 많이 한다
  * RN
  * 찾아봐라
  * 굳이? 우리 홈페이지에 쉽게 들어갈 수 있는 아이콘을 만들어라
  * 안드로이드 내부 api 사용할 수 있는지? -> 잘은 모르겠다.
* 오픈 API 호출 시 
  * GPS를 받아서 그 지역에 해당하는 api호출
  * 호출이되면 캐시DB에 저장
  * 추후 호출이되면 캐시 DB에 있으면 그것을 사용(Redis)
  * -> 날씨 데이터를 가져올 때 언제 저장된 정보인지 가져올 것이다.
    * 이전이 24시간 전이면 업데이트하여라
* 점수 계산시
  * 비로그인 자는 점수가 없어도 날씨 데이터를 보여줄 것임
  * -> API 서버에서 openAPI를 호출하는 것이 나을 것
* s3에 이미지서버를 구축
  * 유저의 프로필 사진
  * 버튼, 로고 안 바뀌는 것은 
* 로그스태시 ,ELK
  * 매우 좋다
  * 통계학적으로 의미가 있다.
  * 어떤 키워드? -> 잘 모른다
* 어떤로그를 저장할 지?
  * 3주차에 생각해볼 것 
* 타입스크립트
  * good. 도입하면 좋다.



## SA 이후 회의

* 이메일, 알림톡 좋은 듯
* PWA 더 알아보자



# 할 것

* ELK 알아보기

* PWA 배포방법

* 컨셉 정하기(테마)

  * 화요일

* element 컴포넌트 만들기

  * 디자이너에게 가이딩 받기

* 타입스크립트 공부

* Next.js 공부하기

* 패키지 설정

* 불변성 유지 공부

* 도메인 준비

* s3 세팅

* HTTPS 알아보기

  

