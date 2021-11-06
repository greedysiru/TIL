# liftIO 2021(2)

> **국내의 함수형 개발자 커뮤니티를 빌딩하기 위한 첫 걸음**
>
> **김상현님, 김대현님, 김은민님, 박지수님**

# 1. Haskell Type-level 맛보기



## 1.1 Mu-Haskell

* 마이크로서비스를 위한 순수 함수형 프레임워크
* Mu-Scala
* GraphQL, gRPC, gRPC Client, Open API, REST 지원



## 1.2 Type-level Programming

* Haskell에서 type 구문은 type alias



## 1.3 Value(data)와 Type

* Haskell은 data 구문으로 Value 생성자들로 타입을 생성
* False Value 생성자로 생성한 Value는 Boolean Type



## 1.4 Type과 Kind

* Value가 Type에 속하는 것처럼 Type도 Kind에 속함



## 1.5 함수(Value)와 Type 생성자(Type)

* 함수는 Value이기 때문에 Type에 속함
* Type 생성자는 Type이기 때문에 Kind에 속함



## 1.6 Kind의 용도

* Type은 어디에?
  * 임의의 Value를 Type으로 컴파일 시점에 제한
  * 임의의 Value에 대한 Meta data - 코드를 읽기위한
* Kind는 어디에?
  * 임의의 Type을 Kind로 컴파일 시점에 제한
  * 임의의 Type에 대한  Meta data - 코드를 읽기 위한 + 런타임 활용



## 2. 느낀점

함수형 프로그래밍이라는 말을 취업 전 면접 준비를 하며 많이 접했었다. 그래서, 항상 무엇이 다르고 어떤 점이 좋은 것인지에 대한 호기심이 컸었다.

그러던 중, 부트캠프에서 같은 조원이셨던 분의 추천으로 인해서 함수형 프로그래밍 컨퍼런스인 liftIO2021을 알게되었고 곧바로 신청하게 되었다.

컨퍼런스는 코로나로 인해서 줌으로 진행되었다. 하지만, 참석한 모든 사람들의 함수형 프로그래밍에 대한 열정을 느끼기에는 충분했다. 좋은 기술에 대한 관심과 탐구, 이야기들이 이루어지는 것을 보며 큰 자극을 받았던 것 같다.

다만, 아쉬운 점은 내가 관련 지식이 많이 부족하여 듣기에는 수준이 높았던 것 같다. 그래도 더 공부해야겠다는 동기는 부여가 되어서 좋은 시간이었다.

