# 정규표현식(4)

**본 내용은 드림코딩 by 엘리님의 정규표현식, 더이상 미루지 말자 강의를 토대로 작성하였습니다.**



## 1. 퀴즈

### 전화번호 찾기

```
/\d{2,3}[- .]\d{3}[- .]\d{4}/gm
```



### 이메일 선택하기

```
/[a-zA-Z0-9._+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9.]+/gm
```



### 유튜브 주소 찾기

```
/(?:https?:\/\/)?(?:www\.)?youtu.be\/([a-zA-Z0-9-]{11})/gm
```



## 2. JavaScript에서의 활용

```JavaScript
const regex = /(?:https?:\/\/)?(?:www\.)?youtu.be\/([a-zA-Z0-9-]{11})/;

const url = 'https://www.youtu.be/-ZClicWm0zM'

// 결과값이 배열로 return
const result = url.match(regex);
```



# Reference

[[드림코딩 by 엘리]정규표현식, 더이상 미루지 말자 ](https://www.youtube.com/watch?v=t3M6toIflyQ)

