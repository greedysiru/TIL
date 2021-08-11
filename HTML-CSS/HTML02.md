# [드림코딩 by 엘리] HTML 태그 정리



**본 내용은 드림코딩 by 엘리님의 강의를 토대로 작성하였습니다.**



## 1. Semantic Tags(Semantic Markup)

* Semantic: 의미의, 의미가 있는
* 의미가 있는 Semantic 태그를 적절한 곳에 사용하는 것이 권장된다.
  * 예시) 웹 페이지의 제목을 강조하기 위해서 span 태그를 사용하여 글자 크기를 키우는 것보다, h1태그를 사용



### Semantic Tag를 사용하면 좋은 점

* SEO: 검색 최적화
* Accessibility: 웹 접근성
* Maintainability: 유지보수성



## 2. 웹사이트 구조를 이루는 태그들(박스 태그)

* div태그를 남발하는 것은 자제



### header 태그

* 웹 사이트 로고
* 사용자 중요 정보



### nav 태그

* 하위에 여러가지 메뉴가 모여있을 때



### footer 태그

* 웹사이트 하단에 사이트에 대한 정보나 부가적인 정보가 표현할 때



### main 태그

* 웹사이트의 중요 정보



### aside 태그

* 페이지와 상관없는 부가적인 정보



## 3. 혼동되는 태그들

### article 태그 vs. section 태그

* article 태그
  * 블로그 포스트에서 포스트 하나
  * 신문 기사에서 기사 하나
  * 하나 그 자체를 묶어줄 때 사용
  * 독립적으로 보여줘도 문제가 없을 때 사용

* section 태그
  * article태그 안에 공통적으로 묶을 수 있는 것들
  * 연관있는 것을 묶는 태그



### i태그 vs. em태그

* i태그
  * 시각적으로만 이탤릭체
* em태그
  * 강조하는 이탤릭체



### b태그 vs. strong태그

* b태그
  * 시각적으로만 볼드체
* strong태그
  * 강조하는 볼드체



### ol태그 vs. ul태그 vs. dl태그

* ol태그
  * 순서가 있는 목록
* ul태그
  * 순서가 없는 목록
* dl태그
  * description list
  * 단어에 대해서 설명이 묶여있을 때 단어에 대한 목록을 나타냄
  * dt태그: 단어
  * dd태그: 단어의 의미



## 4. img태그 vs. css background-image

* img태그
  * 웹 페이지에서 하나의 중요한 요소로 자리를 잡을 때
* css background-image
  * 문서의 내용과는 별개로 스타일링 목적(배경 이미지)



## 5. button태그 vs. a태그

* button태그
  * 사용자의 특정 액션을 위할 때 사용
* a태그
  * 클릭 시 어디론가 이동할 때 사용



## 6. table태그 vs. css

* table태그
  * 많은 데이터를 행과 열로 표현
* css
  * 스타일링 목적
  * flex, grid

# Reference

[[드림코딩 by 엘리] HTML 태그 정리](https://www.youtube.com/watch?v=T7h8O7dpJIg)