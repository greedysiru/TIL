# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (9) (2021.3.23)



# 리액트 특강



## 과제 설명

* 아래 순서대로 하기
* 캘린더 화면 그리기
  * 캘린더 뷰
  * 일정 클릭 팝업 뷰 (모달): 캘린더와 하나에 묶기
  * 완료일정, 모든일정보기 토글버튼으로
  * 일정 추가하기 뷰: 별도의 url, 라우터, 일정이 없으면 팝업이 안되도록(맨 마지막에)
  * 일자 하나 하나는 배열
  * 
* 기능 만들기
  * 바로 리덕스 , 파이어 스토어 나중에
  * 페이지 이동
  * 가짜 데이터만들어서 실행시켜보기
  * 일정에대한 모든 데이터는 무엇이 가지고 있을까? -> 메인 컴포넌트 가지고 있다.
* 리덕스
  * 수정, 삭제
* 파이어 스토어
  * 미들웨어



# 라우트

* 경로를 나눠준다.
* react-route-dom
* 주소와 컴포넌트를 엮는다.
* props를 넘길 수 있다.
* history를 자동으로 넘긴다.
* 파라미터를 넘길 수 있다.
  * 페이지별로 쪼갤 수 있다.



# 리덕스

* 데이터를 전역으로 관리
* 상태들을 가지고 수정, 추가, 삭제를 한다.
* 모듈을 먼저 만든다.
* 모든 리듀서를 합친 것 -> rootReducer
* 그 이후에 컴포넌트와 엮는다.
* Provider: 컴포넌트트리에 리덕스 주입
* 함수형 컴포넌트와 클래스형 컴포넌트에서 사용하는 방법이 다르다.
  * useSelector: 함수형에서 스토어를 구독
  * useDispatch: 함수형에서 액션을 실행(액션 크리에이터)

