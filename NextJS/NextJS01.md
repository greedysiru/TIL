# NextJS(1) - Initialize, Framework Vs. Library

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Initialize

```shell
npx create-next-app
```



## 2. Framework Vs. Library

* 라이브러리
  * 사용하는 것
  * 원하는 대로 코드를 작성
* 프레임워크
  * 추상화된 코드를 불러오는 것
  * 정해진 방식대로 구현
* 자유도의 차이
  * 라이브러리 > 프레임워크
* 대표적으로 NextJS의 경우 pages 디렉토리 안에서 파일을 기준으로 라우팅을 할 수 있음
  * NextJS가 **파일명**에 맞추어 라우팅을 해줌
* Inversion of Control(통제의 역전)
  * 개발자는 **라이브러리를 사용**
  * 개발자는 **프레임워크의 규칙을 지킴**

# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

