# [항해99 1기] [Chapter3-2] 주특기 심화 - 리액트 심화반 (2) (2021.3.27)



# 1. 프로젝트 세팅

## 개발환경 세팅

* 크롬 익스텐션
  * Redux devTools: 리덕스 사용시, 리덕스 액션에 따른 데이터의 변화를 볼 수 있다.
  * React developer Tools: 리액트 디버깅에 용이
* VSCode
  * react extension pack
  * prettier - code formatter



# 2.  기획서 쪼개기

## 2.1 기획서

* 프로토 타입 툴

  * 진행할 프로덕트의 화면을 공유하는 협업 툴
  * 제플린, XD, 피그마 등등을 사용

  

## 2.2 컴포넌트 쪼개기

* 각자의 방식이 있다.
* 편한 방식으로 쪼개는 것이 best
* 너무 짝게 만들면 만들기 어렵다.
* 너무 크게 만들면 재활용이 어렵다.
* 기획서를 보면서 컴포넌트를 쪼개기
  * 페이지마다 반복되는 부분 컴포넌트로 만들기



# 3. 프로젝트 진행하기

## 3.1 폴더 구조 잡기

* 이것 또한 각자의 방식이 있다.
* 이번 강의에선 아래와 같이 나누기

> **build: 빌드 후 결과물**
>
> **node_moduels: 설치한 패키지**
>
> **public: 가상 돔이 들어갈 빈 껍데기 html(index.html)이 들어있는 폴더**
>
> **src: 실제 소스코드가 있는 폴더**



## 3.2 src 폴더의 구조

* 실제 소스코드가 있는 src폴더의 구조는 아래와 같다.

> **/elements: button, input 등 최소단위 컴포넌트**
>
> **/components: elements의 컴포넌트를 조합해서 쪼갠 컴포넌트를 만든다.**
>
> **/pages: 페이지 시작점. components를 조합하여 페이지를 만든다.**
>
> **/redux: 리덕스 모듈과 스토어가 들어간다.**
>
> **/shared: 공용으로 사용할 코드가 들어간다. App.js, Cookie.js 등 시작점 또는 전역으로 사용할 객체는 이곳에 만든다.**



## 3.3 작업 순서

* 페이지부터 만들기
* 페이지에 들어갈 내용을 크게 쪼개서 컴포넌트 만들기
* 들어갈 내용 나누기
* 데이터를 받아올 내용과 가공이 필요한 내용을 분리
  * 페이지를 그리는데 필요한 defaultProps를 담아두어 데이터가 없어서 발생할 오류를 방지
* 최소단위 컴포넌트 만들기



## 3.4 defaultProps

* 유저의 정보가 필요한 컴포넌트를 만들 때 어떤 데이터가 필요할 지 생각하여 아래와 같이 defayltProps에 담아둔다.

```React
import React from "react";

const Post = (props) => {

    console.log(props);
    return (
        <React.Fragment>
            <div>img / nickname / time / btn</div>
            <div>contents</div>
            <div>image</div>
            <div>comment cnt</div>
        </React.Fragment>
    )
}

Post.defaultProps = {
  user_info: {
    user_name: "siru",
    user_profile: "임의의 img",
  },
  image_url: "임의의 url",
  contents: "고양이다",
  comment_cnt: 10,
  insert_dt: "2021-02-27 10:00:00",
};

export default Post;
```



# 4. 최소단위 컴포넌트 만들기

## 4.1 styled-components

* 컴포넌트의 스타일을 부여하기 용이한 패키지 설치

```shell
yarn add styled-components
```



## 4.2 Grid

* 컴포넌트들을 넣어서 정렬하기 용이한 최소 컴포넌트 정의하기

```react
import React from "react";
import styled from "styled-components";

const Grid = (props) => {
  // 상위 컴포넌트로부터 props를 전달 받기
  const { is_flex, width, margin, padding, bg, children } = props;

  // 전달받은 props를 별도의 변수에 저장
  const styles = {
      is_flex: is_flex,
      width: width,
      margin: margin,
      padding: padding,
      bg: bg,
  };
  return (
    <React.Fragment>
      {/* 전달받은 스타일의 정보가 있는 변수를 스프레드 문법으로 태그 안에 풀어넣기 */}
      <GridBox {...styles}>{children}</GridBox>
    </React.Fragment>
  );
};

// Grid의 defaultProps
// 부여할 것으로 예상되는 스타일들에 대해서 미리 값을 부여해 놓는다.
Grid.defaultProps = {
  chidren: null,
  is_flex: false,
  width: "100%",
  padding: false,
  margin: false,
  bg: false,
};

// styeld component
// porps로부터 전달받은 스타일정보들을 styled component로 적용할 수 있도록 한다.
const GridBox = styled.div`
  width: ${(props) => props.width};
  height: 100%;
  box-sizing: border-box;
  ${(props) => (props.padding ? `padding: ${props.padding};` : "")}
  ${(props) => (props.margin ? `margin: ${props.margin};` : "")}
  ${(props) => (props.bg ? `background-color: ${props.bg};` : "")}
  ${(props) =>
    props.is_flex
      ? `display: flex; align-items: center; justify-content: space-between; `
      : ""}
`;

export default Grid;
```

* 최소단위 컴포넌트는 상위 컴포넌트로부터 props를 전달받는다.
  * html에서 프로퍼티를 부여하는 것과 비슷한 맥락
* props에 대한 아래의 기본설정을 해야한다
* defaultProps설정
* 상위 컴포넌트로부터 전달받은 props들 담기
* 전달받은 props를 적용하기 위한 styled-component 설정하기
  * 삼항 연산자 응용하기
  * 최소단위 컴포넌트가 가져야할 기본 css 설정을 작성하기

# Reference

[스파르타코딩클럽 리액트 심화반](https://spartacodingclub.kr/online/react/plus)

