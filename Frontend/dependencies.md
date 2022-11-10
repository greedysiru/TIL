# dependencies vs. devDependencies



## 1. 개요

오늘 package.json의 dependencies와 devDependencies에 대해 질문을 받았다. 나는 내가 알고 있는 것을 토대로 이렇게 답변을 드렸다.

> dependencies는 production에 관여하는 의존성들입니다. 실질적으로 사용자가 접하는 코드를 구성하는 의존성들이라고 할 수 있습니다. 대표적인 예로 React.js를 들 수 있겠습니다.
> devDependecies는 development에서만 관여하는 의존성입니다. **개발단계 또는 빌드과정에서만 관여하는 의존성입니다.** webpack과 같은 번들링 패키지, babel과 같은 트랜스파일러 등이 그 예라고 들 수 있겠습니다.

그러나 엄밀히는 이 내용이 맞지 않다는 것을 듣게 되었다. 그리고 이와 관련해서 **빌드 배포, 패키지 배포**라는 키워드를 토대로 공부해보라는 조언을 받을 수 있었다.



## 2. package.json

### npm

npm은 node package manager의 약자이다. 약자 뜻풀이 그대로 Node.js를 기반으로한 프로젝트의 관리를 담당한다. 예를 들자면, 내가 만들고 있는 React 프로젝트에서 필요한 의존성들의 설치와 개발 서버 실행 및 배포까지 npm이 가능하게 한다.



### package.json

npm이 위와 같은 기능을 할때는 바로 package.json을 참조한다. 이 파일은 json 확장자이며, key와 value로 해당 프로젝트의 정보들을 표현한다. (프로젝트 명, 버전, 의존성 등)

npm 공식 문서에 나와있는 예시를 들자면 아래와 같다.

```Json
{
  "name": "my_package",
  "version": "1.0.0",
  "dependencies": {
    "my_dep": "^1.0.0",
    "another_dep": "~2.2.0"
  }
}
```



### dependencies & devDependencies

프로젝트 내에서 의존성을 추가하는 방법은 CLI에서 다음을 입력하면 된다

```shell
// dependencies install
npm install <example>

// devDependencies install
npm install <dev-example> --save-dev
```

위 명령이 실행되고 완료되면 root의 node_modules 디렉토리 안에 의존성의 실질적인 코드가 설치되고 아래와 같이 pakcage.json에 해당 패키지의 정보가 추가된다.

```Json
{
  "name": "my_package",
  "version": "1.0.0",
  "dependencies": {
    // 설치한 패키지 정보
    "example": "^1.0.0",
  },
  "devDependencies": {
    "dev-example": "^1.0.0",
  }
}
```

이제 package.json에 의존성 정보가 담겨있으니, 다른 동료들도 이를 기반으로 동일한 의존성을 갖출 수 있다. (이또한 npm의 강력한 기능이다.)



## 3. dependencies vs. devDependencies

[공식 문서](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file)에 따르면, 아래와 같이 설명되어 있다.

> - `"dependencies"`: Packages required by your application in production.
> - `"devDependencies"`: Packages that are only needed for local development and testing.

이러한 내용따라, 나는 당연히 devDependencies는 production에는 관여하지 않으므로 빌드에 포함되지 않을 것으로 알고 있었다. 하지만, webpack 관점에서는 틀렸다는 것을 알게 되었다.



### devDependencies in webpack

