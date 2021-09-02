

# CSS 방법론

**본 내용은 10분 테코톡 동동님의 강의를 토대로 작성하였습니다.**



## 1. CSS란?

* HTML, XML 문서의 스타일을 나타내는 언어
* 문서의 구조와 스타일을 분리하여 HTML, XML 문서의 각 요소를 꾸미는 것이 역할



## 2. CSS의 등장 이전과 이후

### 등장 이전

* 각 요소의 전용 속성이나 style 속성으로 스타일을 지정
* 문제점
  * 여러 페이지에 같은 스타일 요소를 적용 시, 그만큼 반복해야 한다.
  * HTML은 본래 문서 구조를 의미하므로 바람직하지 않다.

```HTML
<font color="#00f">텍스트</font>
<p style="color: #f00; font-size: 18px">
  문단
</p>
```



### 등장 이후

* CSS 파일과 HTML 문서를 분리하여 사용 가능
* HTML문서에서의 스타일 관련 코드를 분리할 수 있게 됨
* 여러 페이지에 같은 스타일을 적용시키기 용이

```CSS
/* p태그의 스타일을 설정 */
p {
  color: black;
  font-size: 18px;
}
```



## 3. CSS의 문제점

* CSS는 모든 것이 전역 범위이므로 스타일링 간에 간섭할 가능성
* CSS파일이 분리되어 있어도 이 파일들을 읽은 HTML에서는 모든 스타일링이 동일한 범위 안에 존재
* 웹 사이트가 복잡해 지면서, 유지 보수 가 용이한 CSS를 작성하기 위해 방법론들이 제시 됨



## 4. OOCSS

* Object Oriented CSS: 객체 지향 CSS
* 니콜 설리번(Nicole Sullivan)이 제창
* 주요 발상
  * 레고처럼 자유로운 조합이 가능한 모듈의 집합을 만든다.
  * 그 모듈을 조합해 페이지를 마든다.
  * 그리하여 신규 페이지를 만드는 경우에도 기본적으로 추가적인 CSS를 만들 필요가 없다.
  * OOCSS의 역사는 매우 길지만, 명확하게 규칙이라고 불리는 것이 많지 않음
  * 다른 CSS 방법론들은 기본적으로  OOCSS를 참조
  * OOCSS 한 가지만으로 실직적으로 CSS 설계를 하는 것은 현실적이지 않음



### 레고와 같은 모듈을 구현하기 위한 두 가지 원칙

* 스트럭처(구조)와 스킨(화면)의 분리
  * 스트럭처: 공통적인 부분
  * 스킨: 다른 부분
  * 유지, 보수가 용이
  * 중복을 피하면서 간단하게 새로운 요소를 추가하기 쉽다.
* 컨테이너와 콘텐츠 분리
  * 컨테이너: 영역
  * 콘텐츠: 모듈
  * 특정한 컨텍스트에 지나치게 의존하지 않는다.



### 스트럭처(구조)와 스킨(화면)의 분리 예시

* HTML

```HTML
<main id="main">
	<button class="btn-accept">
    기본 버튼
  </button>
  <button class="btn-cancle">
    취소 버튼
  </button>
</main>
```

* CSS

```CSS
/* 스트럭쳐 */
#main .btn {
  width: 10rem;
  max-width: 100%;
  padding: 0.75rem;
}

/* 스킨 */
#main .accpet {
  background-color: teal;
  color: white;
}

#main .cancel {
  background-color: white;
  color: teal;
}
```



### 컨테이너와 콘텐츠 분리 예시

* HTML

```HTML
<!-- 컨테이너 -->
<main id="main">
  <!-- 콘텐츠들 -->
	<button class="btn-accept">
    기본 버튼
  </button>
  <button class="btn-cancle">
    취소 버튼
  </button>
</main>
```

* CSS
  * 모듈을 가능한 특정한 영역에 의존하지 않도록 선택자 수정

```CSS
/* 스트럭쳐 */
.btn {
  width: 10rem;
  max-width: 100%;
  padding: 0.75rem;
}
```



## 5. SMACSS

* Scalable and Modular Architecture for CSS
* 조나단 스눅 (Jonathan Snook)이 제창
* 프로젝트에서 고려해야 하는 대부분의 CSS 규칙을 포함
* 각 규칙이 엄격하지 않아 유연하나, 경우에 따라 규칙이 너무 유연하여 실제 코드의 지침으로 삼기 어려움
* 모듈 규칙에 OOCSS를 적용하거나 BEM의 규칙을 일부 적용하는 등 다른 설계 기법과 조합하는 경우가 많음
* CSS 코드를 그 역할에 따라 분류한 것이 특징
  * 베이스(Base)
  * 레이아웃(Layout)
  * 모듈(Module)
  * 스테이트(State)
  * 테마(Theme)



