---
layout: single
title: "D+36(37) HTTP / 네트워크 기초, REST API"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

http와 rest api 정리글.

## 1. 클라이언트 서버-아키텍쳐(2 Tier Architecture / 2티어 아키텍쳐)

리소스가 존재하는 곳과, 리소스를 사용하는 앱을 분리시킨 것.

① 클라이언트: 리소스를 사용하는 앱

② 서버: 리소스를 제공하는 주체(serve + r). 리소스를 전달하는 역할(이지만 단순히 전달만 하는 것은 아님).

⇒ 클라이언트와 서버는 요청과 응답을 주고 받는 관계이다. 클라이언트-서버 아키텍처에서는 요청이 선행되고, 그 후에 응답이 온다(요청 없는 응답은 없다).

③ 데이터베이스: 리소스를 저장하는 공간. ⇒ 기존 2티어 아키텍쳐에 데이터베이스가 추가된 것을 3티어 아키텍쳐라고 한다.

### 1-1. 클라이언트와 서버의 종류

① 클라이언트: 보통 플랫폼에 따라 구분된다.

‣ 웹사이트 / 웹 앱: 브라우저를 통해 주로 이용하는 웹 플랫폼에서의 클라이언트

‣ 스마트폰 / 태블릿(iOS나 안드로이드와 같은)플랫폼,

데스크탑 플랫폼(윈도우와 같은)에서 이용하는 앱도 클라이언트가 될 수 있다.

② 서버: 무엇을 하느냐에 따라 종류가 달라진다.

‣ 파일 서버: 파일을 제공하는 앱, 웹 서버는 웹사이트에서 필요로 하는 정보들을 제공하는 앱(이후 주로 만들게 될 서버)

‣ 메일 서버: 메일을 주고 받을 수 있도록 도와주는 앱 ⇒ 데이터베이스도 데이터 제공자로서 일하므로 일종의 서버라고 볼 수 있다.

