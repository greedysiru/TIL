

# Vue.js - 프런트엔드, NVM

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. 프런트엔드

### 1.1 개발 절차

* 현대 웹 서비스의 개발 절차는 아래와 같음

1. 요구사항 : 어떤 것을 만들지
2. 서비스 기획 : 아이디어를 구체화
3. UI, UX 상세 설계
4. GUI 디자인 : 디자인 시안
5. 퍼블리싱 : 디자인 시안을 HTML, CSS 코드로 옮김(프런트엔드와 구분이 없을 수 있음)
6. 백엔드 API 개발
7. 프런트엔드 개발 : 화면단에 데이터를 연동
8. QA



### 1.2 프런트엔드 개발자의 역할

* 화면단 코드 작성
* 기획, 디자인, 퍼블리싱, 백엔드 개발자와 **소통**
  * 소통 능력 필수



## 2. NVM(Node Version Manager)

* 노드 버전 매니저
* Node.js의 버전을 관리하고 사용할 버전을 변경할 수 있음



### 2.1 NVM 설치

```shell
export NVM_DIR="$INSTALL_DIR"
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```



### 2.2 환경변수 설정

* ~/.zshrc에 아래와 같이 입력하여 저장

```shell
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```



### 2.3 Node.js 버전 설치

```shell
nvm install [버전명]
```



### 2.4 Node.js 버전 전환

```shell
nvm use [버전명]
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

[nvm](https://github.com/nvm-sh/nvm)