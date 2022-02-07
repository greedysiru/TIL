# Vue.js - 컴포넌트 디자인 패턴(Common)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 컴포넌트 디자인 패턴

* 유용한 기능 또는 확장성을 가지는 컴포넌트 설계 방식
* Common
* Slot
* Controlled
* Renderless



## 2. Common

* 기본적인 컴포넌트 등록, 통신 방식
* 자식 컴포넌트로 props를 전달
* 자식 컴포넌트에서 부모컴포넌트로 event를 emit
  * 부모에서 해당 event를 감지
* 1 way data flow
* Container - Presenter



### Props Validation

* props: 컴포넌트 간에 주고받는 데이터
* 유효성 검사를 할 수 있음
  * props의 타입
  * required

```Vue
// 부모로부터 props를 받는 자식 컴포넌트
...
<script>
export default {
  props: {
    name: {
      // 해당 props의 type
      type: String,
      // 해당 props가 필수인 경우 (필수가 아니면 false)
      required: true,
    }
  }
}
</script>
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)