> [Difference between dependencies, devDependencies and peerDependencies](https://www.geeksforgeeks.org/difference-between-dependencies-devdependencies-and-peerdependencies/)

위 articles에 따르면, devDependencies라도 최종 코드 번들에 포함된다고 한다. 그러므로 webpack 관점에서는 dependencies와 devDependencies의 분류가 무의미해 보인다. 그래서 이 [article](https://jsramblings.com/do-dependencies-devdependencies-matter-when-using-webpack/)에서 처럼 모든 의존성을 dependencies에 넣는 경우도 있다고 한다.



### 빌드 배포 vs. 패키지 배포

하지만, **어떤 것을 배포하느냐**의 관점에서 분명 유의미한 차이가 있다. 제시받은 **빌드 배포와 패키지 배포**키워드를 토대로 조사해보니, 알아낼 수 있었다.

여기서 **빌드 배포**란, 통상적으로 우리가 진행하는대로 React 프로젝트를 세팅하고 관련된 의존성을 설치 한뒤 기능 구현을 완료한 후 해당 앱을 빌드, 배포하는 것을 뜻한다. **엄밀히는 애플리케이션 번들링(webpack docs 기준)**이라고 할 수 있다. **패키지 배포**는 라이브러리를 배포하는 것을 의미한다.

[Authoring Libraries - webpack](https://webpack.kr/guides/author-libraries/#authoring-a-library)에서 아래와 같은 내용이 있다.

> 라이브러리에 번들 되는 것을 막고 라이브러리가 비대해지는 것을 방지하기 위해 `lodash`를 `dependencies` 대신 `devDependencies`로 설치합니다.

즉, 패키지를 배포하는 관점에서는 devDependecies가 번들되지 않는 것이다! 그러므로, 패키지를 배포할 때 최대한 번들을 경량화하기 위해 의존성을 구분하는 것은 매우 중요하다고 할 수 있다.

그렇다면, 왜 빌드 배포의 경우 devDependecies또한 번들에 포함되는 것일까?

[`dependencies` vs `devDependencies` in Node.js – Which one should I use?](https://www.oddicles.net/blog/dependencies-vs-devdependencies-in-node-js-which-one-should-i-use/)에 따르면 아래와 같은 내용이 있다.

> A browser app built by webpack has no node dependencies. However, many projects not only serve but also build during production. It is true that this is an unconventional use of the word “build” for node developers (in scenario 1), as building typically refers to doing it before production instead of during. Instead of build and run in separate commands, it’s more like “build-to-run” in one.

요약하자면, 빌드된 웹 앱 자체는 노드 종속성이 없으나 대부분의 프로젝트들은 **앱을 생산하는 것에도 관여한다는 것이다.** 생각해보면, package.json에서 정의한 빌드 스크립트를 수도 없이 써왔다. 내가 지금것 진행했던 프로젝트들은 **앱을 빌드하는 프로젝트**이므로 devDependencies도 번들링되는 것이다! 엄밀히는 dependencies에 웹펙, 바벨, sass와 같은 것들이 위치하는 것이 옳다. (앱을 **빌드** 하는 프로젝트 이므로)



## 4. 결론

정리하자면 **우리가 통상적으로 진행하는 프로젝트는 앱을 빌드하는 프로젝트이므로 devDependencies에 webpack, babel이 위치하더라도 빌드에 관여하므로 번들링에 포함된다.** 그러므로 나의 설명은 틀렸다.

[webpack-issues](https://github.com/webpack/webpack/issues/520)에서 pbrn46이라는 개발자가 남긴 글을 읽어보니 devDependencies의 기준을 잡을 수 있었다. 그에 따르면, 빌드하는 프로젝트는 그 용도에 따라 빌드하는 의존성이 dependencies에 정리되어야 한다라고 주장했다. 그리고 Jest와 같은 테스트 라이브러리는 빌드에 전혀 관여하지 않기 때문이다.

나는 당연히, 빌드된 결과물인 앱을 기준으로 생각하였기 때문에 번들링 자체에 대해서도 혼동했던 것 같다. pbrn46라는 개발자의 글을 읽어보니 해당하는 관점이 타당하다고 생각이 들었고 당장 회사와 내 프로젝트에서 package.json을 정리해야겠다는 생각이 들었다. 종속성에 대해 깊은 생각을 하며 이와 관련한 개발자들의 좋은 아티클들과 열정적인 토론을 볼 수 있어서 다시 한 번 자극을 받을 수 있었다. 또 이러한 계기를 제공해준 키워드 제공자(?)분께도 감사드린다!!

# Reference

[npm Docs](https://docs.npmjs.com/)

[Difference between dependencies, devDependencies and peerDependencies](https://www.geeksforgeeks.org/difference-between-dependencies-devdependencies-and-peerdependencies/)

[Difference between dependencies and devDependencies](https://www.youtube.com/watch?v=FS31-9zbcLA)

[dependencies vs. devDependencies](https://www.oddicles.net/blog/dependencies-vs-devdependencies-in-node-js-which-one-should-i-use/)

[webpack-issues](https://github.com/webpack/webpack/issues/520#issuecomment-333279468)