![](https://blog.kakaocdn.net/dn/bdosel/btroEpb2XBO/elWWeWFfZbSpW8bS03EPyK/img.png)

(웹 아키텍쳐의 전반적인 설명)

웹 아키텍쳐의 전반적인 설명 ⇒ 클라이언트는 인터넷에 연결된 사용자의 디바이스, 또는 웹에 접근할 수 있는 소프트웨어를 뜻한다.

대표적인 예로 브라우저가 있는데, 브라우저는 HTML, CSS, JavaScript 등으로 작성된 코드를 내부 엔진으로 해독하여 사용자가 쉽게 이해할 수 있는 형태의 컨텐츠로 보여주는 역할을 한다.

서버는 클라이언트가 어떤 자원을 요청하면 해당 요청을 적절하게 처리하는 역할을 하고, 클라이언트는 서버의 자원을 어떻게 사용할 수 있는지 명시해 둔 인터페이스 API에 따라 요청을 전송한다.

이렇게 클라이언트와 서버가 서로 요청과 응답을 주고받을 수 있는 것은 HTTP 라는 통신 규약 덕분이다.

✅ 프론트엔드와 백엔드의 차이?

아키텍처에서 어떤 분야를 다루는지에 따라 구분된다.

![](https://blog.kakaocdn.net/dn/bClt4Q/btrrU9wnrKw/COJsSckAlcEcNQRWWKtkEk/img.png)

‣ 프론트엔드 개발자: 클라이언트처럼 사용자가 직접 눈으로 보고, UI를 클릭 또는 터치하는 등의 상호작용을 할 수 있는 앱을 주로 개발

‣ 백엔드 개발자: 사용자 눈에 보이지 않지만 상품 정보를 API로 노출한다던지, 로그인/로그아웃, 권한 관리 등의 사용자 인증을 주로 다루는 개발자. 데이터베이스 등의 시스템 설계까지 도맡아서 하는 경우도 있음.

## 2. HTTP를 이용한 클라이언트-서버 통신과 API

‣ 클라이언트-서버 아키텍처에서는 서버 마음대로 클라이언트에 리소스를 전달하지 않지만, 간혹 서버가 일방적으로 클라이언트에게 전달하는 경우가 있다(자세한 내용은 나중에).

① 프로토콜: 통신 규약, 클라이언트와 서버 간의 통신을 하기 위한 약속(통신을 할 수 있는 다양한 방법 존재)

‣ 웹 애플리케이션 아키텍처에서는 클라이언트와 서버가 서로 HTTP라는 프로토콜을 이용해서 서로 대화를 나눈다.

→ [HTTP 메시지](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages): HTTP를 이용해 주고받는 메시지. 서버와 클라이언트 간에 데이터가 교환되는 방식.

✷ 주요 프로토콜

‣ OSI 7 Layers: 컴퓨터 시스템이 네트워크를 통해 통신하는 데 사용하는 7개의 계층. 해당 프로토콜이 어떤 계층에 속해있는 지 표시해줌.

(7. 응용 계층)

| 프로토콜 이름 |                        설명                        |
| :-----------: | :------------------------------------------------: |
|     HTTP      |  웹에서 HTML, JSON 등의 정보를 주고 받는 프로토콜  |
|     HTTPS     |          HTTP에서 보안이 강화된 프로토콜           |
|      FTP      |                 파일 전송 프로토콜                 |
|     SMTP      |           메일을 전송하기 위한 프로토콜            |
|      SSH      |  CLI 환경의 원격 컴퓨터에 접속하기 위한 프로토콜   |
|      RDP      | 윈도우 계열의 원격 컴퓨터에 접속하기 위한 프로토콜 |
|   WebSocket   |      실시간 통신, Push 등을 지원하는 프로토콜      |

(4. 전송 계층)

| 프로토콜 이름 |                                     설명                                     |
| :-----------: | :--------------------------------------------------------------------------: |
|      TCP      |    HTTP, FTP 통신 등의 근간이 되는 인터넷 프로토콜. 양방향으로 작동한다.     |
|      UDP      | 단방향으로 작동하는, 훨씬 더 빠르고 단순하지만 신뢰성이 낮은 인터넷 프로토콜 |

② API(Application Programming Interface)

프로그램들이 서로 상호작용하는 것을 도와주는 매개체.

→ 서버가 클라이언트에게 리소스를 잘 활용할 수 있도록 인터페이스(interface)를 제공해줘야 하는 것

→ 앱이 요청할 수 있고 프로그래밍 가능한 인터페이스.

→ 응용 프로그램에서 사용할 수 있도록 운영체제 / 프로그래밍언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스.

⇒ 서버가 리소스 전달을 위해 구축해놓은 인터페이스.

✷ 인터넷에 있는 데이터를 요청할 때는 HTTP라는 프로토콜을 사용, 주소(URL, URI)를 통해 접근할 수 있게 된다.

ex) API에 대해 이해하기 쉬운 카페 메뉴 주문 예제

<mark style='background-color: #dcffe4'>?</mark>

|                                  요청                                  |                                                                                URL                                                                                 |
| :--------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                         카푸치노 한 잔 주세요                          |                                                                         /coffee/cappuccino                                                                         |
|                      샹그리아 에이드 한 잔 주세요                      |                                                                          /ade/sangriaade                                                                           |
|                   아포가토 <mark>두 잔</mark> 주세요                   |                                       coffee/affogato<mark style='background-color: #dcffe4'>?</mark><mark>quantity=2</mark>                                       |
| 아메리카노 <mark>두 잔</mark> 전부 <mark>바닐라 시럽</mark> 넣어주세요 | /coffee/americano<mark style='background-color: #dcffe4'>?</mark><mark>quantity=2</mark><mark style='background-color: #dcffe4'>&</mark><mark>syrup=vanilla</mark> |

⇒ <mark>두 잔 / 바닐라 시럽</mark> 등 옵션이 들어가는 것들을 <mark>파라미터<mark> 라고 한다.

⇒ <mark>파라미터</mark>를 사용하기 위해 <mark style='background-color: #dcffe4'>물음표(?), & 기호</mark>를 사용

[✷ 쿼리와 파라미터의 차이](https://react.vlpt.us/react-router/02-params-and-query.html)

[✷ 쿼리 스트링 파라미터(query-string-parameter)](https://velog.io/@pear/Query-String-%EC%BF%BC%EB%A6%AC%EC%8A%A4%ED%8A%B8%EB%A7%81%EC%9D%B4%EB%9E%80)

![](https://blog.kakaocdn.net/dn/dzYSuv/btrr2TOLLaR/Xk8R1LKtsbJcPhdkDZC4c1/img.png)

(출처: 코드스테이츠)

③ HTTP 디자인의 Best Practice - 사용자 관리 API

ex)

|             요청             | URL 디자인 | 사용하는 메소드 |
| :--------------------------: | :--------: | :-------------: |
|    모든 사용자 조회(Read)    |   /user    |       GET       |
|    새 사용자 추가(Create)    |   /users   |      POST       |
| 1번 사용자 정보 갱신(Update) |  /users/1  | PUT( or PATCH)  |
| 1번 사용자 정보 삭제(Delete) |  /users/1  |     DELETE      |
|  1번 사용자 정보 조회(Read)  |  /users/1  |       GET       |

URL 디자인은 비교적 단순하나 HTTP 요청에는 HTTP 메소드의 종류가 존재한다.(마치 CRUD 같은, 이것들의 각각의 행동과 일치하는)

→ 위의 예시에서는 그저 리소스를 달라고(GET) 요청했지만, 사용자 관리 API에서는 사용자를 추가해 달라고(CREATE) 요청하거나, 지워달라고(DELETE) 요청할 수도 있다.

## ✅ HTTP 요청 메소드

[HTTP 요청 메소드](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)

[HTTP 메소드 링크2](https://velog.io/@yh20studio/CS-Http-Method-%EB%9E%80-GET-POST-PUT-DELETE)

① GET: 특정 리소스의 표시를 요청함. 이 메소드를 사용하는 요청은 데이터를 받기만 한다. 데이터를 받아오기 위한 요청.

② HEAD: GET 메소드의 요청과 동일한 응답을 요구하지만, 응답 본문을 포함하지 않는다.

③ POST: 데이터 전송(삽입)을 위한 요청. 특정 리소스에 Entity를 제출할 때 쓰인다. 종종 서버의 상태 변화 / 부작용을 일으킨다.

④ DELETE: 특정 리소스를 삭제한다.

⑤ CONNECT: 목적 리소스로 식별되는 서버로의 터널을 맺는다.

⑥ OPTIONS: 목적 리소스의 통신 설정에 쓰인다.

⑦ TRACE: 목적 리소스의 경로를 따라 메시지 loop-back 테스트를 한다.

⑧ PATCH: 리소스의 부분을 수정하는 데에 쓰인다.

### 🌟 GET과 POST의 차이점

[참고링크](https://noahlogs.tistory.com/35)

[GET과 POST의 차이점 - 참고 블로그](https://im-developer.tistory.com/166)

```
‣ GET: 데이터를 받아오기 위한 요청. 서버의 리소스에서 데이터를 요청할 때 사용함.
‣ POST: 데이터를 전송(삽입)하기 위한 요청. 서버의 리소스를 새로 생성하거나 업데이트할 때 사용함.
```

→ DB로 따지면 GET은 SELECT 에 가깝고, POST는 Create 에 가깝다고 보면 된다.

→ GET은 리소스를 조회한다는 점에서 여러 번 요청하더라도 응답이 똑같을 것이다. 반대로 POST는 리소스를 새로 생성하거나 업데이트할 때 사용되기 때문에 멱등이 아니다.(POST 요청이 발생하면 서버가 변경될 수 있다.)

<mark>✷ get, post 등의 메소드들은 클라이언트가 보내는것, 서버는 200 300 400 500 같은 status code로 응답하는 것.</mark>

## 3. 보이지 않는 곳에서의 브라우저 작동 원리

### ① URL / URI

✷ 브라우저의 주소창에 입력한 URL: 서버가 제공되는 환경에 존재하는 파일의 위치. /(슬래쉬)를 이용해 서버의 폴더에 진입하거나 파일을 요청할 수 있지만, 기본적인 보안의 일환으로 외부의 직접 접근이 가능한 경우는 거의 없다.

✷ [URL] 크롬 브라우저에 입력하면, 브라우저로 PC의 폴더와 파일을 탐색할 수 있다.

```
# macOS에서 크롬 브라우저를 파일 탐색기로 사용할 수 있는 방법
# username에는 본인의 사용자 이름을 입력

file://127.0.0.1/Users/username/Desktop/

(우분투에서는 Users를 home으로 바꿀 것)
```

✅ URI는 URL을 포함하는 상위개념

'URL은 URI다.' 는 true, 'URI는 URL이다.' 는 false.

‣ URL(Uniform Resource Locator): 네트워크 상에서 웹 페이지, 이미지, 동영상 등의 파일이 위치한 정보를 나타낸다.

‣ scheme: URL에서 가장 먼저 작성하는 것. 프로토콜(통신 방식)을 결정함. → 일반적인 웹 브라우저에서는 http(s)를 사용함.

‣ hosts: 웹 서버의 이름이나 도메인, IP를 사용하며 주소를 나타냄.

‣ url-path: 웹 서버에서 지정한 루트 디렉토리부터 시작, 웹 페이지, 이미지, 동영상 등이 위치한 경로와 파일명을 나타냄.

‣ URI(Uniform Resource Identifier): 브라우저의 검색창을 클릭하면 나타나는 주소. → URL의 기본 요소 세 가지에 query, bookmark를 포함한다.

‣ query: 웹 서버에 보내는 추가적인 질문.

✷ port: 웹 서버에 접속하기 위한 통로. 서버로 진입할 수 있는 통로.

ex)

<mark style='background-color: #dcffe4'>:scheme:</mark> <mark>:hosts:</mark> <mark style='background-color: #99CEFA'>:url-path</mark> <mark style="background-color: #F6B4C1">:query:</mark> <mark style='background-color: #ffdce0'>:port:</mark>

‣ <mark style='background-color: #dcffe4'>file://</mark><mark>127.0.0.1</mark><mark style='background-color: #99CEFA'>/Users/username/Desktop/</mark>

‣ <mark style='background-color: #dcffe4'>http://</mark><mark>www.google.com</mark><mark style='background-color: #ffdce0'>:80</mark><mark style='background-color: #99CEFA'>/search</mark><mark style="background-color: #F6B4C1">?q=JavaScript</mark>

이 링크를 브라우저의 검색창에 입력하면 구글에서 JavaScript를 검색한 결과가 나옴.

### ② IP와 포트

‣ IP 주소: 네트워크에 연결된 특정 PC의 주소를 나타내는 체계(Internet Protocol address, IP address). 인터넷 상에서 사용하는 주소 체계.

‣ IPv4(IP 주소체계의 네 번째 버전, Internet Protocol version 4): 인터넷에 연결된 모든 PC는 IP 주소체계를 따라 네 덩이의 숫자로 구분된다.

→ 위의 예시에서 보았던 127.0.0.1 이 IP 주소이고, 이를 IP 주소체계인 IPv4라고 한다.

→ 터미널에서 nslookup 명령어를 이용해 IP 주소를 알 수 있다.

→ IPv4는 각 덩어리마다 0부터 255까지 나타낼 수 있고, 이 시스템을 따르면 약 43억 개(2^(32))의 IP 주소 표현 가능.

✷ IPv6(IP version 6)

인터넷 보급률이 낮았던 초기에는 IPv4로 네트워크에 연결된 PC에 주소를 할당하는 일이 가능했다.

그러나 개인 PC의 보급으로 누구나 PC로 인터넷에 접속하고, 각종 서비스를 위해 서버를 생산하면서 IPv4로 할당할 수 있는 PC가 한계를 넘어서게 되었고, 이를 위해 세상에 나오게 된 것이 IPv6.

IPv6는 표기법을 달리 책정하여 2^(128)개의 IP 주소를 표현할 수 있다.

✅이미 용도가 정해져 있는 IP 주소

‣ localhost, 127.0.0.1: 현재 사용 중인 로컬 PC를 지칭.

‣ 0.0.0.0, 255.255.255.255: broadcast address, 로컬 네트워크에 접속된 모든 장치와 소통하는 주소.
서버에서 접근 가능 IP 주소를 broadcast address로 지정하면, 모든 기기에서 서버에 접근할 수 있다.

‣ PORT: IP 주소가 가리키는 PC에 접속할 수 있는 통로(채널).

→ 리액트를 실행했을 때 로컬 PC의 IP 주소로 접근하여, 3000번의 통로를 통해 실행 중인 리액트를 확인할 수 있다(localhost:3000).

이미 사용 중인 포트는 중복 사용 불가. 다른 프로그램에서 포트를 사용 중이면 다른 포트 번호로 실행된다(localhost:3001).

→ 포트 번호는 0~65,535까지 사용 가능.

→ 이미 정해진 포트 번호라도 필요에 따라 자유롭게 사용할 수 있다.

→ 잘 알려지지 않은 포트(:3000과 같은 임시 포트)는 반드시 URI 등에 포함해야 한다. (잘 알려진 포트의 경우 URI 등에 명시하지 않음).

✅ 잘 알려진, 반드시 알아야 할 포트 번호

[(더 많은 포트 번호 확인)](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)

```
‣ 21: FTP
‣ 22: SSH
‣ 80: HTTP
‣ 443: HTTPS
```

### ③ 도메인과 DNS

‣ Domain name: 웹 브라우저를 통해 특정 사이트에 진입을 할 때, IP 주소를 대신하여 사용하는 주소.

→ 도메인 이름을 이용하면 한눈에 파악하기 힘든 IP 주소를 보다 분명하게 나타낼 수 있다.

ex)
![](https://blog.kakaocdn.net/dn/cbJLXp/btroDPue9R3/toWcf2OSuOOmgvOrzB6lM0/img.png)

ex) IP 주소는 142.250.196.142 이고, 도메인 이름은 google.com이다. 브라우저 주소창에 IP 주소를 입력하면 그에 해당하는 사이트인 구글 페이지로 이동할 수 있다.

‣ DNS(Domain Name System): 호스트의 도메인 이름을 IP 주소로 변환하거나 반대의 경우를 수행할 수 있도록 개발된 데이터베이스 시스템. ⇒ 사람이 기억하기 쉬운 도메인 주소를 컴퓨터가 이해할 수 있는 IP 주소로 변환.

![](https://blog.kakaocdn.net/dn/dKxSys/btroEyF4eaI/k4UN5YrEoadNCk0dLp3tK1/img.png)

(출처: 코드스테이츠)

→ 네트워크 상에 존재하는 모든 PC는 IP 주소가 있지만, 모든 IP 주소가 도메인 이름을 가지는 것은 아니다.

로컬 PC를 나타내는 127.0.0.1은 localhost 로 사용할 수 있지만, 그 외의 모든 도메인 이름은 일정 기간 대여하여 사용한다.

브라우저의 검색창에 도메인 이름을 입력하여 해당 사이트로 이동하기 위해 해당 도메인 이름과 매칭된 IP 주소를 확인하는 작업이 반드시 필요하다. 네트워크에는 이것을 위한 서버가 별도로 있는데, 이것이 DNS이다.

→ 도메인 네임 서버 중 권한 있는 네임 서버는 IP 주소 및 도메인 정보를 관리하는 권한을 가진 서버다.

→ DNS 요청이 HTTP 요청보다 우선한다.

→ 브라우저 검색창에 google.com을 입력하면 이 요청은 DNS에서 IP 주소를 찾고, 이 IP 주소에 해당하는 웹 서버로 요청을 전달하여 클라이언트와 서버가 통신할 수 있도록 한다.

✷ 도메인 주소는 오른쪽부터 왼쪽으로 최상위 도메인과 여러 개의 도메인으로 구성되어 있는데, 서브 도메인(Sub Domain), 루트 도메인(Root Domain), 최상위 도메인(Top Level Domain)이다.

‣ 최상위 도메인: 도메인의 가장 오른쪽에 위치한다. 예시로는 .com, .kr, .net 등이 있다. kr, us와 같은 국가 코드를 사용하는 도메인은 co, ac와 같은 2단계 도메인과 함께 사용되기도 한다.

‣ 서브 도메인: 도메인의 가장 왼쪽에 위치한다. 일반적으로 www(기본), m(모바일), store(스토어)와 같은 것들이 있다. 호스트의 이름으로 불리기도 하며, 웹 사이트의 특정 부분을 나눠서 보여주어야 하는 경우에 사용한다. 도메인에 따라 사이트의 구성이 달라진다.

→ 대표적으로 모든 도메인을 관리하는 루트 네임 서버. TLD를 관리하는 네임 서버, 권한 있는 네임 서버로 구성됨.

⇒ 루트 도메인 네임 서버는 각 최상위 도메인 네임 서버들의 주소를 알고 있으며 최상위 도메인 네임 서버는 권한 있는 네임 서버의 주소를 알고 있다.

권한 있는 네임 서버는 도메인 IP 주소 및 도메인 정보를 관리하는 권한을 가진 서버다.

→ DNS는 안정성을 위해 최소 두 개 이상의 서버가 하나의 도메인 네임을 담당한다. 여러 개의 서버로 구성하는 것이 과부하 및 서비스 거부 공격에 대해 효율적인 대응이 가능하다.

✷ DNS lookup의 순서

```
① 브라우저는 리졸버에게 특정 URL에 대한 IP 주소를 요청한다.
② 리졸버는 우선 기존에 찾아본 도메인정보가 내용이 담긴 캐시 파일을 살펴본다.
③ 해당되는 도메인정보가 있다면 즉시 IP주소를 리턴한다.
④ 해당되는 도메인 정보를 찾을수 없는 경우 DNS 리졸버는 IP주소를 얻기 위해
루트, 탑레벨, 권한있는 도메인 서버에 차례대로 쿼리를 진행하며 IP주소를 알아낸다.
⑤ 마지막으로 리졸버는 전달받은 결과값인 IP주소를 기록하고 브라우저에게 전달한다.
```

✷ 리졸버: 요청받은 도메인의 IP 주소를 찾기위해 여러 네임 서버에 반복적인 질의를 하는 이름 서버.

![](https://blog.kakaocdn.net/dn/bnLUf7/btroFWueWR1/9rpODb5asbYMmbnVBArNZK/img.png)

→ root, top level domain, 권한 있는 도메인 서버 순서대로 쿼리를 진행하며 IP주소를 알아낸다.

DNS lookup → DNS는 응답을 보내기 위해 한 개 이상의 존 파일(zone file)을 가지고 있다.

존 파일은 네임(도메인 네임 / 서브 도메인 네임)과 클래스(네트워크 타입 지정 / 일반적으로 IN으로 지정됨), TTL(Time To Live, 클라이언트가 데이터를 저장 가능한 시간 / 리졸버가 레코드를 몇 초동안 저장할 지를 명시하고  해당 시간이 지나면 리졸버는 해당 레코드를 삭제), 레코드 타입(변환될 데이터의 형식), 레코드 데이터(반환되는 데이터)로 구성된 레코드들로 구성되어 있다.

→ 네임 서버들은 존 파일들을 바탕으로 요청에 해당하는 레코드를 리턴하고, 리졸버는 이 레코드를 살펴보고 리턴해야할 IP 혹은 다음에 쿼리를 진행할 서버의 주소를 확인한다.

✷ 대표적인 레코드 타입

⇒ 인터넷 네트워크를 사용하며 192.168.0.2 는 deploy 서브도메인의 주소, www 서브도메인은 states.com 도메인으로 연결되어 있음.

| states.com | IN  |  SOA  | NS.도메인.주소; 포트번호; 만료시간; ... |
| :--------: | :-: | :---: | :-------------------------------------: |
| states.com | IN  |  ns   |             NS.도메인.주소              |
|   deploy   | IN  |   A   |               192.168.0.2               |
|    www     | IN  | CNAME |               states.com                |

‣ A, AAAA: IPv4, IPv6 주소임을 명시함

‣ CNAME: 데이터가 도메인 주소임을 명시함

‣ NS: 데이터가 도메인 네임 서버들의 주소임을 명시함

‣ SOA: 데이터가 도메인 네임 서버들 중 주 서버의 정보들에 대한 데이터. 주 네임 서버와 통신할 수 있는 포트 번호, TTL, 도메인 주소 등이 적혀 있음

### ④ 크롬 브라우저 에러 읽기

에러 메시지는 웹페이지를 제공하는 서버와 Chrome 브라우저가 소통하는 단계, 또는 기기와 네트워크의 연결, Chrome 브라우저가 해석할 수 없는 데이터를 전송받은 경우 발생한다.

‣ Aw, Snap! (앗, 이런!)

웹페이지 대신 '앗, 이런!' 에러 페이지 또는 다른 에러 메시지가 표시되는 것은 Chrome 브라우저가 웹 페이지를 로드하는 데에 문제가 발생한 경우이다.

이 경우 페이지가 느리게 로드되거나, 열리지 않을 수도 있다.

✷ 페이지를 여는 중에 문제가 발생했다는 뜻의 에러 메시지들

|             Error Messages              |                                                            Description                                                             |
| :-------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------: |
|        "Aw, Snap!" ("앗, 이런!")        |                                   Chrome 브라우저에서 페이지를 로드하는 데 문제가 발생했습니다.                                    |
|          ERR_NAME_NOT_RESOLVED          |                                             호스트 이름(웹 주소)이 존재하지 않습니다.                                              |
|        ERR_INTERNET_DISCONNECTED        |                                           사용 중인 기기가 인터넷에 연결되지 않았습니다.                                           |
| ERR_CONNECTION_TIMED_OUT, ERR_TIMED_OUT | 페이지에 연결하는 데 시간이 너무 오래 걸립니다. 인터넷 연결이 너무 느리거나, 웹페이지에 접속한 사용자가 많아서 발생할 수 있습니다. |
|          ERR_CONNECTION_RESET           |                                       웹페이지 연결을 방해하는 요소가 어딘가에 발생했습니다.                                       |
|           ERR_NETWORK_CHANGED           |                  웹페이지를 로드하는 중에 기기의 네트워크 연결이 해제되었거나, 새로운 네트워크에 연결되었습니다.                   |
|         ERR_CONNECTION_REFUSED          |                                     웹페이지에서 Chrome 브라우저의 연결을 허용하지 않았습니다.                                     |
|             ERR_CACHE_MISS              |                             웹페이지로부터 이전에 입력한 정보를 다시 한 번 제출하도록 요청받았습니다.                              |
|           ERR_EMPTY_RESPONSE            |                    웹페이지에서 데이터를 전혀 전송하지 않았으며 데이터를 전송할 서버가 다운되었을 수 있습니다.                     |
|         ERR_SSL_PROTOCOL_ERROR          |                                 페이지에서 전송된 데이터를 Chrome 브라우저가 해석하지 못했습니다.                                  |
|      ERR_BAD_SSL_CLIENT_AUTH_CERT       |               클라이언트 인증서(은행 또는 회사 내부 웹사이트 등)에 오류가 발생하여 웹페이지에 로그인할 수 없습니다.                |

⇒ 전체 에러 메시지 목록은 크롬 브라우저의 검색창에 chrome://network-errors/를 입력하여 확인할 수 있다.

⇒ [문제 해결에 도움을 받을 수 있는 페이지](https://support.google.com/chrome/answer/95669#zippy=%2Cpage-loading-error-codes-and-issues)

위에서의 에러 메시지를 만나면, 다음과 같은 문제가 발생할 수 있다.

‣ 웹페이지에 연결할 수 없습니다.

‣ 웹페이지가 열리지 않습니다.

‣ HTTPS가 적용된 웹페이지가 열리지 않습니다.

‣ 사진이 로드되지 않습니다.

‣ 새 탭이 로드되지 않습니다.

## 4. How to use Chrome Network Tab

{% include video id="e1gAyQuIFQo" provider="youtube" %}

(영어 영상을 한국어로 자동 번역해서 적는 것이므로 잘못 해석된 부분이 있을 수 있음)

① 일단 [<font color="red">여기</font>](https://devtools.glitch.me/network/getstarted.html)로 들어가서

② (맥에서는)opt+cmd+I로 개발자 도구를 연다(또 다른 자세한 단축키는 [여기](https://hsly22xk.github.io/information/mac-hotkey/)에)

③ Network를 클릭하고

④ 페이지를 새로고침 한다.(개발자 도구에 영어로 써있는 것을 한국어로 보고싶다면 설정에서 바꿀 수 있다)

![](https://blog.kakaocdn.net/dn/bKdPtN/btroHaLeTPH/KQkjkIaBfAgBF5TvKLK7Dk/img.png)

⑤ 아래에서 총 요청 수(5 requests)와 전송된 총 데이터 양(12.2 kB transferred)을 볼 수 있다.

⑥ 위에 있는 차트(200ms, 400ms ...)는 네트워크 활동에 대한 개요를 제공한다.

(하지만 이 글에서는 개요를 설명하지 않을 것이기 때문에 X 버튼 밑에 있는 톱니바퀴를 눌러 Show overview(개요 표시)에 체크를 풀어준다. 그리고 다시 톱니바퀴를 눌러준다.)

![](https://blog.kakaocdn.net/dn/by98Dg/btroDwBZ56S/ktvKjUYeb5U67oygTZBl00/img.png)

⑦ Name, Status, Type ... 이 쓰여있는 이 표(테이블)를 '네트워크 로그' 라고 한다. 기본적으로 네트워크 활동에 대한 시간순 로그를 보여준다.

⇒ 네트워크 요청이 예상대로 진행되고 있는 지 확인할 때 네트워크 로그가 도움이 된다.

ex) 리소스를 가져오기 위해 코드를 추가할 때 네트워크 패널을 열고 새 요청이 통과하는 지 확인한다.

혹은 undefined 된 다른 파일의 일부 기능에 대한 reference error가 발생하면 네트워크 로그를 관찰하여 스크립트가 잘못된 순서로 로드되는 지 확인한다.

‣ Status(상태)열: 서버가 반환한 HTTP 응답 코드

‣ Type(유형)열: 리소스 유형

‣ Initiator열: 리소스를 요청한 원인을 알려준다.

‣ Size열: 리소스의 크기. 특히 리소스가 압축되었는 지 확인할 때 유용하다.

‣ Time열: 브라우저에서 리소스를 업로드하거나 다운로드 하는 데에 걸린 시간을 알려준다.

‣ Waterfall: 각 리소스에 대한 네트워크 활동에 대한 시각적 요약을 제공한다.

![](https://blog.kakaocdn.net/dn/bHFTPV/btroAJVZs4N/OWLkZlHX4iUUyXNRIEMk7k/img.png)

⑧ Waterfall 위로 마우스를 갖다대면 여러 단계의 분석이 표시된다. 각 리소스의 자세한 정보를 보고 싶으면 아까처럼 톱니바퀴를 눌러 Use Large request rows(큰 요청 열)을 체크해준다.

![](https://blog.kakaocdn.net/dn/muGeA/btroFLLIw2Y/UUEtac1onthRhvnlKcHXfK/img.png)

위에 써 있는 값(1.4 kB)은 압축되지 않은 크기, 아래에 써있는 값(1.2 kB)은 압축된 크기이다. 만약 두 값이 같다면 압축이 작동하지 않는 것이다.

⑨ 각각의 헤더(Name, Status ... Time)를 클릭하여 해당 차원에 따른 로그를 구성할 수 있고, Waterfall을 클릭하면 시간 순 정렬로 돌아간다.

⑩ 헤더를 우클릭하면 기본으로 나오는 열 이외에 다른 기능들을 체크하여 보이게 할 수 있다.

![](https://blog.kakaocdn.net/dn/biH67L/btroDfHglQh/OwednJBxNqmFTG7VZMVUB0/img.png)

✅ 개발자 도구(DevTools)가 열려있는 한 로그에 네트워크 활동이 계속 기록된다.

→ 위의 사진들에서 48.png라는 파일이 제일 밑에 있는 것을 볼 수 있는데, 브라우저에서 Get Data 버튼을 누르면 로그 맨 아래에 getstarted.json이라는 새 리소스가 있는 것을 확인할 수 있다.

엄청난 양의 네트워크 활동을 기록하는 페이지가 있고, 필요한 정보가 모두 이미 있는 경우에는 기록 중지(빨간 버튼)를 누를 수 있다.

✷ 네트워크 조절을 사용하면 연결 속도를 낮춰 모바일 사용자처럼 사이트를 경험할 수 있다.

![](https://blog.kakaocdn.net/dn/MZBLL/btroDf8rccV/5j50BXSebjt3KFodkSD38K/img.png)

① 빨간 버튼이 있는 줄에 No throttling이라는 드롭다운이 있다. 여기서 slow 3G를 선택한다.

그러면 이 탭은 이제 slow 3G와 유사한 네트워크 연결이 지속되며, 개발자 도구가 열려있는 한 계속해서 제한된다.

② 처음 방문한 사람처럼 페이지 로드를 경험하고 싶다고 할 때, 브라우저의 새로고침 버튼을 길게 눌러 Empty Cache and Hard Reload(캐시 비우기 및 강력 새로고침)을 클릭.

⇒ 기본적으로 브라우저가 캐시로 이동하는 대신 모든 리소스에 대해 네트워크로 이동하도록 한다.

⇒ 전부 따라하고 Time 열에 있는 시간을 보면 각 리소스를 다운로드 하는 데에 시간이 더 오래 걸린다는 것을 알 수 있다.

✷ 개별 네트워크 리소스 검사 방법

① Name 열에 있는 리소스들 중 하나를 클릭하면 해당하는 리소스를 자세히 알아볼 수 있다.

![](https://blog.kakaocdn.net/dn/tEVSd/btroAAypRLZ/6nBXBBbiglXGRSKEFcehnK/img.png)

‣ Header탭: HTTP 요청 및 응답 헤더 표시

‣ Preview(미리보기)탭: 리소스의 기본 렌더링

→ HTML의 경우는 HTML에서의 오류 코드를 반환하는 API로 작업할 때 유용하다.

‣ Response(응답)탭: 관련 있는 리소스의 소스 코드가 표시됨.

‣ Timing 탭: 위에서의 Waterfall 위로 마우스를 가져갔을 때 본 것과 동일한 타이밍 분석이 표시됨.

✷ 네트워크 패널은 특정 문자열 / 패턴에 대한 헤더 및 메시지 본문 검색을 지원한다.

⇒ 리소스가 자주 변경되지 않는 경우

브라우저는 동일한 리소스가 반복 다운로드 되지 않도록 오랫동안 캐시해야 한다. 헤더에 캐시 정책이 정의되어 있기 때문에 네트워크 패널에서 이 정보를 검색하는 것이 좋다.

![](https://blog.kakaocdn.net/dn/cZa3Jr/btroE8Ha4CW/KWrYVHhonHwRRblX4uLB91/img.png)

돋보기 버튼을 클릭하여 검색창에 Cache-Control이라고 검색한다.

결과를 클릭하여 텍스트가 HTTP 헤더에서 발견된 경우에는 Headers탭에서 열리고,

메시지 본문에서 발견된 경우에는 Reponse 탭에서 열린다.

✷ 필터 기능을 지원한다. ⇒ 돋보기 옆에 있는 깔대기 버튼을 클릭하면 필터 도구 모음이 보여진다.

기본적으로는 굳이 클릭하지 않아도 표시가 되어 있지만, 그렇지 않은 경우 클릭하여 표시해준다.

ex) png같은 특정 파일 형식을 필터링하고 싶을 때, 필터 검색창에 png를 타이핑하면 개발자 도구는 URL에 png 문자열을 포함하는 리소스를 제외한 모든 리소스들을 필터링하여 보여준다.

⇒ 특정 파일 유형에 집중하고 싶을 때 필터링 할 수 있다.

![](https://blog.kakaocdn.net/dn/bOhy8V/btroDPOR2dv/fJEPYwNYdim24rcQ9IsvWk/img.png)

위에 Fetch/XHR, JS, CSS ... Other가 써있는 것으로 필터링 할 수 있다.

JS 파일만 보고싶으면 JS를 클릭하고, CSS만 보고 싶으면 CSS를 클릭하면 된다.

내가 보고 싶은 파일 형식을 제외한 모든 파일 형식이 필터링 되는 것을 확인할 수 있다.

만약 하나가 아닌 두 개 이상의 파일 형식을 한 번에 보고 싶으면 하나를 클릭한 상태에서 cmd(command 키)를 누르고 다시 또 다른 파일 형식을 클릭한다. 다시 모든 파일 형식을 보려면 All을 클릭하면 된다.

⇒ 파일 패턴을 일치시키려면 정규식을 사용할 수 있다.

```
ex) /.\*\[cj]s+$/
```

이 패턴은 c or j 다음에 하나 이상의 s로 끝나지 않는 리소스를 필터링한다. 파일이나 패턴을 제외하려면 이름 앞에 - 를 넣으면 negative filter가 된다.

![](https://blog.kakaocdn.net/dn/cBghOD/btroDhFakMR/LkJuqXx3RJo2Ho3CUTEKm0/img.png)

main.css를 필터창에 입력했을 때 문자열과 일치하는 모든 리소스를 필터링하여 보여주는 것을 알 수 있다.

✷ [각 리소스의 속성별로 필터링할 수 있는 10개의 특수 키워드](https://developer.chrome.com/docs/devtools/network/reference/#filter-by-property)

ex)

```
domain:raw.githubusercontent.com를 입력하면 해당 도메인과 일치하지 않는 모든 URL이 필터링된다.
```

더 자세히 보려면 제목에 달아놓은 링크를 통해 들어가면 됨.

✷ 요청 차단을 사용하여 개별 리소스를 차단하고 해당 리소스를 사용할 수 없을 때 페이지의 작동 방식

ex) 스타일 시트가 차단되었을 때 페이지가 어떻게 작동하는 지에 대한 예시

① cmd + shift + P를 이용하여 명령 팔레트를 연다.

② block을 입력하고 Show Network request blocking(제일 위에 있는 것)를 선택한다.

③ 밑에서 Add pattern을 클릭한다.

④ main.css를 입력한 다음 Add를 클릭하고 브라우저 새로고침을 누른다.

⇒ 이렇게 하면 브라우저의 스타일이 처음과는 이상한 것을 발견할 수 있다. 그리고 main.css가 차단 되었음을 나타내기 위해 빨간 글씨로 읽혀진다.

[(더 많은 개발자 도구 네트워크 기능 참조 사이트)](https://developer.chrome.com/docs/devtools/network/reference/)

## 5. HTTP(HyperText Transfer Protocol)

HTML과 같은 문서를 전송하기 위한 Application Layer 프로토콜(통신규약).

→ 웹 브라우저와 웹 서버의 소통을 위해 디자인되었음.

→ 전통적인 클라이언트-서버 모델에서 클라이언트가 HTTP messages 양식에 맞춰 요청을 보내면 서버도 HTTP messages 양식에 맞춰 응답한다.

→ HTTP는 특정 상태를 유지하지 않는다(stateless).

### ① HTTP Messages, Request & Response

클라이언트와 서버 사이에서 데이터가 교환되는 방식.

→ HTTP messages는 몇 줄의 텍스트 정보로 구성되지만 개발자는 이런 메시지를 직접 작성할 필요가 거의 없다. 구성 파일, API, 기타 인터페이스에서 HTTP messages를 자동으로 완성한다.

![](https://blog.kakaocdn.net/dn/bmcBOd/btroCxHVwiV/Af51pO4bl6F90PoyAYAqK1/img.png)

### HTTP Messages의 구조

✅ HTTP Messages의 2가지 유형

![](https://blog.kakaocdn.net/dn/baBORw/btroEyMZ2XS/VNrg1YRddolByHW90eedo1/img.png)

-요청(request): 클라이언트가 서버로 전달해서 서버의 액션이 일어나게끔 하는 메시지.

{% include video id="pHFWGN-upGM" provider="youtube" %}

⇒ 통신은 항상 서버에 HTTP 요청을 보내는 클라이언트에 의해 시작되고, 서버는 응답 메시지로 응답한다. 이 메시지는 나중에 기계가 작업, 이미지 및 멀티미디어 컨텐츠로 해석할 수 있는 텍스트의 본문이다.

‣ start line: 요청이나 응답의 상태를 나타내며 항상 첫 번째 줄에 위치한다. 응답에서는 status line이라고 부른다.

① 수행할 작업(GET, PUT, POST 등)이나 방식(HEAD / OPTIONS)을 설명하는 HTTP method.

ex) GET method는 리소스를 받아야 하고, POST method는 데이터를 서버로 전송한다.

② 요청 대상(일반적으로는 URL / URI) 또는 프로토콜, 포트, 도메인의 절대 경로는 요청 컨텍스트에 작성된다. 이 요청 형식은 HTTP method 마다 다르다.

→ origin 형식: ?와 쿼리 문자열이 붙는 절대 경로. [POST, GET, HEAD, OPTIONS 등의 method](https://developer.mozilla.org/ko/docs/Web/HTTP/Method)와 함께 사용한다.

```
POST / HTTP 1.1
GET /background.png HTTP/1.0
HEAD /test.html?query=alibaba HTTP/1.1
OPTIONS /anypage.html HTTP/1.0
```

→ 여기에는 HTTP verb, URI, HTTP 버전 번호가 포함된다.

ex)

<mark>HTTP verb</mark> / <mark style='background-color: #dcffe4'>URI</mark> / <mark style='background-color: #ffdce0'>HTTP 버전 번호</mark>

<mark>GET</mark> / <mark style='background-color: #dcffe4'>home.html</mark> <mark style='background-color: #ffdce0'>HTTP/1.1</mark>

<mark>POST</mark> / <mark style='background-color: #dcffe4'>index.html</mark> <mark style='background-color: #ffdce0'>HTTP/1.1</mark>

<mark>DELETE</mark> / <mark style='background-color: #dcffe4'>query.html</mark> <mark style='background-color: #ffdce0'>HTTP/1.1</mark>

→ absolute 형식: 완전한 URL 형식으로, 프록시에 연결하는 경우 대부분 GET method와 함께 사용한다.

```
GET http://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1
```

→ authority 형식: 도메인 이름과 포트 번호로 이루어진 URL의 authority component. HTTP 터널을 구축하는 경우, CONNECT와 함께 사용할 수 있다.

```
CONNECT developer.mozilla.org:80 HTTP/1.1
```

→ asterisk 형식: OPTIONS 와 함께 별표(asterisk) 하나로 서버 전체를 표현한다.

```
OPTIONS * HTTP/1.1
```

③ HTTP 버전에 따라 HTTP message의 구조가 달라진다. 따라서 start line에 HTTP 버전을 함께 입력한다.

‣ HTTP headers: 요청을 지정하거나, 메시지에 포함된 본문을 설명하는 헤더의 집합.

![](https://blog.kakaocdn.net/dn/py4v9/btrozwbJliB/wju3D0kKtUOhdwAIDbpkZk/img.png)

→ 요청의 Headers는 기본 구조를 따른다. 헤더 이름(대소문자 구분이 없는 문자열), 콜론( : ), 값을 입력한다. 값은 헤더에 따라 다르다. 여러 종류의 헤더가 있고, 이렇게 그룹을 나눌 수 있다.

① General headers: 메시지 전체에 적용되는 헤더, body를 통해 전송되는 데이터와는 관련 없음.

② Request headers: fetch를 통해 가져올 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더.

User-Agent, Accept-Type, Accept-Language과 같은 헤더는 요청을 보다 구체화한다.

Referer처럼 컨텍스트를 제공하거나 If-None과 같이 조건에 따라 제약을 추가할 수 있다.

③ Representation headers: 이전에는 Entity headers로 불렀으며, body에 담긴 리소스의 정보(컨텐츠 길이, MIME 타입 등)를 포함하는 헤더.

‣ empty line: 헤더와 본문을 구분하는 빈 줄.

‣ body: 요청과 관련된 데이터나 응답과 관련된 데이터 또는 문서를 포함한다.

요청과 응답의 유형에 따라 선택적으로 사용한다. HTTP message 구조의 마지막에 위치한다.

→ 모든 요청에 body가 필요한 것은 아니다.

→ GET, HEAD, DELETE, OPTIONS처럼 서버에 리소스를 요청하는 경우에는 본문이 필요하지 않다. POST나 PUT과 같은 일부 요청은 데이터를 업데이트하기 위해 사용한다.

① Single-resource bodies(단일-리소스 본문): 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성된다.

② Multiple-resource bodies(다중-리소스 본문): 여러 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지닌다. 보통 [HTML form](https://developer.mozilla.org/en-US/docs/Learn/Forms)과 관련이 있다.

이 중 start line과 HTTP headers를 묶어 요청이나 응답의 헤드(head)라고 하고, [payload](<https://ko.wikipedia.org/wiki/%ED%8E%98%EC%9D%B4%EB%A1%9C%EB%93%9C_(%EC%BB%B4%ED%93%A8%ED%8C%85)>)는 body라고 한다.

-응답(response): 요청에 대한 서버의 답변.

{% include video id="c9sMNc2PrMU" provider="youtube" %}

⇒ 클라이언트가 요청을 보내면 서버는 응답을 반환 하는데, 이 응답에는 요청된 정보 혹은 오류 메시지가 있는 경우 오류 메시지를 포함할 수 있다.

‣ Status line은 선택적 응답 헤더가 뒤따른다.

상태 표시줄에는 HTTP 버전, 상태 코드, 상태 코드를 영어로 설명하는 이유 문구가 포함된다.

ex)

<mark>HTTP 버전</mark> / <mark style='background-color: #dcffe4'>상태 코드</mark> / <mark style='background-color: #ffdce0'>상태 코드 설명 문구</mark>

<mark>HTTP/1.1</mark> <mark style='background-color: #dcffe4'>200</mark> <mark style='background-color: #ffdce0'>OK</mark>

<mark>HTTP/1.1</mark> <mark style='background-color: #dcffe4'>404</mark> <mark style='background-color: #ffdce0'>Not Found</mark>

<mark>HTTP/1.1</mark> <mark style='background-color: #dcffe4'>403</mark> <mark style='background-color: #ffdce0'>Forbidden</mark>

<mark>HTTP/1.1</mark> <mark style='background-color: #dcffe4'>500</mark> <mark style='background-color: #ffdce0'>Internal Server Error</mark>

[✷ HTTP 상태 코드에 대한 MDN 문서](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

```
HTTP code

2xx 성공
200: 클라이언트의 요청을 정상적으로 수행함.
201: 클라이언트에게 생성 작업을 요청 받았고, 생성 작업을 성공함.
204: 요청은 성공 했지만 응답할 콘텐츠가 없음.

3xx 리다이렉션
301: 클라이언트가 요청한 리소스에 대한 URI가 영구적으로 변경되었을 때 사용함.
302: 301과 같으나 임시적으로 주소가 바뀌었을 경우 사용함.
304: 이전에 방문했을 때의 요청 결과와 다르지 않을 경우 사용함. 캐시된 페이지를 그대로 사용.
307: 임시 페이지로 리다이렉트.

4xx 클라이언트 오류
400: 클라이언트가 올바르지 못한 요청을 보냄.
401: 로그인을 하지 않아 페이지를 열 권한이 없음.
403: 금지된 페이지, 로그인을 하든 안하든 접근할 수 없음. (관리자 페이지)
404: 찾을 수 없는 페이지, 주소를 잘 못 입력했을 때 사용함. 403 대신에 사용할 수도 있음.
(해커들의 공격을 방지하고자 페이지가 없는 것처럼 위장함)

408: 요청 시간이 초과됨.
409: 서버가 요청을 처리하는 과정에서 충돌이 발생한 경우. (회원가입 중 중복된 아이디인 경우)
410: 영구적으로 사용할 수 없는 페이지.

5xx 서버 오류
501: 해당 요청을 처리하는 기능이 만들어지지 않음.
502: 서버로 가능 요청이 중간에서 유실된 경우.
503: 서버가 터졌거나 유지 보수 중
(유지 보수 중일때는 유지 보수중이라는 것을 알려주는 페이지로 전송해주는 것이 좋음)

504: 서버 게이트웨이에 문제가 생겨 시간 초과가 된 경우.
505: HTTP 버전이 달라 요청이 처리할 수 없음.
```

다음의 세 가지 정보를 포함하며, HTTP/1.1 404 Not Found. 처럼 생겼다.

→ 현재 프로토콜 버전(HTTP/1.1)

→ 상태 코드 - 요청 결과(200, 302, 404 등)

→ 상태 텍스트 - 상태 코드에 대한 설명

‣ HTTP headers: 요청 헤더와 동일한 구조를 가지고 있다.

![](https://blog.kakaocdn.net/dn/YDhdx/btroE8fSm6Q/mztFNdYrOJrid1rpaibX80/img.png)

대소문자 구분 없는 문자열과 콜론(:), 값을 입력하며 값은 헤더에 따라 다르다. 요청의 헤더와 마찬가지로 몇 그룹으로 나눌 수 있다.

① General headers: 메시지 전체에 적용되는 헤더. body를 통해 전송되는 데이터와는 관련 없음.

② Response headers: 위치 또는 서버 자체에 대한 정보(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더,

Vary, Accept-Ranges와 같이 상태 줄에 넣기에는 공간이 부족했던 추가 정보를 제공한다.

③ Representation headers: 이전에는 Entity headers로 불렀으며, body에 담긴 리소스의 정보(컨텐츠 길이, MIME 타입 등)를 포함하는 헤더.

‣ Body

응답의 본문은 HTTP messages 구조의 마지막에 위치한다.

모든 응답에 body가 필요하지는 않다. 201, 204와 같은 상태 코드를 가지는 응답에는 본문이 필요하지 않다.

응답의 body는 다음과 같이 두 종류로 나눌 수 있다.

① Single-resource bodies(단일-리소스 본문): 길이가 알려진 단일-리소스 본문은 두 개의 헤더(Content-Type, Content-Length), 길이를 모르는 단일 파일로 구성된 단일-리소스 본문은 Transfer-Encoding이 chunked 로 설정되어 있으며, 파일은 chunk로 나뉘어 인코딩되어 있다.

② Multiple-resource bodies(다중-리소스 본문): 서로 다른 정보를 담고 있는 body.

‣ <mark>Statless(무상태성 - HTTP의 가장 큰 특징)</mark>: 상태를 가지지 않는다는 뜻. HTTP는 특정 상태를 담고 있지 않으며, 이전 요청이나 다음 요청을 기억하지 않음.

HTTP로 클라이언트와 서버가 통신을 주고 받는 과정에서 HTTP가 클라이언트나 서버의 상태를 확인하지 않는다.

ex)

사용자는 쇼핑몰에 로그인하거나 상품을 클릭해서 상세 화면으로 이동하고, 상품을 카트에 담거나 로그아웃을 할 수도 있다. 클라이언트에서 발생한 이런 모든 상태를 HTTP 통신이 추적하지 않는다.

만약 쇼핑몰에서 카트에 담기 버튼을 눌렀을 때, 카트에 담긴 상품 정보(상태)를 저장해둬야 한다.

그러나 HTTP는 통신 규약일 뿐이므로, 상태를 저장하지 않는다.

따라서, 필요에 따라 다른 방법(쿠키-세션, API 등)을 통해 상태를 확인할 수 있다.

✷ 쿠키: 서버가 일방적으로 클라이언트에 전달하는 작은 데이터(응답헤더에 set-cookie 넣어서). → 서버가 웹 브라우저에 정보를 저장하고 불러올 수 있는 수단

✷ 쿠키를 이용한다는 것: 서버가 클라이언트에게 쿠키 전송(+ 클라이언트에서 서버로 쿠키 전송)

→ 장시간 보존해야 하는 정보 저장에 적합(로그인 상태 유지, 사용자 선호 테마 등)

→ 서버는 데이터를 저장한 이후 아무때나 데이터를 가져올 수 없다.
특정 조건이 만족하는 경우에만 다시 가져올 수 있는데, 이런 조건은 쿠키 옵션으로 설정한다.

## 6. 보이는 곳에서의 브라우저 작동 원리

① AJAX(SPA를 만드는 기술 / Asynchronous JavaScript And XMLHttpRequest): <mark>fetch를 사용해서 DOM을 조작하는 방식</mark>으로 JavaScript, DOM, Fetch, XMLHttpReqest, HTML 등의 다양한 기술을 사용하는 웹 개발 기법.

→ **웹 페이지에 필요한 부분에 대한 데이터만 비동기적으로 받아와 화면에 그릴 수 있다.**

⇒ CSR을 위해 사용한다.

⇒ fetch가 비동기이기 때문에 AJAX도 비동기이다.

→ AJAX가 나오기 전에는 동적으로 페이지 렌더링을 했다

ex)

우리가 구글 페이지에 들어갔을 때, 웹 페이지의 html에 의해 유저에게 필요한 페이지가 렌더링 된다.

그러나 검색창 만큼은 html에 작성된 대로 사용하는 것이 아니라, 유저의 요구에 따라 반응하며 변화하는 부분이다.

검색창에 글자를 입력할 때마다, 해당 글자로 시작하는 단어들을 서버로부터 받아와 추천 검색어로 보여준다.

⇒ 검색창에서는 필요한 데이터만 비동기적으로 받아와 렌더링되며, 여기에 AJAX가 사용된다.

⇒ 페이스북 메시지나 네이버 포털사이트의 뉴스 탭도 비동기적으로 데이터를 서버에서 받아와 브라우저에 렌더링 하는 것.

### ①-1. 무한 스크롤

사용자가 페이지의 맨 밑까지 스크롤하여 스크롤바 하단에 도달하면 새로운 리소스를 서버에서 가져와 렌더링 하는 이벤트 → 무한 스크롤이 발생 할 때마다 Fetch를 통해 데이터를 가져와서 업데이트 하고 렌더링한다.

### ①-2. AJAX의 핵심 기술

‣ 웹 페이지 표현을 위한 HTML, CSS

‣ 데이터에 접근하거나, 화면 구성을 동적으로 조작하는 DOM

‣ 데이터 교환에 사용되는 JSON 이나 XML

‣ 웹 서버와 비동기적 통신을 위한 XMLHttpRequest 객체

‣ JavaScript

AJAX를 구성하는 핵심 기술은 JavaScript와 DOM, 그리고 Fetch이다.

전통적인 웹 어플리케이션에서는 form 태그를 이용해 서버에 데이터를 전송해야 했다.

또한 서버는 요청에 대한 응답으로 새로운 웹 페이지를 제공해주어야 했다. ⇒ 클라이언트에서 요청을 보내면 매번 새로운 페이지로 이동해야 했습니다.

그러나 Fetch를 사용하면, 페이지를 이동하지 않아도 서버로부터 필요한 데이터를 받아올 수 있다. Fetch는 사용자가 현재 페이지에서 작업을 하는 동안 서버와 통신할 수 있도록 한다.

⇒ 브라우저는 Fetch가 서버에 요청을 보내고 응답을 받을때까지 모든 동작을 멈추는 것이 아니라, 계속해서 페이지를 사용할 수 있게 하는 비동기적인 방식을 사용한다.

⇒ 자바스크립트에서 DOM을 사용해 조작할 수 있기 때문에, Fetch를 통해 필요한 데이터만 가져와 DOM에 적용시켜 새로운 페이지로 이동하지 않고 기존 페이지에서 필요한 부분만 변경할 수 있다.

‣ XHR과 Fetch

Fetch 이전에는 표준화 된 XHR(XMLHttpRequest)를 사용했지만 XHR은 Cross-Site 이슈 등의 불편함이 있었다.

Fetch는 XHR의 단점을 보완한 새로운 Web API이며, XML보다 가볍고 JavaScript와 호환되는 JSON을 사용하고,간편함, promise 지원 등의 장점을 가지고 있기 때문에 오늘날에는 XHR보다 Fetch를 많이 사용한다.

ex) Fetch의 예제

```js
// Fetch 예제
fetch('http://52.78.213.9:3000/messages').then (function(response) {
  return response.json();
})
.then(function (json) {
  ...
});
```

ex) XHR의 예제

```js
// XMLHttpRequest를 사용
var xhr = new XMLHttpRequest();
xhr.open("get", "http://52.78.213.9:3000/messages");

xhr.onreadystatechange = function () {
  if (xhr.readyState !== 4) return;
  // readyState 4: 완료

  if (xhr.status === 200) {
    // status 200: 성공
    console.log(xhr.responseText); // 서버로부터 온 응답
  } else {
    console.log("에러: " + xhr.status); // 요청 도중 에러 발생
  }
};

xhr.send(); // 요청 전송
```

이 외에도 Axios와 같은 라이브러리도 존재하며, 경우에 따라 적절한 것을 선택하여 사용한다.

### ①-3. AJAX의 장점과 단점

‣ 장점

→ 서버에서 HTML을 완성하여 보내주지 않아도 웹 페이지를 만들 수 있다.

이전에는 서버에서 HTML을 완성하여 보내주어야 화면에 렌더링을 할 수 있었지만 AJAX를 사용하면 서버에서 완성된 HTML을 보내주지 않아도 필요한 데이터를 비동기적으로 가져와 브라우저에서 화면의 일부만 업데이트 하여 렌더링 할 수 있다.

→ 표준화 된 방법 이전에는 브라우저마다 다른 방식으로 AJAX를 사용했으나, XHR이 표준화 되면서부터 브라우저에 상관 없이AJAX를 사용할 수 있게 되었다.

→ AJAX는 유저 중심 어플리케이션 개발이기 때문에 필요한 일부분만 렌더링하여 빠르고 더 많은 상호작용이 가능한 어플리케이션을 만들 수 있다.

→ 더 작은 대역폭

대역폭: 네트워크 통신 한 번에 보낼 수 있는 데이터의 크기.

전에는 서버로부터 완성된 HTML 파일을 받아와야했기 때문에 한번에 보내야 하는 데이터의 크기가 컸지만, AJAX에서는 필요한 데이터를 텍스트 형태(JSON, XML 등) 보내면 되기 때문에 비교적 데이터의 크기가 작다.

‣ 단점

→ SEO(검색 엔진 최적화 / Search Engine Optimization)에 불리

AJAX 방식의 웹 어플리케이션은 한 번 받은 HTML 렌더링 한 후, 서버에서 비동기적으로 필요한 데이터를 가져와 그려낸다.

→ 처음 받는 HTML 파일에는 데이터를 채우기 위한 틀만 작성되어 있는 경우가 많다.

검색 사이트에서는 전세계 사이트를 돌아다니며 각 사이트의 모든 정보를 긁어와, 사용자에게 검색 결과로 보여준다.

AJAX 방식의 웹 어플리케이션의 HTML 파일은 뼈대만 있고 데이터는 없기 때문에 사이트의 정보를 긁어가기 어렵다.

→ 뒤로가기 버튼 문제

일반적으로 사용자는 뒤로가기 버튼을 누르면 이전 상태로 돌아갈 거라고 생각하지만, AJAX에서는 이전 상태를 기억하지 않기 때문에 사용자가 의도한 대로 동작하지 않는다.

따라서 뒤로가기 등의 기능을 구현하기 위해서는 별도로 History API를 사용해야 한다.

### ② SSR과 CSR

‣ SSR(Server Side Rendering): 서버에서 웹 페이지를 브라우저로 보내기 전에, 서버에서 완전히 렌더링한다.

→ 브라우저가 서버의 URI로 GET 요청을 보내면, 서버는 정해진 웹 페이지 파일을 브라우저로 전송한다.

서버의 웹 페이지가 브라우저에 도착하면 완전히 렌더링되고, 웹 페이지의 내용에 데이터베이스의 데이터가 필요한 경우, 서버는 데이터베이스 데이터를 불러온 후 웹 페이지를 완전히 렌더링 된 페이지로 변환하고 브라우저에 응답으로 보낸다.

→ 웹 페이지를 살펴보던 사용자가 브라우저의 다른 경로로 이동하면 이동할 때마다 서버는 이 작업을 다시 수행한다.

‣ SSR을 쓰는 경우

→ SEO(검색 엔진 최적화)가 우선 순위인 경우

→ 웹 페이지의 첫 화면 렌더링이 빠르게 필요한 경우 단일 파일의 용량이 작은 SSR이 적합함.

→ 웹 페이지가 사용자와 상호작용이 적은 경우

‣ SSR 사용 예시: 네이버 블로그, 뉴욕 타임즈 홈페이지(SSR은 초기 로딩 속도가 빠르다)

‣ CSR(Client Side Rendering): 클라이언트에서 페이지를 렌더링하는 것(일반적으로 SSR의 반대로 여겨짐).

✷ 웹 개발에서 사용하는 대표적인 클라이언트는 웹 브라우저.

→ 서버로 브라우저의 요청을 보내면 서버는 웹 페이지의 골격이 될 웹 페이지(단일 페이지)와 함께 JavaScript 파일을 클라이언트에 보낸다.

→ 클라이언트가 웹 페이지를 받으면 웹 페이지와 함께 전달된 JavaScript 파일은 브라우저에서 웹 페이지를 완전히 렌더링 된 페이지로 바꾼다.

→ 웹 페이지에 필요한 내용이 데이터베이스에 저장된 데이터인 경우 브라우저는 데이터베이스에 저장된 데이터를 가져와서 웹 페이지에 렌더링을 해야 하는데, 이를 위해 API가 사용된다.

웹 페이지를 렌더링하는 데에 필요한 데이터를 API 요청으로 해소한다.

→ 브라우저가 다른 경로로 이동하면 CSR에서는 서버가 웹 페이지를 다시 보내지 않는다.

브라우저는 브라우저가 요청한 경로에 따라 페이지를 다시 렌더링한다.

이 때 보이는 웹 페이지의 파일은 맨 처음 서버로부터 전달받은 웹 페이지 파일과 동일한 파일이다.

‣ CSR을 사용하는 경우

→ SEO(검색 엔진 최적화)가 우선이 아닌 경우

→ 사이트에 풍부한 상호 작용이 있는 경우 빠른 라우팅으로 강력한 사용자 경험 제공.

→ 웹 애플리케이션 제작할 때 더 나은 사용자 경험(빠른 동적 렌더링 등)제공 가능.

✷ CSR 사용 예시: 아고다 등 예약 사이트들.

✅ SSR과 CSR의 차이점: 렌더링 되는 위치가 다르다. **SSR은 서버에서 페이지를 렌더링하고, CSR은 브라우저(클라이언트)에서 페이지를 렌더링한다.**

브라우저는 사용자가 다른 경로를 요청할 때마다 페이지를 새로고침 하지 않고, 동적으로 라우팅을 관리한다.

### ③ Browser Secury Model

‣ [CORS(Cross-Origin Resource Sharing)](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

[CORS](https://ingg.dev/cors/)

[그래서 CORS가 정확하게 뭐라구요?](https://hannut91.github.io/blogs/infra/cors)

[CORS -> 매우 중요한 내용이기 때문에 여러 링크를 타고 제대로 알아둘 것](https://hanamon.kr/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-http-options-%EB%A9%94%EC%86%8C%EB%93%9C%EB%A5%BC-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0%EC%99%80-cors%EB%9E%80/)

서버쪽에서 클라이언트를 대상으로 리소스의 허용 여부를 결정하는 방법

→ 브라우저가 자발적으로 브라우저 애플리케이션의 유저들을 보호하기 위해 따르는 정책.

→ 클라이언트와 서버가 서로 다른 origin에 있는 경우가 있으므로 CORS 기술이 도입되었다.

✷ <mark>클라이언트는 서버가 어떤 origin 요청을 허용하는지는 알 수 없다.</mark> 클라이언트에서 요청을 보낸 후, 서버로부터 받은 Access-Control-Allow-Origin 헤더 속성을 통해서 접속 가능 여부 확인.

→ 같은 origin에서 fetch를 시도하면 CORS 문제가 발생하지 않는다.

![](https://blog.kakaocdn.net/dn/dherLF/btroEnL1w73/TwqKZjuJQoI6EP5cg0n600/img.png)

(출처: 코드스테이츠)

✅ **<mark>JS 코드가 실행이 되면 simple request가 아닌 이상 브라우저가 자발적으로 서버에 preflight request를 날린다.</mark>**

**<mark>그 다음에 실제로 내가 원했던 요청이 날아가고, 그에 대한 응답을 받아 브라우저는 JS script에 그 응답을 처리할 수 있다.</mark>**

‣ 출처(origin)가 다르다고 판단되는 경우

프로토콜 - http와 https는 프로토콜이 다르다.

도메인 - domain.com과 other-domain.com은 다르다.

포트 번호 → 8080포트와 3000포트는 다르다.

ex)

```js
Simple Request: GET 메소드에 의해 요청이 이루어진다.

const invocation = next XMLHTTPRequest();
const url = 'http://bar.other/resources/public-data/';

function callOtherDomain() {
  if(invocation) {
    invocation.open('GET', url, true);
    invocation.onreadystatechange = handler;
    invocation.send();
    }
}
```

![](https://blog.kakaocdn.net/dn/bLti8F/btroDqI3hvr/yhVh7YIKTDQPWHngJDK05K/img.png)

Client와 Server가 있는데, 여기서 GET으로 다른 origin으로 Server-b.com을 요청

(코드에서는 'http://bar.other/resources/public-data/')

simple request에 해당되기 때문에 Access-Control-Allow-Origin: \*(asterisk)해서 200 OK를 받음.

ex) 클라이언트와 서버간의 통신 예제

```
// 요청하는 쪽
GET /resources/public-data/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,_/_;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
Origin: https://foo.example --> 요청하는 오리진(출처)
```

```
// 응답하는 쪽
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2
Access-Control-Allow-Origin: \*
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Transfer-Encoding: chunked
Content-Type: application/xml

[…XML Data…]
```

서버는 이에 대한 응답으로 Access-Control-Allow-Origin 헤더를 다시 전송한다.

가장 간단한 접근 제어 프로토콜은 Origin 헤더와 Access-Control-Allow-Origin 을 사용하는 것이다.

이 경우 서버는 Access-Control-Allow-Origin: \*, 으로 응답해야 하며, 모든 도메인에서 접근할 수 있다는 뜻이다.

https://bar.other 의 리소스 소유자가 오직 https://foo.example 의 요청만 리소스에 대한 접근을 허용하려는 경우 Access-Control-Allow-Origin: https://foo.example
을 전송한다.

ex) Preflighted Requests: 실제 요청이 안전한지 서버가 미리 파악할 수 있도록 하는 수단

→ 실질적인 요청 전, OPTIONS 메소드에 의해 요청이 이루어진다.

→ 모든 cross origin 요청이 preflight request를 발생시키는 것은 아니다.

```js
const invocation = new XMLHttpRequest();
const url = "http://bar.other/resources/post-here/";
const body = '<?xml version="1.0"?><person><name>Arun</name></person>';

function callOhterDomain() {
  if (invocation) {
    invocation.open("POST", url, true);

    // 기본 세팅 헤더가 아닌 내가 원하는 헤더를 세팅하는 경우
    invocation.setRequestHeader("X-PINGOTHER", "pingpong");
    invocation.setRequestHeader("Content-type", "apllication/xml");

    invocation.onreadystatechange = handler;
    invocation.send(body);
  }
}
```

![](https://blog.kakaocdn.net/dn/baXK9U/btroJDticJk/0FLkQ8GA1REmfbxiRmkYSK/img.png)

<mark>실제 POST 요청에는 Access-Control-Request-\* 헤더가 포함되지 않는다. OPTIONS 요청에만 필요하다.</mark>

클라이언트와 서버간의 완전한 통신. 첫 번째 통신은 preflight request/response.

```
OPTIONS /resources/post-here/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,_/_;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
Origin: http://foo.example
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER, Content-Type

HTTP/1.1 204 No Content
Date: Mon, 01 Dec 2008 01:15:39 GMT
Server: Apache/2
Access-Control-Allow-Origin: https://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
Access-Control-Max-Age: 86400
Vary: Accept-Encoding, Origin
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
```

preflight request가 완료되면 실제 요청을 전송한다.

```
POST /resources/post-here/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,_/_;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
X-PINGOTHER: pingpong
Content-Type: text/xml; charset=UTF-8
Referer: https://foo.example/examples/preflightInvocation.html
Content-Length: 55
Origin: https://foo.example
Pragma: no-cache
Cache-Control: no-cache

<person><name>Arun</name></person>

HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:15:40 GMT
Server: Apache/2
Access-Control-Allow-Origin: https://foo.example
Vary: Accept-Encoding, Origin
Content-Encoding: gzip
Content-Length: 235
Keep-Alive: timeout=2, max=99
Connection: Keep-Alive
Content-Type: text/plain

[Some GZIP'd payload]
```

‣ XSS(Cross-site Scripting)

‣ CSRF(Cross-Site Request Forgery)

## 7. REST API(Representational State Transfer)

웹에서 사용되는 데이터나 자원(Resource)을 HTTP URI로 표현하고, HTTP 프로토콜을 통해 요청과 응답을 정의하는 방식.

→ 클라이언트와 서버 사이에는 데이터와 리소스를 요청하고 요청에 따른 응답을 전달하기 위한 API가 필요하다. API를 보고 클라이언트는 서버에 요청하고, 이에 대한 응답을 다시 서버에서 클라이언트로 전송하게 된다.

⇒ HTTP 프로토콜 기반으로 요청과 응답에 따라 리소스를 주고받기 위해서 알아보기 쉽고 잘 작성된 API가 수행해야 하므로 서로 잘 알아볼 수 있도록 작성하는 것이 중요하다.

### ① REST API 작성 시 지켜야 할 규칙들

→ 로이 필딩이 논문에서 제시한 REST 방법론을 보다 더 실용적으로 적용하기 위해 레오나르드 리차드슨은 REST API를 잘 적용하기 위한 4단계 모델을 만들었다.

→ 로이 필딩은 모델의 모든 단계를 충족해야 REST API라고 부를 수 있다고 주장했으나 실제로 엄밀하게 3단계까지 지키기 어렵기 때문에 2단계까지만 적용해도 좋은 API 디자인이라고 볼 수 있고, 이런 경우 HTTP API 라고도 부른다.

‣ 리차드슨의 REST API를 잘 적용하기 위한 REST 성숙도 모델 구조화

![](https://blog.kakaocdn.net/dn/bnbUXf/btroJ6JovVY/tQHRJP5DZwtkSyk9uqOuiK/img.png)

‣ 0단계: 단순히 HTTP 프로토콜을 사용하기만 해도 된다고 한다.

0단계는 좋은 REST API를 작성하기 위한 기본 단계.

ex)

```js
// 요청
예약 가능한 시간 확인
POST / appointment HTTP/1.1
[헤더 생략]
{
  "date": "2022-08-10",
  "doctor": "Harvey"
}

// 응답
HTTP/1.1 200 OK
[헤더 생략]
{
"slots" : [
  { "doctor": "Harvey", "start": "09:00", "end": "12:00" },
  { "doctor": "Harvey", "start": "13:00", "end": "15:00" }
  ]
}

// 요청
특정 시간에 예약
POST / appointment HTTP/1.1
[헤더 생략]
{
  "doctor": "Harvey",
  "start": "10:00",
  "end": "11:00",
  "patient": "Sam"
}

// 응답
HTTP/1.1 200 OK
[헤더 생략]
```

‣ 1단계: 개별 리소스와의 통신을 준수해야 한다. 요청하는 리소스가 무엇인지에 따라 각기 다른 엔드포인트로 구분하여 사용해야 한다.

```js
// 요청
예약 가능한 시간 확인
POST / doctors/Harvey HTTP/1.1
[헤더 생략]
{
  "date": "2022-08-10"
}

// 응답
HTTP/1.1 200 OK
[헤더 생략]
{
"slots" : [
  { "id": "123", "doctor": "Harvey", "start": "09:00", "end": "12:00" },
  { "id": "124", "doctor": "Harvey", "start": "13:00", "end": "15:00" }
  ]
}

// 요청
특정 시간에 예약
POST / slots/123 HTTP/1.1
[헤더 생략]
{
  "patient": "Sam"
}

// 응답
HTTP/1.1 200 OK
[헤더 생략]
{
  "appoinment": {
    "slot": { "id": "123", "doctor": "Harvey", ... },
    "patient": "Sam",
    "reason": "해당 시간은 이미 예약되어 있습니다."
    }
}
```

위의 예시에서 예약 가능한 시간 확인이라는 요청의 응답으로 받게 되는 자원(리소스)은 의사의 예약 가능한 시간대이다.

그렇기 때문에 요청 시 /doctors/Harvey 라는 엔드포인트를 사용한 것을 볼 수 있다.

뿐만 아니라, 특정 시간에 예약하게 되면, 실제 slot이라는 리소스의 123이라는 id를 가진 리소스가 변경되기 때문에,하단의 특정 시간에 예약이라는 요청에서는 /slots/123으로 실제 변경되는 리소스를 엔드포인트로 사용하였다.

어떤 리소스를 변화시키는지 혹은 어떤 응답이 제공되는지에 따라 각기 다른 엔드포인트를 사용하기 때문에, 적절한 엔드포인트를 작성하는 것이 중요하다.

엔드포인트 작성 시에는 동사, HTTP 메소드, 혹은 어떤 행위에 대한 단어 사용은 지양하고, 리소스에 집중해 명사 형태의 단어로 작성하는 것이 바람직하다.

⇒ 요청에 따른 응답으로 리소스를 전달할 때 사용한 리소스에 대한 정보와 함께 리소스 사용에 대한 성공/실패 여부 반환.

만약 환자가 의사에게 9시에 예약을 진행하였으나 해당 시간이 마감되어 예약이 불가능하다고 가정할 때, 리소스 사용에 대한 실패 여부를 포함한 응답을 받아야 한다.

‣ 2단계: CRUD에 맞게 적절한 HTTP 메소드를 사용하는 것에 중점을 둔다.

0단계와 1단계에서는 모든 요청을 CRUD에 상관없이 POST로 하고 있으나 REST 성숙도 모델 2단계에 따르면 이는 CRUD에 따른 적합한 메소드를 사용한 것은 아니다.

```js
// 요청
예약 가능한 시간 확인
GET / doctors/Harvey slots?data=2022-08-10 HTTP/1.1
[헤더 생략]

// 응답
HTTP/1.1 200 OK
[헤더 생략]
{
  "slots" : [
    { "id": "123", "doctor": "Harvey", ... },
    { "id": "124", "doctor": "Harvey", ... }
    ]
}

// 요청
특정 시간에 예약
POST / slots/123 HTTP/1.1
[헤더 생략]
{
  "patient": "Sam"
}

// 응답
HTTP/1.1 201 Created
Location: slots/123/appoinment
[헤더 생략]
{
  "appoinment": {
    "slot": { "id": "123", "doctor": "Harvey", ... },
    "patient": "Sam"
    }
}
```

→ 예약 가능한 시간을 확인한다는 것은 예약 가능한 시간을 조회(READ)하는 행위를 의미하고, 특정 시간에 예약한다는 것은 해당 특정 시간에 예약을 생성(CREATE)한다는 것과 같다.

그렇기 때문에 조회(READ)하기 위해서는 GET 메소드를 사용하여 요청을 보내고, 이때 GET 메소드는 body를 가지지 않기 때문에 query parameter를 사용하여 필요한 리소스를 전달한다.

→ 또한 예약을 생성(CREATE)하기 위해서는 POST 메소드를 사용하여 요청을 보내는 것이 좋으며 POST 요청에 대한 응답이 어떻게 반환되는지도 중요하다.

이 경우 응답은 새롭게 생성된 리소스를 보내주기 때문에, 응답 코드도 201 Created 로 명확하게 작성해야 하며, 관련 리소스를 클라이언트가 Location 헤더에 작성된 URI를 통해 확인 할 수 있도록 해야한다.

✷ 메소드 사용의 규칙

- GET 메소드 같은 경우는 서버의 데이터를 변화시키지 않는 요청에 사용해야 한다.

- POST 는 요청마다 새로운 리소스를 생성하고 PUT 은 요청마다 같은 리소스를 반환한다.

멱등성을 가지는 메소드 PUT과 그렇지 않은 POST는 구분하여 사용해야 한다.

✷ 멱등성

‣ 동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때 매 요청마다 같은 리소스를 반환하는 특징을 [멱등(idempotent)](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)하다고 한다.

- PUT은 교체, PATCH는 수정의 용도로 구분 지어 사용한다.

[✷ PUT, PATCH 차이점](https://velog.io/@dulcis-hortus/PUT%EA%B3%BC-PATCH%EC%9D%98-%EC%B0%A8%EC%9D%B4)

‣ 3단계(무조건적인 적용은 아님): HATEOAS(Hypertext As The Engine Of Application State)라는 하이퍼미디어 컨트롤을 적용.

⇒ 3단계의 요청은 2단계와 다르지 않지만, 응답에는 리소스의 URI를 포함한 링크 요소를 삽입하여 작성한다.

응답에 들어가는 링크 요소는 응답을 받은 다음에 할 수 있는 다양한 액션들을 위해 많은 하이퍼미디어 컨트롤을 포함한다.

```js
// 요청
예약 가능한 시간 확인
GET / doctors/Harvey slots?data=2022-08-10 HTTP/1.1
[헤더 생략]

// 응답
HTTP/1.1 200 OK
[헤더 생략]
{
  "slots" : [
    { "id": "123", "doctor": "Harvey", ... }, ...
    ],
    "links" : {
      "appoinment" : {
        "href":"http://localhost:8080/slots/123",
        "method" : "POST"
        }
    }
}

// 요청
특정 시간에 예약
POST / slots/123 HTTP/1.1
[헤더 생략]
{
  "patient": "Sam"
}

// 응답
HTTP/1.1 201 Created
Location: slots/123/appoinment
[헤더 생략]
{
  "appoinment": {
    "slot": { "id": "123", "doctor": "Harvey", ... },
    "patient": "Sam"
    },
    "links" : {
      "self": {
        "href": "http://localhost:8080/slots/123",
        "method" : "GET"
        }
        "cancel" : {
          "href": "http://localhost:8080/slots/cancel",
          "method" : "DELETE"
          }
    }
}
```

의사의 예약 가능 시간을 확인한 후 그 시간대에 예약을 할 수 있는 링크를 삽입하거나, 특정 시간에 예약을 완료하고 나서

그 예약을 다시 확인할 수 있도록 링크를 작성해 넣을 수도 있다.

→ 응답 내에 새로운 링크를 넣어 새로운 기능에 접근할 수 있도록 하는 것이 3단계의 중요 포인트.

⇒ <mark>리소스 중심의 올바른 엔드포인트 작성, 적절한 응답 코드와 리소스에 대한 정보 기재, CRUD에 적합한 HTTP 메소드 사용 등을 고려해야 좋은 REST API를 디자인 할 수 있다.</mark>

### ② Open API

누구에게나 열려 있지만, 무제한 이용이라는 의미는 아님. → 기관이나 API마다 정해진 이용 수칙이 있고, 그 이용 수칙에 따라 제한사항(가격, 정보의 제한 등)이 있을 수 있다.

ex) [Open Weather Map](https://openweathermap.org/api)

이 사이트는 이렇게 데이터를 제공한다.

‣ 제한적이나마 무료로 날씨 API를 사용할 수 있다.

→ 프리 플랜에서는 기본적으로 분당 60번, 달마다 1백 번 호출이 가능하다.

‣ 데이터를 JSON 형태로 응답한다.

### ③ API key

서버의 문을 여는 열쇠(가끔 필요하지 않은 경우도 있음).

클라이언트의 요청에 따라 서버에서 응답한다 === 서버를 운용하는 데에 비용이 발생한다.

⇒ 서버 입장에서 아무런 조건 없이 익명의 클라이언트에게 데이터를 제공할 의무도, 이유도 없다.

그래서 로그인된 이용자에게만 자원에 접근할 수 있는 권한을 API Key의 형태로 제공하고, 데이터를 요청할 때 API key를 같이 전달해야만 원하는 응답을 받을 수 있다.
