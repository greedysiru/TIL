# 코드리뷰

## template를 만들자

* 협업 시 형식 정하기
* 한 프로젝트에서 여러 코드타입이 나오는 것을 방지



## console.log

* 프로덕션에서 보이지 않도록 하기
* 로거함수를 사용하여 개발 단계에서는 사용하되, 사용자가 볼 수 없도록 한다.
  * 환경 체크를 하여 프로덕션인 경우 출력하지 않게 함



## 주석 잘 달기

### 함수가 하는 일

* 파라미터로 무엇을 받아오는지
* 리턴값은 무엇인지
* 함수 사용방법

### 컴포넌트

* 어떤 컴포넌트인지
* 필요한 props가 무엇인지
* 컴포넌트 사용방법

### 들어가면 좋은 것

* 작업자
* 수정사항



## return

* 최대한 단순하게
* 연산자를 넣어 return하는 것을 자제
* 성능에 안좋은 영향을 끼친다.



##  삼항 연산자

* 너무 많이 사용하는 것은 바람직하지 않다.
* if문으로 사용하여 대체



## 네비게이션 hash 이동

* push말고 replace를 사용할 것
* history에 기록이 되어서 뒤로가기를 하였을 시, 사용자가 원하는 이동을 하지 않는다.
* ux에 좋지 않다.



## axios

* 모듈화하여 사용하기
*  baseURL, default 헤더 등



## immer

* 참조형을 다룰 때, 기존의 방식보다 데이터를 아낄 수 있다.
* 새로이 만들지 않고 데이터를 넣기만해도 처리가 되므로



# 질의 응답

## useSelector

* 필요한 기능별로 묶어서 사용하여 리렌더링이 일어나지 않도록
* 데이터와 관련 없는 컴포넌트에서 불러오는 것을 하지 말 것



## api

* api는 async를 사용할 것
* 비동기 처리가 중요



## https

* api 호출시, api 주소가 적용된 것인지 확인
  * 인증서가 처리되면 도메인이 달라짐



# 포트폴리오 팁

*  콘솔을 잘 이용하여 기능 설명하기
* 반응형 다루기 곤란할 때, 사이즈 작아지면 경고창을 띄우거나 토스트 띄우기
* 가고싶은 회사 도메인에 맞는 핵심 기술 제시하기
* 리드미 잘 쓸 것
* 깃허프 프로필 포트폴리오로 사용하는 것도 나쁘지 않음
  * 프로젝트 주소나 포트폴리오 주소를 보내는 것을 권장
* ppt 제출도 괜찮음
  * 반드시 보여주고 싶은 화면 강조하기