### 베이스(Base) 규칙

* 프로젝트의 표준 스타일을 정의
  * 바탕화면 색 등
* 리셋 CSS, 노멀라이즈 CSS
  *  브라우저 간의 스타일 차이 제거 위해 사용



### 레이아웃(Layout)

* 헤더, 메인 영역, 사이드 바 등 웹사이트의 레이아웃을 구성하는 큰 모듈에 관한 규칙
* 대부분 특정 페이지에서 한 차례만 사용하므로 ID 선택자를 활용한 스타일링을 허용
  * 반복적으로 사용하는 모듈의 경우 class 선택자를 이용
* 특정한 페이지에서만 레이아웃을 변경하고 싶은 경우
  * 손자 셀렉터를 이용해 레이아웃 모듈의 스타일을 덮어씀

```HTML
<header id="header">헤더</header>
<main id="main">
	메인
  <section class="section">1</section>
  <section class="section">2</section>
</main>
<footer id="footer">푸터</footer>
```



### 모듈(Module) 규칙

* 타이틀(Title), 버튼(Button), 카드(Card), 내비게이션(Navigation)등
* 모든 모듈은 레이아웃 규칙 안에 배치되는 것을 가정
* 다른 페이지로 이동하거나 다른 레이아웃 안에 삽입하더라도 형태가 부서지거나 달라지지 않고 사용할 수 있어야 함
  * 특정 컨텍스트에 지나치게 의존하지 않도록 작성
* 한 페이지 내에서 반보갷서 사용되는 상황을 가정
  * 모듈의 루트 요소에는 반드시 클래스 선택자 사용
* 가급적 요소 선택자 사용하지 말 것
  * 요소 선택자를 사용하는 경우 손자 선택자가 아닌, 자녀 선택자를 사용

```HTML
<di class="media">
	<figure>
  <p> 모듈 </p>
  </figure>
</di>
```

```CSS
.media {
  width: 200px;
}

.media > figure {
  backgorund-color: teal;
}
```



### 스테이트(State) 규칙

* 기존 스타일을 덮어쓰거나 확장하기 위해 사용
* 기존 스타일을 모두 덮어써서 스테이트 스타일을 반영하는 것을 기대하기 때문에 필요한 경우에는 **!important** 사용도 권장
* 스테이트는 레이아웃이나 모듈에 할당
* 스테이트 규칙에 따른 클래스 이름은 모두 is- 접두사를 붙임
* 스테이트는 JavaScript에 의존

```CSS
.is-tab-active {
  background-color: blue;
  color: white;
}
```

```JavaScript
// .tab 클래스 요소는 클릭시에 .is-tab-active라는 클래스가 생성/제거 된다.
document.qureySelector(".tab").addEventListener("click", (event) => {
  event.target.classList.toggle("is-tab=active");
})
```



### 테마(Theme) 규칙

* 사이트 내 레이아웃이나 색상, 텍스트 처리 등을 일정한 규칙에 따라 덮어쓰는 것
* 기존의 다양한 스타일링이 덮어쓰기의 대상이 된다.
* 예시) 다크모드 전환, 테마 컬러 변경 등
* theme 접두사를 붙일 것을 권장



## 6. BEM

* Block, Element, Modifier
* 러시아의 Yandex 사가 제창한 컴포넌트 기반 웹 개발 접근법
* UI를 독립된 블록으로 분리함으로써 복잡한 페이지에도 간단하고 신속하게 개발을 수행하는 것이 목적
* 엄격하고 강력하여 널리 사용
* BEM의 모든 엔티티는 동일한 상세도를 가진다.
* Cascading 원칙에 따라 마지막에 선언한 css속성을 적용하는 방식은 금지된다.
* 명명법
  * Block, Element, Modifier 이름 사이를 하나의 언더바로 구분
  * MindBEMding: Modifier 전후의 구분 문자를 언더바 한 개에서 하이픈 두개를 사용하여 구분하는 방식



### Block

* 재사용할 수 있는 기능적으로 독립된 페이지 구성요소
* BEM을 사용할 때는 ID 선택자 또는 요소 선택자를 사용하면 안 됨
* Block 이름은 상태(state)가 아닌 용도(purpose)를 나타냄
* Block은 환경에 영향을 미치지 않아야 함
  * Block 자체에 대한 외부 지오메트리(margin) 또는 Block의 위치(position)를 설정하지 않아야 함
