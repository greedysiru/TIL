# JavaScript 노트 (02)

# jQuery 메소드 활용

## 메소드 활용하여 동적인 화면 만들기

### 보여지는 화면 아래 구하기(좌표)

> **$(window).scrollTop() + $(window).height();**

* **scrollTop()**: 선택된 요소의 수직 스크롤 바의 위치
* **height()**:선택된 요소의 길이
* 가장 위 + 보여지는 화면의 길이 = 보여지는 화면 아래



### 요소의 중간점 구하기(좌표)

>  **element.position().top + element.outerHeight() / 2;**

*  **position()** : 부모 엘리먼트를 기준으로 요소가 위치한 좌표값
* **outerHeight()**: 선택된 요소의 패딩, 테두리를 포함한 높이를 리턴



### 예시

```javascript
function scrollHandler() {
    const scrollBottom =  $(window).scrollTop() + $(window).height();
    // 모든 playlist 하나씩 살펴본 후, 중간 지점의 좌표가 bottom보다 작으면 해당 플레이리스트 보이게 하기
    const playlists = $('.playlist');
    playlists.each(function(){
      const playlistMiddle = $(this).position().top + $(this).outerHeight() / 2;

      if (playlistMiddle < scrollBottom){
          $(this).animate({'opacity': '1'}, 1500);
      }
    }) 
    }
```

* 사용자의 스크롤에 반응하여 요소들을 하나씩 나타나는 애니메이션