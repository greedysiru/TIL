# iOS Button Text Color



## 1. Button Text Color 이슈

2021년 9월 어느날, 서비스 중인 앱 내 버튼 컬러들이 blue로 바뀌어버린 이슈가 인입되었다. 일관적인 UI를 제공하기 위해 해당 이슈는 해결되어야했고 내가 그것을 맡게되었었다.



## 2. 상황 재현

다행히도, 상황을 재현하는 것은 어렵지 않았다. iOS에서만 해당 상황이 재현되었던 것이다. 그것도 최근에 업데이트를 한 기기에서. 때문에 원인을 파악하는 것도 쉽게할 수 있었다.



## 3. 원인 파악

원인은 2021년 9월 경에 iOS 15버전 업데이트였다. 이때 Safari도 대거 업데이트 되면서 엔진 Webkit 또한 업데이트 되었다.

[Text in HTML Buttons is blue on iOS 15](https://developer.apple.com/forums/thread/690529) 에 따르면, 버튼에 명시적인 color 지정이 없는 경우 User Agent Style Sheet에의해 버튼을 포함한 요소에 apple-system-blue을 color 값으로 들어가게 된다.

여기서 User Agent Style Sheet란, 각 브라우저마다 정한 CSS 기본 규칙이다.

즉, 원인을 정리하자면, iOS 15 업데이트에서 Safari, Webkit이 업데이트 되었는데 브라우저의 CSS 기본 규칙이 변경되어 버튼 색상이 기본값으로 blue로 들어가게 된 것이다.



## 4. 해결방법

아주 간단하다. Button 요소의 color를 명시적으로 정의하면 된다.



## 5. 느낀점

회사의 메인 앱은 Java, swift 단에서 webview로 React.js 코드를 실행시키는 하이브리드 앱방식이다. 때문에 OS 업데이트로 인해 엔진의 동작도 변경이 있는 경우 이슈가 발생할 수 있다. 그러므로 각 OS의 메이저 업데이트가 있으면 브라우저 엔진도 변경 사항이 있는지 확인을 하는 것이 좋을 것 같다!

그리고 매번 느끼는건데 애플은 참 마이웨이다...



## Reference

* [Text in HTML Buttons is blue on iOS 15](https://developer.apple.com/forums/thread/690529) 
* [stackoverflow.com/questions/12582624/what-is-a-user-agent-stylesheet](https://stackoverflow.com/questions/12582624/what-is-a-user-agent-stylesheet)
