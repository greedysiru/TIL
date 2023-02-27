# Part 1. FLEX, SCSS 기초(FLEX를 활용한 효율적인 반응형 레이아웃)

* flex를 활용하여 여러 디바이스를 대응할 수 있는 반응형 레이아웃을 정의할 수 있음
* 모바일 우선 레이아웃 작업
  * 데스크탑 레이아웃이 간단한 사이트의 경우
* 데스크탑 우선 레이아웃 작업
  * 데스크탑 레이아웃이 복잡한 사이트의 경우



## 1. flex 기본 모바일 레이아웃

```HTML
<body>
  <main>
    <header>
    	<h1>header</h1>
    </header>
    
    <section>
    	<h1>content</h1>
    </section>
    
    <aside>
    	<h1>side</h1>
    </aside>
    
    <aside>
    	<h1>side</h1>
    </aside>
    
    <footer>
    	<h1>footer</h1>
    </footer>
  </main>
</body>
```



```SCSS
main {
  // 레이아웃 설정
  display: flex;
  // 가로축 기준으로 정렬, 줄바꿈 설정
  flex-flow: row wrap;
  
  // main tag 하위 모든 요소의 공통 스타일
  > * {
    padding: 10px;
    // 부모에 flex 속성 적용시 margin 겹침 현상이 발생하지 않음
    margin: 10px;
    // 컨텐츠들을 모두 같은 비율(1)로 설정
    flex: 1 100%;
  }
  
  header {
    height: 120px;
  }
  
  section {
    height: 300px;
  }
  
  footer {
    height: 80px;
  }
}
```



## 2. 모바일우선 반응형

* media query를 활용하여 기기별 대응
  * min-width로 지정

```SCSS
main {
  display: flex;
  flex-flow: row wrap;
  
  > * {
    padding: 10px;
    margin: 10px;
    flex: 1 100%;
    
    h1 {
      font-size: 30px;
    }
  }
  
  header {
    height: 120px;
  }
  
  section {
    height: 300px;
  }
  
  footer {
    height: 80px;
  }
}

// 태블릿의 기준을 600px 이후로 적용
@media screen and (min-width: 600px) {
  main {
    aside {
      // 태블릿에서 좌우로 적용 됨
      flex: 1;
    }
  }
}

// 데스크탑의 기준을 800px 이후로 적용
@media screen and (min-width: 800px) {
  main {
    section {
      // 데스크탑에서 더 큰 비율을 차지
      flex: 3;
      // 컨텐츠의 순서도 변경
      order: 2;
    }
    
    aside:nth-of-type(1) {
      order: 1;
    }
    aside:nth-of-type(2) {
      order: 3;
    }
    footer {
      order: 4;
    }
  }
}
```



## 3. 데스크탑우선 반응형

* 데스크탑 -> 모바일 순으로 스타일 정의
* 복잡한 데스크탑 레이아웃 -> 소거법으로 모바일 레이아웃 스타일 정의

```SCSS
main {
  display: flex;
  flex-flow: row wrap;
  
  > * {
    padding: 10px;
    margin: 10px;
    flex: 1 100%;
  }
  
  h1 {
    font-size: 30px;
  }
  
  header {
    height: 120px;
  }
  
  section {
    height: 300px;
    flex: 3;
    order: 2;
  }
  
  aside:nth-of-type(1) {
    flex: 1;
    order: 1;
  }
  aside:nth-of-type(2) {
    flex: 1;
    order: 3;
  }
  
  footer {
    heigh: 80px;
    order: 4;
  }
}

// 데스크탑 스타일을 기본으로 모바일 스타일을 정의하는 것이므로 max-width로 기준을 정의
@media screen and (max-width: 799px) {
  main {
    section {
      flex: 1 100%;
      order: 1;
    }
    aside {
      order: 2;
    }
  }
}

@media screen and (max-width: 599px) {
  main {
    aside {
      flex: 1 100%!important;
    }
  }
}
```



## 4. 결론

* `display: flex`로 기본 레이아웃을 정의
  * 기본 레이아웃의 기준은 상황에 따라 모바일 우선 또는 데스크탑 우선으로 정의
* 레이아웃을 정의하는 순서는 데스크탑 레이아웃의 복잡도를 기준으로 하기
  * 복잡도가 낮으면 모바일 우선 반응형 레이아웃을 적용
  * 복잡도가 높으면 데스크탑 우선 반응형 레이아웃을 적용
* `media query` 를 사용하여 기기 또는 브라우저 width에 따라 레이아웃을 