* Block은 서로 중첩될 수 있다.
  * 포함될 수 있다.

```HTML
<!-- 시맨틱한 의미를 사용 O -->
<div class="error"></div>

<!-- 상태를 나타냄 X -->
<div class="red-text"></div>
```



### Element

* Block의 복합 부품으로 Block과 별도로 사용할 수 없음
* Element 이름은 상태(state)가 아닌 용도(purpose)를 나타냄
* 명명법
  * **block-name__element-name**
* 항상 Block의 부분이어야 한다.
* 모든 Block이 Element를 가지는 것은 아니다.
* Element는 서로 중첩될 수 없다.
  * 다른 Element의 부분이 될 수 없다.

```HTML
<form class="search-form">
  <input class="search-form__input" />
  <button class="search-form__button">Search</button>
</form>
```



### Modifier

* Block 또는 Element의 모양, 상태 또는 동작을 정의
* Modifier 이름은 모양(apperance), 상태(state), 동작(behavior)를 나타낸다.
* Modfier는 홀로 사용되지 않는다.



### Modifier의 유형

1. Boolean

   * Modifier 유무만 중요하고 그 값이 무관할 때 사용: disabled, focused
   * Boolean modifier가 있으면, 해당 값이 참으로 간주됨
   * 명명법: **block-name_modifier-name**, **block-name__element-name_modiffier-name**

   ```HTML
   <form class="search-form search-form_focused">
     <input class="search-form__input" />
     <button class="search-form__button search-form__button_disabled">
       Search
     </button>
   </form>
   ```

2. key-value

   * Modifier 값이 중요한 경우에 사용: size_s, theme_islands
   * 명명법: **block_name--modifier-name_modifier_value**, **block-name__element-name_modifier-name_modifier_value**
   * 동일한 유형의 Modifier를 동시에 사용할 수 없음

   ```HTML
   <form class="search-form serach-form_theme_islands">
     <input class="serach-form__input" />
     <button class="serach-form__button serach-form__button_size_m">
       serach
     </button>
   </form>
   ```



### Mix

* Block과 Element가 하나의 HTML 요소에 존재하는 것을 의미
* 코드 중복을 피하면서 여러 BEM엔티티의 동작과 스타일을 결합
* 기존 BEM 엔티티를 기반으로 의미상 새로운 인터페이스 컴포넌트를 작성
* 가급적 상세도를 높이지 않고 Block의 독립성 유지

```HTML
<div class="header">
  <!-- 두 블록의 결합도를 높이지 않고 독립적으로 스타일을 정의해야함 -->
  <div class="serach-form header__search-form"></div>
</div>
```



## 7. 새 CSS 방법론

### 기존 CSS 방법론의 문제점

* CSS가 HTML 구조와 강하게 결합
* HTML에 의존하는 CSS
  * HTML에서 스타일이 필요한 요소에 클래스명을 부여
  * 클래스명이 부여된 요소에 대해 CSS에서 스타일링
* CSS에 의존하는 HTML
  * CSS에서 HTML과 독립적으로 스타일을 선언
  * HTML에서는 선언되어 있는 스타일에 한하여 마크업 작성



### Utility-Frist CSS / Functional CSS

* 시멘틱하고 컨텍스트에 의존하지 않는 CSS 작성하지 않음
* 클래스명만 보아도 CSS 속성의 값을 바로 유추할 수 있도록 단 하나의 속성과 값을 나타내는 CSS를 사전에 미리 정의
* 미리 정의된 클래스를 마치 HTML 요소에 제공하는 API로 생각하여 API(클래스명)을 HTML에 조합해서 사용
* inline style고 ㅏ다른 점
  * 아무 값이나 지정할 수 없고 사전에 정해진 리스트에서 골라야 하므로 전체적인 일관성을 높일 수 있음
  * hover, focus 등의 의사 클래스 셀렉터도 사용
  * media query를 사용할 수 있어 반응형 디자인 대응이 수월
* 널리 알려진 Utility-Frist CSS
  * Tailwind CSS
  * Tachyons
  * Atomic CSS

```HTML
<button class="w-1/2 rounded-md border border-gray-300">
  Button
</button>
```



### State Of CSS

* State of JS와 같이 CSS 최신 트렌드에 대한 서베이를 수행하여 그 결과를 보여줌
* CSS 프레임워크
* CSS 방법론
* 시상식



# Reference

[[10분 테코톡] 동동의 CSS 방법론](https://www.youtube.com/watch?v=B70h37mpD74)