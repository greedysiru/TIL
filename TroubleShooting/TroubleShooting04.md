# 브라우저 호환성



## 1. 슬라이더 이미지가...!

2021년 12월 어느날, 서비스 중인 회사 웹 페이지의 슬라이더의 UI가 깨지는 이슈가 인입되었다.
진행중인 프로모션 이미지를 보여주는 슬라이더였는데, 슬라이더를 구성할 모든 이미지가 쭉 나열되어버리는 것이었다.




## 2. 상황 재현

해당 이슈의 상황 재현은 다행히도 어렵지 않았다. Safari에서만 재현이 되었고 Chrome에서는 정상적으로 슬라이더가 정상적으로 보였다. 즉 브라우저 호환성 이슈였다.



## 3. 원인 파악

각 브라우저에서 지원하는 CSS Property는 차이가 있다. 그러므로 슬라이더에 적용된 Property 중 Chrome에서는 지원하지만 Safari에서는 지원하지 않는 것을 찾아내야 했다.
의심되는 Property는 overflow였다. 보여지지 않아야할 요소가 보여지고 있기 때문이었다. 실제로, 당시 슬라이더에 적용된 CSS는 아래와 같았다. (예시 코드로 실제와는 상이)

```css
	.slider {
		...
		overflow: visible;
		overflow-x: clip;
}
```



위 CSS에서 [overflow 관련 MDN 문서](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-x)를 참고하면, clip이라는 value가 Safari에서 지원하지 않는다고 나와있다. 즉 `overflow-x: clip`이 문제였다.
왜 `clip` value를 부여했는 지는 히스토리도 문서가 없어서 정확히 알 수 는 없다. 우선 `clip` value의 역할은 `hidden`과 마찬가지로 컨텐츠를 padding에 맞추어 가림 처리를 한다. 단, `clip`은 코드를 사용한 스크롤링을 방지하는 것으로 되어있다. 아마 스크롤링을 방지하기 위해서 이러한 스타일을 정의한 것같다.





## 4. 해결방법

Safari에서 지원하지 않는 속성이 부여된 `overflow-x: clip`을 제거하였다. 그리고 `overflow: visible`에서` overflow: hidden`으로 스타일을 수정하였다. 수정한 스타일은 Safari에서도 Chrome에서도 잘 적용 되었다.



## 5. 느낀점

서비스 중인 회사의 웹사이트는 앱을 설치하지 않은 유저들도 접근이 가능하다. 즉, 다양한 브라우저 환경을 고려해야 한다. 만약, 광고 또는 관심으로 인해 유저가 웹 페이지를 들어왔을 때 UI가 깨지거나 일부 기능이 동작하지 않는다면 유저는 실망하고 나가버릴 것이다. 광고와 웹 페이지에 투입한 귀중한 시간과 자원이 허무하게 버려지는 것이다.
그러므로, 웹 개발자라면 MDN 표준을 지키며 코딩해야 한다. 유저에게 좋은 경험 그리고 우리 회사의 매출 성장을 위해서!



## Reference

* [overflow-MDN](https://developer.mozilla.org/ko/docs/Web/CSS/overflow)