# [스파르타코딩] 웹개발 종합반 항해 1기 5주차 (2)(2021.2.5 ~ 6)



**상세 내용 [블로그](https://greedysiru.tistory.com/171) 참고**



# 1. 내 프로젝트를 서버에 올리기

* 웹 서비스를 런칭하고 클라이언트의 요청에 답하기 위해서는
  * 컴퓨터가 **항상** 켜져있고 프로그램이 실행되어 있어야 한다.
  * 모두가 접근할 수 있는 공개 주소인 공개 IP 주소(Public IP Address)로 나의 웹 서비스에 **접근할 수 있어야 한다.**
* 개인 컴퓨터로는 실현하기 어려우므로  **AWS라는 클라우드 서비스를 이용한다.**



## IP 주소와 포트

* 실제로 우리가 접속하는 컴퓨터는 숫**자로 되어있는 주소(IP 주소)**가 붙어있다.
* **문자로 이루어진 URL은 DNS 시스템으로 IP주소를 바꾼 것이다.**
  * DNS : Domain Name System
  * IP주소 : 컴퓨터가 통신할 수 있도록 컴퓨터마다 가지는 고유한 주소. 네트워크가 가능한 모든 기기가 통신할 수 있도록 가지고 있는 특수한 번호. 서버는 하나의 주소를 가지고 있다.
  * 포트(port) : 하나의 IP에 여러 포트가 있다. 하나의 포트에서 하나의 프로그램을 실행시킬 수 있다.



# 2. AWS 서버 구매하기

## AWS EC2 서버

* **서버를 운영할 수 있는 클라우드 서비스**
* Ununtu OS
* Mac Os의 경우 **SSH**가 있어서 명령어로 바로 접근 가능
* **SSH**: Secure Shell Protocol
  * 다른 컴퓨터에 접속할 때 쓰는 프로그램
  * 보안이 뛰어나다.
  * 접속할 컴퓨터가 **22번 포트**가 열려있어야 접속 가능
  * **AWS EC2의 경우, 22번 포트가 열려있다.**



## 쉘 명령어

* **리눅스(우분투)는 쉘 명령어를 통해 OS를 조작**



### 쉘 주요 명령어

`ls` : 내 위치의 모든 파일을 보여준다.

`pwd` : 내 위치(폴더의 경로)를 알려준다.

`mkdir` : 내 위치 아래에 폴더를 하나 만든다.

`cd [갈 곳]` : 나를 [갈 곳] 폴더로 이동시킨다.

`cd ..` : 나를 상위 폴더로 이동시킨다.

`cp -r [복사할 것] [붙여넣기 할 것]` : 복사 붙여넣기

`rm -rf [지울 것]` : 지우기

`sudo [실행 할 명령어]` : 명령어를 관리자 권한으로 실행 

`sudo su` : 관리자 권한으로 들어간다. (나올 때는 exit로 나옴)



### 터미널에서 EC2 리눅스 인스턴스 접속하기

`sudo chmod 400 [키페어]`

`ssh -i [키페어]ubuntu@[인스턴스 퍼블릭 IPv4 주소]` 



# 3. 서버 세팅하기

## filezilla

![web10-1](images/web10-1.png)

* 서버를 아래처럼 세팅 후 연결한다.
  * File - New site를 눌러서 이름을 설정
  * **프로토콜** : STFP
  * **호스트** : 퍼블릭 IPv4 주소
  * **포트** : 22
  * **로그온 유형** : 키파일
  * **사용자** : ubuntu
  * **키파일** : 경로 입력



### 업로드 / 다운로드

![web10-2](images/web10-2.png)

* 좌측은 나의 컴퓨터, **우측이 서버 컴퓨터**이다.
* **드래그앤드랍으로 파일을 업로드 / 다운로드할 수 있다.**



### 파이썬 실행해보기

* 파이썬 파일을 업로드 후 EC2 콘솔창에서 실행할 수 있다.

```shell
python3 test.py
```



## 서버 환경 통일하기

* 구매한 서버에 필요한 세팅(업그레이드, DB설치, 명렁어 통일 등)을 할 수 있다.



### 파일로 세팅하기

 [initial_ec2.sh](ec2_setting/initial_ec2.sh) 

* 필요한 세팅을 할 수 있는 shell 명령어 파일을 터미널에서 실행하여 한 번에 할 수 있다.
* 파일을 서버에 업로드 후, 아래 명령어를 입력한다.

```shell
sudo chmod initial_ec2.sh
.initial_ec2.sh
```



### 서버 환경 세팅(코드 설명)

* 한국 시간 세팅

```shell
sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
```

* 파이썬 (python3 -> python)

```shell
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
```

* pip (pip3 -> pip)

pip3 설치

```shell
sudo apt-get update
sudo apt-get install -y python3-pip
```

pip3 -> pip

```shell
sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1
```



# 4. flask 서버를 실행해보기

* flask 서버 파일을 실행하기 위해서 pip로 패키지를 설치한다.

## pip

* **파이썬의 패키지들을 설치할 수 있는 라이브러리**
* 아래를 입력하여 플라스크를 설치한다.

```shell
pip install flask
```



# 5. AWS에서 포트 열어주기

* AWS EC2에서 자체적으로 포트를 열어줘야 서버를 이용할 수 있다.
* EC2 관리 콘솔에서 보안 그룹에 들어간다.![web10-3](images/web10-3.png)

* 인바운드 규칙 편집을 들어가서 아래의 세 포트를 추가한다.
  * 프로토콜은 전부 **TCP**, 소스정보는 **위치무관**으로 설정
  * **80포트** : HTTP 접속을 위한 기본포트
  * **5000포트** : flask 기본포트
  * **27017포트** : 외부에서 mongoDB 접속을 하기위한 포트
* 추가 후 아래 화면이 나오는지 확인

![web10-4](images/web10-4.png)



# 6. 원페이지 쇼핑몰 업데이트

## Robo 3T

* **Connections -> Create** 클릭
* 접속정보 세팅
  * **Adress에 EC2 IP 입력**
  * **포트는27017**

![web10-5](images/web10-5.png)

* 이후, **Authentication 탭**에서 **Perform authentication 체크 ,생성한 계정의 아이디와 비밀번호를 입력하고 저장**



## MongoDB 접속 세팅

* 업로드할 app.py의 접속 세팅을 변경한다.
* pymongo 코드를 아래로 변경

```python
client = MongoClient('mongodb://test:test@localhost', 27017)
```

* 이후, filezila에서 **home/ubuntu에 업로드한다.**



## 실행하기

* pymongo 설치

```shell
pip install pymongo
```

* 실행

```shell
python app.py
```

* 브라우저 접속 : http:// ec2 아이피:5000/



# 7. 포트포워딩

* 포트 번호를 떼고 접속을 하여도 웹 페이지에 접속할 수 있다.

## 기본개념

* **http 요청에서는 80포트가 기본**이다. 때문에, **:80을 붙이지 않아도 자동으로 연결**된다.
* **포트포워딩**으로 **80포트로 오는 요청**을 **플라스크의 포트인 5000포트로 전달**할 수 있다.



## 쉘 명령어

```shell
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 5000
```



# 8. nohup 설정하기

* SSH 접속을 끊어도 서버가 계속 돌게 한다.

## 쉘 명령어

* 서버 돌아가게 하기

```shell
nohup python app.py &
```

* 서버 프로세스 보기

```shell
ps -ef | grep 'app.py'
```

* 서버 종료하기 - 강제종료

```shell
kill -9 [pid값]
```



# 9. 도메인 구매 / 연결하기

* [가비아](https://my.gabia.com/service#/)에서 도메인을 구입 후 연결할 수 있다.

## 도메인 구입

* 도메인을 구입하는 것은 **네임서버를 운영하는 업체에 IP와 도메인 매칭 유지비를 내는 것이다.**



## 도메인 연결

*  https://my.gabia.com/service#/
* **DNS 관리툴 -> 도메인 연결 -> DNS 설정**
* 아래와 같이 입력한다.
  * **호스트** : @
  * **값 / 위치** : ec2 IP

![web10-6](images/web10-6.png)



# 10. og 태그 만들기

* 카톡 / 페이스북 / 슬랙 등에서 페이지를 공유했을 때, og태그를 사용하면 그것을 보여준다.

![10-7](images/10-7.png)

## og 태그 삽입

* static 폴더에 원하는 이미지를 넣는다.**(800 * 400)**
* 프로젝트 **HTML의 head에 아래의 코드를 입력**

```HTML
<meta property="og:title" content="내 사이트의 제목" />
<meta property="og:description" content="보고 있는 페이지의 내용 요약" />
<meta property="og:image" content="{{ url_for('static', filename='ogimage.png') }}" />
```



## og 태그 초기화

* 변경한 og태그를 적용한다.

>  https://developers.facebook.com/tools/debug/
>
>  https://developers.kakao.com/tool/clear/og

# Reference

**스파르타코딩 - 웹개발 종합반**