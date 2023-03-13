---
layout: single
title: "D+65 인터넷 프로토콜, HTTP 헤더, 웹 캐시"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

[✷ HTTP protocol](https://gmlwjd9405.github.io/2019/04/17/what-is-http-protocol.html)

[✷ OSI 7 Layers](https://shlee0882.tistory.com/110)

## 1. 인터넷 프로토콜

IP(Internet Protocol)와 IP Packet: 클라이언트와 서버 사이의 수많은 노드들을 지나 데이터가 전달되어 통신하기 위한 규칙

✷ 노드: 하나의 서버 컴퓨터

① 클라이언트 패킷 전달

![](https://blog.kakaocdn.net/dn/ct01mG/btrwWgXH7gQ/ssK8urs41o0SAJKtgv0gDK/img.png)

→ IP는 지정한 IP Address에 Packet이라는 통신 단위로 데이터 전달을 한다.

→ IP 패킷에는 전송 데이터를 무사히 전송하기 위해 출발지 IP, 목적지 IP와 같은 정보가 포함되어 있다. 패킷 단위로 전송하면 노드들은 목적지 IP에 도달하기 위해 서로 데이터를 전달하고, 이를 통해 정확한 목적지로 패킷을 전송할 수 있다.

② 서버 패킷 전달

![](https://blog.kakaocdn.net/dn/4dTmo/btrwMGjx9m2/hK9FH5diKYKDRJ2Rr7qMk1/img.png)

→ 서버에서 무사히 데이터를 전송받아 응답을 돌려줄 때 IP 패킷을 이용하여 클라이언트에 응답을 전달한다.

③ IP 프로토콜의 한계

‣ 비연결성

![](https://blog.kakaocdn.net/dn/bLnsSS/btrwTdAVMUe/fmdn9eivqrf6VtFMpOcVnK/img.png)

패킷을 받을 대상이 없거나 서비스 불능 상태여도 클라이언트는 서버의 상태를 파악할 방법이 없어 패킷을 그대로 전송.

‣ 비신뢰성

![](https://blog.kakaocdn.net/dn/c5NQbn/btrwUkGlOMB/5jXnr9qQlWwK9OvKBJBhH1/img.png)

→ 중간에 있는 서버가 데이터를 전달하던 중 장애가 생겨 패킷이 사라지거나 클라이언트는 이를 파악할 방법이 없다.

![](https://blog.kakaocdn.net/dn/s83oV/btrwMFE2cOV/WoPw60EL1rrQqZF8YdtyVk/img.png)

→ 전달 데이터의 용량이 클 경우 이를 패킷 단위로 나누어 데이터를 전달하게 되는데 이때 패킷들은 중간에 서로 다른 노드들을 통해 전달될 수 있고, 이로 인해 클라이언트가 의도하지 않은 순서로 패킷이 도착할 수 있기 때문에 패킷의 순서를 보장할 수 없음

## 2. TCP / UDP

![](https://blog.kakaocdn.net/dn/ozaZu/btrwUkzx3Du/Nem8gkCZchgZmrpjoJ2iB0/img.png)

✷ TCP/IP 4 계층이 OSI 7 계층보다 먼저 개발되었으며, TCP/IP 프로토콜의 계층은 OSI 모델의 계층과 정확하게 일치하는 것은 아니다. → IP 프로토콜보다 더 높은 계층에 TCP 프로토콜이 존재하기 때문에 IP 프로토콜의 한계 보완 가능.

![](https://blog.kakaocdn.net/dn/c8TdRJ/btrwTbJUnLZ/hGqkKsYOWCfn3IvtrWAPk0/img.png)

① HTTP 메시지가 생성되면 Socket 라이브러리를 통해 전달된다.

② IP 패킷을 생성하기 전 TCP 세그먼트를 생성한다.

TCP 세그먼트에는 IP 패킷의 출발지 IP, 목적지 IP 정보를 보완할 수 있는 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보 등을 포함한다.

③ 이렇게 생성된 TCP/IP 패킷은 LAN 카드와 같은 물리적 계층을 지나기 위해 이더넷 프레임 워크에 포함되어 서버로 전송된다.

‣ 네트워크 소켓(Network Socket): 프로그램이 네트워크에서 데이터를 송수신할 수 있도록(=네트워크 환경에 연결할 수 있게) 만들어진 연결부

### ① TCP(전송 제어 프로토콜 / Transmission Control Protocol)

같은 계층에 속한 UDP에 비해 상대적으로 신뢰할 수 있는 프로토콜

‣ TCP 특징

![](https://blog.kakaocdn.net/dn/z1CsO/btrwMGDTQhY/67f8XlxtKDnyQYeVtSAsv0/img.png)

→ 연결 지향형 프로토콜 - TCP 3 way handshake(가상 연결)

‣ 연결 방식

① 클라이언트는 서버에 접속을 요청하는 SYN(Synchronize) 패킷을 보낸다.

② 서버는 SYN 요청을 받고 클라이언트에게 요청을 수락한다는 ACK(Acknowledgment / 승인)와 SYN이 설정된 패킷을 발송, 클라이언트가 다시 ACK로 응답하기를 기다린다.

③ 클라이언트가 서버에게 ACK를 보내면 이 이후로 연결이 성립, 데이터를 전송할 수 있다.

④ 만약 서버가 꺼져있다면 클라이언트가 SYN을 보내고 서버에서 응답이 없기 때문에 데이터를 보내지 않는다. ⇒ 현재에는 최적화가 이루어져 3번 ACK을 보낼 때 데이터를 함께 보내기도 한다.

![](https://blog.kakaocdn.net/dn/dXfghO/btrwWlYVmKY/lPdt8B4LFHhr2U8f6PhNVk/img.png)

→ 데이터 전달 보증: 데이터 전송이 성공적으로 이루어진다면 이에 대한 응답을 돌려주기 때문에 IP 패킷의 한계인 비연결성을 보완할 수 있다.

![](https://blog.kakaocdn.net/dn/EFmuN/btrwRxGq6ln/uVmQmkZ7aiue4YwPNUn63K/img.png)

→ 순서 보장: 패킷이 순서대로 도착하지 않으면 TCP 세그먼트에 있는 정보를 토대로 패킷 전송 재요청이 가능하여 IP 패킷의 한계인 비신뢰성(순서 보장 X) 보완 가능.

### ② UDP(사용자 데이터그램 프로토콜 / User Datagram Protocol)

IP 프로토콜에 PORT, 체크섬 필드 정보만 추가된 단순한 프로토콜. TCP보다는 신뢰성이 낮음.

✷ 체크섬(checksum): 중복 검사의 한 형태, 오류 정정을 통해 공간(전자 통신)이나 시간(기억 장치) 속에서 송신된 자료의 무결성을 보호하는 단순한 방법.

→ 기능이 거의 없어 커스터마이징이 가능함(하얀 도화지에 비유).

→ 비연결지향

→ 데이터 전달 보증, 순서 보장 X - 단순하고 빠름

→ 신뢰성보다는 연속성이 중요한 서비스(실시간 스트리밍 등)에 자주 사용됨.

![](https://blog.kakaocdn.net/dn/bZIlDK/btrwVr6mVU2/KLvrZ9el7fPqk6nGq8CkCK/img.png)

‣ TCP/IP의 경우 기본적으로 연결을 유지한다(connection oriented). 연결을 유지하는 모델에서는 클라이언트는 요청을 보내지 않더라도 계속 연결을 유지해야 하고, 이런 경우 연결을 유지하는 서버의 자원이 계속 소모된다.

## 3. HTTP

‣ HTTP 역사

![](https://blog.kakaocdn.net/dn/ATGOx/btrwTOAVgMd/bZbBWEv3EicL81PfQarvTk/img.png)

‣ HTTP 특징

![](https://blog.kakaocdn.net/dn/EGrWq/btrwPbwT9aG/dcXtkQ9bDcN97IkBPukFpk/img.png)

→ 클라이언트 서버 구조: 클라이언트가 서버에 요청을 보내고 응답을 대기하면, 서버는 그에 대한 결과를 만들어 응답을 보내는 구조.(Request - Response 구조)

‣ 무상태(stateless)프로토콜

HTTP에서는 서버가 클라이언트의 상태를 보존하지 않는 무상태 프로토콜이다.

🌟 **<mark>클라이언트가 준 정보(상태)를 서버가 저장하고 있으면 stateful, 저장하지 않으면 stateless</mark>**

• 장점

![](https://blog.kakaocdn.net/dn/FrS5v/btrwTbwuJxJ/WM56c7yreWevb8qEAywjl1/img.png)

갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다(아무 서버나 호출해도 된다).

![](https://blog.kakaocdn.net/dn/cO8fm5/btrwXzCODkC/a3aTkcx0I0xhosxQuAVCqK/img.png)

서버에 장애가 생겨도 다른 서버에서 응답을 전달하면 되기 때문에 클라이언트는 다시 요청할 필요 없음.

![](https://blog.kakaocdn.net/dn/byZC7Q/btrwVdNDM6k/iQcLeg84haLIAvtNnyiWOK/img.png)

응답 서버를 쉽게 바꿀 수 있어 무한한 서버 증설이 가능하다(스케일 아웃 - 수평 확장 유리)

• 한계

무상태로 설계할 수 있는 경우도 있지만, 없는 경우도 있다. → 로그인이 필요 없는 단순 서비스 소개 화면 같은 경우는 무상태로 설계 가능, 로그인이 필요한 서비스인 경우 유저의 상태를 유지해야 하기 때문에 브라우저 쿠키, 서버 세션, 토큰 등을 이용한다.

‣ 비연결성(connectionless): HTTP는 기본적으로 연결을 유지하지 않는 모델. 실제로 요청을 주고받을 때만 연결을 유지하고 응답을 주고 나면 TCP/IP 연결을 끊어 최소한의 자원으로 서버 유지를 가능하게 한다.

• 장점

트래픽이 많지 않고 빠른 응답을 제공할 수 있는 경우 비연결성의 특징이 효율적으로 작동한다.(일반적으로 초 단위 이하의 빠른 속도로 응답함)

ex) 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십 개 이하로 매우 작음. 웹 브라우저에서 연속해서 검색 버튼을 누르지 않는 것처럼.

• 한계

트래픽이 많고 큰 규모의 서비스를 운영할 때는 한계를 보인다. TCP/IP 연결을 새로 맺어야 하기 때문에 3 way handshake 시간이 추가된다.

웹 브라우저로 사이트를 요청하면 HTML과 CSS, JS, 추가 이미지 등 수많은 자원이 함께 다운로드된다.

⇒ 해당 자원들을 각각 보낼 때마다 연결을 끊고 다시 연결하는 것을 반복하는 것은 비효율적이기 때문에 지금은 HTTP 지속 연결(Persistent Connections)로 문제를 해결한다.

✷ HTTP 지속 연결(Persistent Connections)

![](https://blog.kakaocdn.net/dn/VNztO/btrwPbjpm4m/Omm628f6jvH7yKGR3DtHz0/img.png)

HTTP 초기에는 각각의 자원을 다운로드하기 위해 연결과 종료를 반복해야 했지만 지속 연결에서는 연결이 이루어지고 난 뒤 각각의 자원들을 요청하고 모든 자원에 대한 응답이 돌아온 후에 연결을 종료한다.

→ HTTP 메시지

→ 단순함, 확장 가능

## 4. HTTP 헤더

HTTP 전송에 필요한 모든 부가정보(메시지 바디의 내용, 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보 ... )를 담기 위해 사용한다. → 필요시 임의의 헤더 추가 기능

### ① 표현 헤더(Representation Headers)

‣ 데이터 메시지 본문(message body)를 통해 표현 데이터를 전달하는데, 이 메시지 본문을 페이 로드(payload)라고 한다.

‣ 표현은 요청이나 응답에서 전달할 실제 데이터 ⇒ 표현 헤더는 표현 데이터를 해석할 수 있는 정보(데이터 유형(html, json), 데이터 길이, 압축 정보 등) 제공

```
// HTTP 헤더 형식
GET /search?q=codestates&hl=ko HTTP/1.1

<field name> : <field-value>
Host: www.google.com

HTTP/1.1 200 OK

<field name> : <field-value>
Content-type: text/html;charset=UTF-8
// Content-type: application/json
Content-Length: 3423

field name은 대소문자 구분 없음
```

→ [Content-Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Type): 표현 데이터의 형식.

> Text/htaml; charset=utf-8
>
> application/json
>
> Image/png

→ [Content-Length](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Length): 표현 데이터의 길이. 바이트 단위이며 [Transfer-Encoding(전송 코딩)](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Transfer-Encoding)을 사용하면 Content-Length 사용하면 안 됨.

✷ Transfer-Encoding: 전송 시 어떤 인코딩 방법을 사용할 것인가를 명시한다. → 그러나 현재는 Transfer-Encoding보다는 Content-Encoding을 사용하며, Transfer-Encoding을 사용하는 경우 chunked의 방식으로 사용한다.

→ chunked 방식의 인코딩은 많은 양의 데이터를 분할하여 보내기 때문에 전체 데이터의 크기를 알 수 없기 때문에 표현 데이터의 길이를 명시해야 하는 Content-Length 헤더와 함께 사용할 수 없다.

→ [Content-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Encoding): 표현 데이터의 압축 방식. 표현 데이터를 압축하기 위해 사용하는 것으로 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가, 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제.

> gzip
>
> deflate
>
> identity

→ [Content-Language](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Language): 표현 데이터의 자연 언어

> ko
>
> en
>
> en-US

⇒ 표현 헤더는 요청, 응답 둘 다 사용함.

### ② HTTP 주요 헤더

![](https://blog.kakaocdn.net/dn/de9LCl/btrwVdfMiUN/Qh56qS185o00xtkiYhdlU0/img.png)

‣ 요청(Request)에서 사용되는 헤더

• From: 유저 에이전트의 이메일 정보 → 검색 엔진에서 주로 사용하며 일반적으로 잘 사용하지 않는다.

• Referer: 현재 요청된 페이지의 이전 웹 페이지 주소(feferrer의 오탈자이지만 스펙으로 굳어짐). → Referer를 사용하면 유입 경로 수집 가능 → A에서 B로 이동하는 경우 B를 요청할 때 Referer: A를 포함해서 요청

• User-Agent: 유저 에이전트 애플리케이션 정보

→ 클라이언트의 애플리케이션 정보(웹 브라우저 정보 등)

→ 통계 정보

→ 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능

ex)

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/ 537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
```

• Host: 요청한 호스트 정보(도메인)

→ 필수 헤더

→ 하나의 서버가 여러 도메인을 처리해야 할 때 호스트 정보를 명시하기 위해 사용함

→ 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 호스트 정보를 명시하기 위해 사용함.

![](https://blog.kakaocdn.net/dn/cfD06k/btrwXycRA7X/YHqk1r8Jc3Xbw3v8UkigS0/img.png)

‣ Origin: 서버로 POST 요청을 보낼 때 요청을 시작한 주소를 나타냄.

→ 여기서 요청을 보낸 주소와 받는 주소가 다르면 CORS 에러 발생.

→ 응답 헤더의 Access-Control-Allow-Origin과 관련

‣ Authorization: 인증 토큰(JWT 등)을 서버로 보낼 때 사용하는 헤더 → "토큰의 종류 + 실제 토큰 문자"를 전송

ex)

```
Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l
```

‣ 응답(Response)에서 사용되는 헤더

• Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보

ex)

```
Sever: Apache/2.2.22 (Debian)
Server: nginx
```

• Date: 메시지가 발생한 날짜와 시간

ex)

```
Date: Tue, 22 Mar 2022 22:59:42 GMT
```

• Location: 페이지 리디렉션

웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면 Location 위치로 자동 이동(리다이렉트)

→ 201(Created): Location 값은 요청에 의해 생성된 리소스 URI

→ 3xx(Redirection): Location 값은 요청을 자동으로 리디렉션 하기 위한 대상 리소스를 가리킴

• Allow: 허용 가능한 HTTP 메소드

→ 405(Method Not Allowed)에서 응답에 포함

ex)

```
Allow: GET, HEAD, PUT
```

• Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

→ 503(Service Unavailable): 서비스가 언제까지 불능인지 알려 줄 수 있음

ex)

```
Retry-After: Fri, 31 Dec 2020 23:59:59 GMT(날짜 표기)
Retry-After: 120(초 단위 표기)
```

### ③ HTTP 헤더를 이용한 콘텐츠 협상(Content Negotiation)

[콘텐츠 협상(1)](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation)

✷ [콘텐츠 협상](https://velog.io/@devapploper/http-Content-Negotiation)

클라이언트가 선호하는 표현 요청(협상 헤더는 요청 시에만 사용)

→ Accept: 클라이언트가 선호하는 미디어 타입 전달

→ Accept-Charset: 클라이언트가 선호하는 문자 인코딩

→ Accept-Encoding: 클라이언트가 선호하는 압축 인코딩

![](https://blog.kakaocdn.net/dn/blef5w/btrwWnWUk1q/njeFLitr6kXKjJbiCEGaUK/img.png)

→ Accept-Language: 클라이언트가 선호하는 자연 언어

• 한국어 브라우저에서 콘텐츠 협상이 적용되지 않으면 서버는 요청으로 받은 우선순위가 없기 때문에 기본 언어로 응답하고, ko를 작성하여 요청하면 서버에서 해당 우선순위 언어를 지원할 수 있어 한국어 응답을 돌려준다.

• Accept-Language에 요청했으나 기본 언어로 요청한 언어를 지원하지 않는 경우(=== 서버에서 지원하는 언어는 여러 개인데 클라이언트가 최우선으로 선호하는 언어를 지원하지 않는 경우)

![](https://blog.kakaocdn.net/dn/bSmgDn/btrwT1NyIQV/BPo5pn65WhaNc0G3Kpubl1/img.png)

⇒ 협상 헤더에서 원하는 콘텐츠에 대한 우선순위 지정 가능

```
GET /event
Accept-Language:ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

⇒ q(Quality Values)를 사용하여 0~1 사이의 값을 지정할 수 있다. 숫자가 클수록 높은 우선순위를 가진다. 생략하는 경우는 1이다. ko-KR은 ko-KR;q=1 을 줄여서 쓰는 것이다.

⇒ 0~1까지 우선순위를 부여하면 서버는 이를 토대로 응답을 지원한다.

## 5. 웹 캐시

### ① 캐시의 기본 원리 및 적용

‣ 캐시가 없을 때

![](https://blog.kakaocdn.net/dn/wIMyf/btrwTc3ABGz/FH5kdyLp8wVp9AkkqiKc70/img.png)

→ 데이터가 변경되지 않아도 계속 네트워크를 통해 데이터를 다운로드 받아야한다.

→ 용량이 클수록 비용이 커지고 브라우저의 로딩 속도가 느려져 느린 사용자 경험을 제공하게 된다.

‣ 캐시 적용

✷ 캐시(cache): 데이터나 값을 미리 복사해놓는 임시 저장소

→ 캐시의 접근 시간에 비해 원래 데이터를 접근하는 시간이 오래 걸리는 경우나 값을 다시 계산하는 시간을 절약하고 싶은 경우 사용한다.

![](https://blog.kakaocdn.net/dn/JmgLB/btrz7zACfkO/oRTbDVHv7cLUtoBnIaHsAk/img.png)

→ 캐시에 데이터를 미리 복사해놓으면 계산이나 접근시간 없이 더 빠른 속도로 데이터 접근 가능

→ 브라우저에 캐시를 저장할 때 헤더에 cache-control 속성을 통해 캐시 유효 시간 지정 가능

→ 응답을 받았을 때 브라우저 캐시에 해당 응답 결과 저장, 지정한 시간만큼 유효한다.

⇒ 캐시 가능 시간 동안 네트워크를 사용하지 않아도 되어 비싼 네트워크 사용량을 줄이고 브라우저 로딩 속도가 매우 빨라 빠른 사용자 경험을 제공할 수 있다.

‣ 캐시를 적용했지만 캐시 시간이 초과했을 경우

![](https://blog.kakaocdn.net/dn/UBL9Q/btrw2OfDuPA/lqSWbvvpjJz6lNLa6QtqMK/img.png)

![](https://blog.kakaocdn.net/dn/cOjapq/btrwRyFTcz6/4jBkh6lY68UFKymck5AMCK/img.png)

→ 서버를 통해 데이터를 다시 조회하고 캐시를 갱신하는데 이때 다시 네트워크 다운로드가 발생한다.

→ 응답 결과를 브라우저가 렌더링 하면 브라우저 캐시는 기존 캐시를 지우고 새 캐시로 데이터를 업데이트하는데, 이 과정에서 캐시 유효시간이 다시 초기화된다.

### ② 캐시를 제어할 수 있는 검증 헤더와 이를 이용한 조건부 요청

[✷ HTTP 조건부 요청](https://ngwoon.github.io/network/2020/10/03/HTTP-%EC%A1%B0%EA%B1%B4%EB%B6%80-%EC%9A%94%EC%B2%AD/)

![](https://blog.kakaocdn.net/dn/ZAd8E/btrwTvnSHCU/zzmRi3YFgU0FMJ8iDDxFd0/img.png)

→ 검증 헤더 Last Modified를 이용하여 캐시의 수정 시간을 알 수 있다.

‣ Last Modified: 데이터가 마지막으로 수정된 시간 정보를 헤더에 포함하여 응답 결과를 캐시에 저장할 때 데이터 최종 수정일도 저장된다.

![](https://blog.kakaocdn.net/dn/n9XDN/btrwTwmKiz1/5BHaNgDbpW2GRVJY661N0k/img.png)

① 데이터가 수정되었는지 검증

② 수정되지 않았다면 바디를 제외한 HTTP 헤더만 전송 → 서버의 해당 자료의 최종 수정일과 비교하여 데이터가 수정되지 않았을 경우 응답 메시지에 담아 알려준다. 이때 HTTP 바디는 응답 데이터에 없음. 상태 코드는 변경된 것이 없다는 304 Not Modified. 전송 데이터에 바디가 빠졌기 때문에 헤더만 포함된 0.1M만 전송된다.

③ 브라우저 캐시에서 응답 결과 재사용, 헤더 메타데이터 갱신

④ 브라우저는 캐시에서 조회한 데이터 렌더링

⇒ 클라이언트에서는 해당 응답을 받은 후 캐시를 갱신해주고 다시 일정 시간 동안 유효하게 된다.

⇒ 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드하여 매우 실용적인 해결책이다.

![](https://blog.kakaocdn.net/dn/qw4z2/btrwJ8G2QMv/NfpT6AoNLnr4LHaJkgRhTK/img.png)

‣ 캐시 유효 시간이 초과되더라도 If-Modified-Since 헤더를 이용하여 조건부 요청을 할 수 있다.

‣ Last-Modified와 If-Modified-Since의 단점

→ 1초 미만(0.x초) 단위로 캐시 조정 불가능

→ 날짜 기반의 로직 사용

→ 데이터를 수정하여 날짜가 다르지만 같은 데이터를 수정해서 데이터 결과가 똑같은 경우

→ 서버에서 별도의 캐시 로직을 관리하고 싶은 경우

ex) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

‣ ETag(Entity Tag)

![](https://blog.kakaocdn.net/dn/wSwqj/btrwWhpnGuM/sE0rDNMQuxorxQ8mICYDc0/img.png)

캐시용 데이터에 임의의 고유한 버전 이름을 달아두고 데이터가 변경되면 이 이름을 바꾸어 변경(Hash 재생성).

→ 단순히 ETag만 보내서 같으면 유지하고 다르면 다시 받는 방식.

→ 서버에서 완전히 캐시를 컨트롤하고 싶은 경우 사용한다.

⇒ 캐시 제어 로직을 서버에서 완전히 관리하고 클라이언트는 단순히 이 값을 서버에 제공한다(즉, 클라이언트는 캐시 메커니즘을 모른다)

![](https://blog.kakaocdn.net/dn/bavyXD/btrwZZPgoHT/bP2gGp1ISzbXanH1ygaqr0/img.png)

→ 서버에서 헤더에 ETag를 작성하여 응답하고, 클라이언트의 캐시에서 해당 ETag값을 저장한다.

![](https://blog.kakaocdn.net/dn/cSOUZ3/btrwWgRyG8o/Nmbqa2lwaWISYFpe5ZwsK1/img.png)

→ 캐시 유효시간이 초과되어 다시 요청해야 하는 경우 ETag값을 검증하는 If-None-Match를 요청 헤더에 작성하여 조건부 요청을 할 수 있다.

![](https://blog.kakaocdn.net/dn/44B1g/btrwTOuH4EK/kULknIXV3dbSXnpnkizh50/img.png)

① 데이터가 수정되었는지 ETag를 이용하여 검증

② 수정되지 않았다면 바디를 제외한 HTTP 헤더만 전송

→ 서버에서 데이터가 변경되지 않았을 경우 ETag는 동일하기 때문에 If-None-Match는 거짓이 된다.

→ 서버에서 304 Not Modified를 응답, HTTP 바디는 없음.

③ 브라우저 캐시에서 응답 결과 재사용, 헤더 메타데이터 갱신

④ 브라우저는 캐시에서 조회한 데이터 렌더링

‣ Cache-Control

• Cache-Control: max-age

→ 캐시 유효 시간. 초 단위

• Cache-Control: no-cache

→ 데이터는 캐시 해도 되지만 항상 Origin 서버에 검증하고 사용

• Cache-Control: no-store

→ 데이터에 민감한 정보가 있으므로 저장하면 안 됨(메모리에서 사용하고 최대한 빨리 삭제)

‣ Expires(캐시 만료일 지정 / 하위 호환)

• Expires: Wed, 30 Mar 2022 00:00:00 GMT

→ 캐시 만료일을 정확한 날짜로 지정하고, HTTP 1.0부터 사용

→ 지금은 더 유연한 Cache-Control: max-age 권장

→ Cache-Control: max-age와 함께 사용되면 Expires는 무시됨

### ③ 프록시 캐시(proxy cache)

‣ 프록시와 프록시 서버

→ 클라이언트와 서버 사이에 대리로 통신을 수행하는 것. 그 중계 기능을 하는 서버

→ 클라이언트 혹은 서버가 다른 네트워크에 간접 접속할 수 있기 때문에 보안, 캐싱을 통한 성능, 트래픽 분산 등의 장점을 가진다.

![](https://blog.kakaocdn.net/dn/bMN3i6/btrw2NA3joN/elLXpavJm3hElxlKU1Wvx0/img.png)

→ 클라이언트에서 사용하고 저장하는 캐시를 private 캐시, 프록시 캐시 서버의 캐시를 public 캐시 라고 한다.

‣ Cache-Control(프록시 캐시와 관련된 헤더)

• Cache-Control: public → 응답이 public 캐시에 저장되어도 됨

• Cache-Control: private → 응답이 해당 사용자만을 위한 것. private 캐시에 저장해야 함(기본값)

• Cache-Control: s-maxage → 프록시 캐시에만 적용되는 max-age

• Age: 60 → Origin 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)

‣ 캐시 무효화: 클라이언트가 캐시를 적용하지 않아도 임의로 브라우저가 캐시를 적용하는 경우, 특정 페이지에서 캐시가 되면 안 되는 정보(통장 잔고 등)가 있다면 무효화할 수 있는 헤더

‣ Cache-Control: no-cache → 데이터는 캐시 해도 되지만 항상 Origin 서버에 검증하고 사용(이름에 주의)

‣ Cache-Control: no-store → 데이터에 민감한 정보가 있으므로 저장하면 안 됨(메모리에서 사용하고 최대한 빨리 삭제)

‣ Cache-Control: must-revalidate

→ 캐시 만료 후 최초 조회 시 Origin 서버에 검증해야 함

→ Origin 서버 접근 실패 시 반드시 오류가 발생해야 함 - 504(Gateway Timeout)

→ must-revalidate는 캐시 유효 시간이라면 캐시를 사용함

‣ Pragma: no-cache → HTTP 1.0 하위 호환 ⇒ 캐시 무효화를 확실하게 해야 하는 경우 Pragma와 같은 하위 호환까지 적용해야 한다.

```
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
```

‣ no-cache와 must-revalidate의 다른 점

① no-cache

![](https://blog.kakaocdn.net/dn/cKKFml/btrwWg5fqEB/uU9bEPpV6MCefJE6hyV4Hk/img.png)

(no-cache 기본 동작)

캐시 서버 요청을 하고 프록시 캐시 서버에 도착하면 no-cache의 경우 원 서버에 요청을 하게 되고, 원 서버에서 검증 후 304 Not Modified 응답을 하게 된다.

![](https://blog.kakaocdn.net/dn/wZKro/btrw2Omy5lU/otqHT8QbPU1akdNB8Xu380/img.png)

만약 프록시 캐시 서버와 원 서버 간의 네트워크 연결이 단절되어 접근이 불가능한 경우, no-cache에서는 응답으로 오류가 아닌 오래된 데이터라도 보여주자는 개념으로 200 OK 응답을 한다.

② must-revalidate

![](https://blog.kakaocdn.net/dn/bDpc9r/btrAdGMYur1/Umu0UxRs3BjmonMu0XsrX0/img.png)

no-cache와 다르게 must-revalidate는 원 서버에 접근이 불가할 때 504 Gateway Timeout 오류를 보낸다. 중요한 정보(통장 잔고 등)가 원 서버를 받지 못해도 예전 데이터로 뜨면 안 되기 때문에 must-revalidate를 쓴다.

✷ CDN(Content Delivery Network): 콘텐츠를 좀 더 빠르고 효율적으로 제공하기 위해 등장한 서비스

→ 원본을 복사하여 저장할 여러 개의 캐시 서버로 구성

→ 콘텐츠를 요청받은 경우 데이터를 전달하기 가장 유리한 캐시 서버에서 관련 콘텐츠 제공 ⇒ 제공할 콘텐츠를 가지고 있으며 위치상으로 가장 가까운 캐시 서버가 우선순위를 가짐.

‣ 정적 콘텐츠(Static Contents): 내용이 거의 변하지 않는 콘텐츠

→ HTML 파일, 동영상 같이 변화가 거의 없는 콘텐츠, 뉴스 기사 등 개인화되지 않은 대중적인 콘텐츠 ⇒ CDN의 캐시 서버에 저장하기 적합함

‣ 동적 콘텐츠(Dynamic Contents): 위치, IP 주소 등 사용자가 접근할 때마다 내용이 바뀌거나 사용자마다 다른 내용을 보여주는 콘텐츠

→ 위치, IP 주소, 사용시간 관련 콘텐츠. 카드번호, 전화번호 등 개인화된 정보 관련 콘텐츠

→ 콘텐츠가 바뀔 때마다 캐시 서버에 바뀐 콘텐츠가 전파되어야 하기 때문에 공통적인 HTML 파일 부분을 캐시 서버에 저장한다. ⇒ CDN 네트워크가 지원하기 어려움

‣ CDN의 이점

• 디도스(DDoS / Distributed Denial of Service attack)공격에 대해 어느 정도 대응 가능 → 서버의 수용량보다 훨씬 많은 요청을 보내 서버를 사용 불가능하게 만드는 디도스 공격에도 CDN의 데이터 센터는 하나의 데이터 센터를 사용하지 못하더라도 다른 데이터 센터에서 콘텐츠를 제공받을 수 있다.

→ 데이터 센터들은 거대한 컴퓨팅 능력을 갖고 있어 서비스 장애가 발생하기 어렵다.

• 로딩 속도 감소로 인한 사용자 경험 향상

• 트래픽 분산으로 인한 트래픽 관련 비용 절감 → 모든 요청을 하나의 서버에서 담당한다면 고성능의 서버 및 인터넷 수용력이 필요하게 되어 비용이 많이 들고 소모되는 전력이 많아진다.

⇒ 서버들을 분산시키면 지역에 맞게 서버와 인터넷의 성능을 낮추어도 서비스 제공 가능, 외국에 있는 사용자들의 로딩 시간을 단축시켜 사용자 경험 향상 및 비용 절감의 효과를 볼 수 있다.

‣ 네트워크 구성 방법 → 필요에 따라 선택하여 사용하는 방식이 다르다

• Scattered 방식: 최대한 낮은 응답 시간에 집중(최대한 빠른 응답속도가 목표)

→ 세계 곳곳에 최대한 많은 캐시 서버 제공

→ 낮은 수용량의 데이터 센터 및 캐시 서버

→ 매우 높은 관리비용, 클라우드 제공자는 관리비용을 사용자에게 전가하기 때문에 높은 사용자 요금

→ 연결 수요가 적은 지역 대상으로 적절한 방식

• Consolidated 방식: 여러 서버(데이터 센터)들을 통합하여 운용하는 방식

→ 다수의 고성능 서버로 통합하여 운용하는 방식

→ 응답 시간이 증가하지만 데이터 센터의 수가 줄어듦으로 인해 관리 및 유지비용이 낮아짐

→ 유지관리비용이 적어져 사용자들에게 전가되는 요금이 줄어들어 사용자들의 부담이 줄어듦.

→ 연결 수요가 많은 지역 대상으로 적절한 방식

![](https://blog.kakaocdn.net/dn/bDNZ8I/btrwWnbMQGo/NNGHknBdkk8FOuJp5AfkIk/img.png)

과거에는 응답속도에 중점을 두어 Scattered 방식, 정적 콘텐츠 CDN이 주류여서 응답 속도는 매우 높았지만 사용자에게 전가되는 비용이 매우 높았다.

현재는 동적 콘텐츠를 지원하고 데이터 센터를 통합하기 시작하여 관리하는 데이터 센터의 수가 줄어 사용자에게 전가되는 비용이 줄어들고 있다.

디도스 공격 등 사이버 공격에 대응하고 어느 상황에서도 콘텐츠를 제공할 수 있도록 보안과 안정성에 집중하고 있다.
