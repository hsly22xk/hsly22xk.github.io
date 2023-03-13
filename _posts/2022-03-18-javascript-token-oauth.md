---
layout: single
title: "D+61(62) Token, OAuth"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

token과 oauth.

## 1. 토큰(Token)

[토큰](https://victorydntmd.tistory.com/116)

유저 정보를 암호화한 상태로 담을 수 있고, 암호화했기 때문에 클라이언트에 담을 수 있다.

![](https://blog.kakaocdn.net/dn/cDFPfq/btrwbr1G64E/KiMH7CT0nPIuB6k00QCHG1/img.png)

![](https://blog.kakaocdn.net/dn/qJM7R/btrzQn8EHwP/mYG8jKKdwUQ5We0z04qDC0/img.png)

### ① 토큰 기반 인증(Token-based Authentication)

기존의 세션 기반 인증은 서버(혹은 DB)에 유저 정보를 담는 방식이었고, 항상 요청이 들어올 때마다 DB를 살펴보아야 하는 부담을 클라이언트에게 넘겨줄 수 없을까?에서 고안되었다. → 클라이언트에서 인증 정보를 보관하는 방법으로 고안되었다. 클라이언트가 토큰을 가지고 있으면 서버에게 토큰을 보여주고, 다양한 기능들을 요청할 수 있다.

### ② JWT(JSON Web Token)

[jwt](https://jwt.io/)

대표적인 토큰 기반 인증. JSON 포맷으로 사용자에 대한 속성을 저장하는 웹 토큰. 어떤 종류의 토큰인지, 어떤 알고리즘으로 암호화하는지 적혀있으며 JSON 형태로 나타난다.

```js
{"alg":"HS256", "typ":"JWT"}
```

‣ Payload: 정보들이 담겨있음. 어떠한 정보에 대해 접근할 수 있는 권한을 담을 수 있고, 기타 필요한 데이터들은 페이로드에 담아 암호화 시킴. (암호화시킨다 하더라도 민감한 정보는 되도록 담지 않는 것이 중요함)

```js
{"sub":"someInformation",
"name":"phillip",
"iat":151623391}
```

‣ Signature: Header, Payload를 base64로 인코딩 된 값과 salt값의 조합으로 암호화된 값.

base64 인코딩을 한 값은 누구나 쉽게 디코딩 할 수 있지만, 서버에서 사용하고 있는 비밀 키를 가지고 있지 않다면 해독하는 데에 많은 시간과 노력이 들어간다.

```
HMACSHA256(
  base64URLEncode(header)+"."+
  base64Encode(payload),
secret)
```

```
table ID를 준다.

그 정보를 JSON 형태로 전달(객체)

유효기간도 전달
{ "id": 1,
"exp": 2019_12_19
}

http headers(주요한 내용을 넣는)에서 이용할 수 있도록 JSON 을 'token'화 함.

'.'을 기준으로 3부분으로 나뉘어짐.

첫번째, 두번째는 코드화(encoding), 누구든 decode 할 수 있음

마지막은 암호화(복호화를 아무나 하지 못함, 웹코드를 서버한 페이지는 할 수 있음),
도용의 문제를 막기 위해 다른 서버는 복호화를 할 수 없음. => 인가가 안 됨

서버가 직접 발행한 웹토큰만 복호화할 수 있음

Authorization header 부분에 같이 첨부해서 보냄.
프론트에서 리퀘스트가 있으면 저장하고 있던 토큰을 백에 첨부해서 같이 보냄.
```

#### ✷ JWT의 종류

‣ Access Token: 보호된 정보들(유저의 이메일, 연락처, 사진 등)에 접근할 수 있는 권한부여에 사용한다.

→ 클라이언트가 처음 인증을 받게 될 때(로그인) access token과 refresh token 모두 받지만 실질적으로 사용하는 토큰은 access token이다.

→ 권한을 부여받는 데엔 access token만 있으면 되지만 악의적인 유저가 얻어냈을 경우를 대비하여 비교적 짧은 유효 기간을 두어 탈취되더라도 오랫동안 사용할 수 없는 것이 좋다.

‣ Refresh Token: access token이 만료되었을 때 refresh token을 이용하여 새로운 accss token을 발급받아 유저는 다시 로그인할 필요가 없다. → 유저의 편의보다 정보를 지키는 것이 더 중요한 웹사이트들은 refresh token을 사용하지 않는 곳이 많다.

⇒ 각 방법들의 장단점을 참고하며 필요에 맞게 사용하는 것이 좋다.

### ③ 토큰 기반 인증 절차

![](https://blog.kakaocdn.net/dn/cqoDQY/btrv6enY2vS/ojx0lG2NlrZXO66ivTG4Ik/img.png)

→ 클라이언트가 요청을 보내면 서버는 DB에 확인을 하고 jwt 토큰을 생성하여 그 토큰을 클라이언트에 보내고 클라이언트는 로컬 스토리지나 쿠키, 리액트의 상태(state) 등에 토큰을 저장한다.

→ 클라이언트가 jwt토큰을 담아서 서버에 어떠한 정보를 달라는 get요청을 하고 서버는 그 토큰을 해독하여 서버가 발급해준 토큰이 맞다는 판단이 내려지면 클라이언트의 요청을 처리를 하고 그에 따른 응답을 한다.

### ④ 토큰 기반 인증의 장점

‣ 무상태성 & 확장성(Statelessness & Scalability): 서버는 클라이언트에 대한 정보를 저장할 필요가 없어(토큰 해독이 되는지만 판단하면 됨), 서버와 DB의 부담을 덜어주게 된다.

클라이언트는 토큰을 헤더에 추가함으로 인증 절차가 완료된다. ⇒ 하나의 토큰으로 여러 서버에서 인증을 받을 수 있음.

⇒ 서버와 DB의 부담을 덜어주어 여러 개의 서버를 사용하는 서비스를 운영하고, 이렇게 여러 개의 서버를 사용하며 접접 커져가는 앱이라면(앱의 확장을 고려하고 있다면) 토큰 기반 인증을 고려해 봐야 한다.

‣ 안정성: 암호화 한 토큰을 사용하고 암호화 된 키를 노출할 필요가 없음.

‣ 어디서나 생성 가능: 토큰을 생성하는 서버가 꼭 토큰을 만들지 않아도 됨. → 토큰 생성용 서버를 만들거나 토큰 관련 작업을 맡길 수도 있는 등 다양한 활용이 가능하다.

‣ 권한 부여에 용이: 토큰의 내용물(payload) 안에 어떤 정보에 접근 가능한 지 정의할 수 있다.

ex) 사진과 연락처 사용권한 부여 / 사진 권한만 부여 / 연락처 권한만 부여

[jsonwebtoken 공식문서](https://www.npmjs.com/package/jsonwebtoken)

## 2. 인증(Authentication)과 인가(authorization)의 차이

누가, 언제, 어떻게 쓰고 있는가를 파악하기 위해 모든 사이트에는 인증과 인가가 있음.

### ① 인증

유저가 누구인지 확인하는 절차(회원가입 / 로그인)

```
Q. 어떻게 하면 정보를 첨부해 통신을 보낼 수 있을까?
민감한 정보는 아니면서 일정시간 동안 유효하게, 그리고 도용되지 않게.

opt1. 아이디와 비밀번호를 같이 보낸다.
⇒ 매번 서버에서 확인을 해야 함, 정보의 민감성

opt2. 시간제한이 있는 임시 아이디를 보낸다
⇒ 어떤 유저인지 파악하기 힘듦, 그 유저의 정보를 또 따로 저장을 해야 함.(실제 유저 정보와 맵핑을 따로 해야 함)

opt3. 일정 시간 동안 인가에 유효한 정보로 대체한다. ⇒ JWT(JSON Web Tokens) 이용

Q. 유저의 비밀번호 암호화는 어떻게 해야 할까?

→ 유저의 비밀번호는 절대 비밀번호 그대로 DB에 저장 하지 않음.
DB가 해킹을 당하면 유저의 비밀번호도 그대로 노출될 뿐더러 내부 개발자나 인력이 그 정보를 볼 수 있기 때문에 유저의 비밀번호는 꼭 암호화 해서 저장한다.

→ 비밀번호 암호에는 단방향 해쉬 함수(one-way hash function)가 일반적으로 쓰임.
단방향 암호화-복호화가 안 되는 암호, 원본의 문자를 알아낼 수가 없음

→ 외부에서 정보가 해킹당했을때, 내부에서 정보가 유출될 때를 모두 대비해 단방향 암호화로 만듦.

Q. 암호화된 문자의 원본을 어떻게 알 수 있을까?

→ 동일한 알고리즘을 이용하면 동일한 값이 나옴.
→ 복호화해서 확인할 수 없기 때문에 똑같은 알고리즘을 이용해 동일한 결과값이 나오면 같은 값인 것을 알 수 있음.

⇒ 암호화값이 다르면 원본값이 다른 것. 유저의 비밀번호 원본 문자는 서버에서 알 수가 없음.
→ 클라이언트가 암호화하는 것이 아니라 서버쪽에서 암호화 하는 것. 백에서 암호화를 맞춰봄.
```

‣ 단방향 암호화를 decoding 하는 방법

→ Bruceforce Attack: 같은 값이 나올 때까지 모든 암호값을 다 때려 맞춰보는 것. 조합 가능한 숫자와 문자, 특수기호 등을 다 조합해 봐야 하므로 시간이 오래 걸림.

→ Rainbow Attack: 미리 계산된 테이블을 갖고 조합해보는 것. 서칭을 해봄으로써 원본값을 찾을 수 있음.

✷ 'rainbow attack'이 가능한 이유: 해쉬 암호화는 연산화되는 시간이 짧음. 비밀번호를 암호화하기 위해 만든 알고리즘이 아니기 때문에 누구라도 쉽게 값을 찾아낼 수 있음.

‣ 기존의 단방향 해쉬에서 진화한 암호 알고리즘 'Bcrypt'

‣ Salting : 원본값에 '소금을 뿌리듯이' random값을 추가 하는 것.

‣ Key Chaining : 연산을 느리기 위해 해쉬 값이 구해지면 그 해쉬 값을 기반으로 또 해쉬를 하고 해쉬를 하고 n번 하는 것. 최종값을 저장. ⇒ rainbow attack이 어려워짐. ⇒ 단방향 해쉬 함수의 단점을 보완

### ② 인가

유저가 요청하는 request를 실행할 수 있는 권한이 있는 유저인가를 확인하는 절차.

→ jwt를 쓰면 인가가 수월함. 서버가 유저 정보를 갖고 있으므로 데이터에서 유저의 권한 정보도 읽어들이면 됨.

→ 'access token'을 통해 해당 유저 정보를 얻을 수 있으므로 해당 유저가 가지고 있는 권한(permission)도 확인 가능.

#### ‣ 인가(Authorization) 절차

```
Authentication 절차를 통해 access token을 생성한다.

access token에는 유저 정보를 확인할 수 있는 정보가 들어가 있어야 한다 (예를 들어 user id).

유저가 request를 보낼때 access token을 첨부해서 보낸다.

서버에서는 유저가 보낸 access token을 복호화 한다.

복호화된 데이터를 통해 user id를 얻는다.

user id를 사용해서 database에서 해당 유저의 권한(permission)을 확인하다.

유저가 충분한 권한을 가지고 있으면 해당 요청을 처리한다.

유저가 권한을 가지고 있지 않으면 Unauthorized Response(401) 혹은 다른 에러 코드를 보낸다.
```

## 🌟 스프린트 진행 과정 중 나왔던 에러 핸들링

① Timeout

```
Error: Timeout of 2000ms exceeded.
For async tests and hooks, ensure "done()" is called;
if returning a Promise, ensure it resolves.
```

로그인 기능을 구현하는 과정에서 테스트를 돌렸더니 타임아웃 에러가 떠서, 구글링을 해본 결과 테스트 파일에서의 시간을 길게 수정하는 방법이 있었다. 그렇게 해봤을 때도 해결이 되지 않았는데, 결국 해결했다.

해결할 수 있었던 방향은 테스트에서의 타임 지연이 아닌, jsonwebtoken을 require해오지 않고 바로 jwt 문법을 사용하여 타임아웃 에러가 뜬 것으로 생각한다.

② TypeError

```
TypeError: Cannot convert undefined or null to object
```

undefined나 null 타입을 object로 convert할 수 없다는 타입 에러가 떴다. 이 부분은 환경변수에 저장해둔 ACCESS_SECRET을 제대로 가져오지 않아 생긴 에러였다.

## 3. OAuth 2.0

① oauth: 인증을 중개해 주는 메커니즘. → 보안된 리소스에 액세스하기 위해 클라이언트에게 권한을 제공(authorization)하는 프로세스를 단순화하는 프로토콜.

⇒ 이미 사용자 정보를 가지고 있는 웹 서비스(GitHub, google, facebook 등의 소셜 로그인)에서 사용자의 인증을 대신해 주고 접근 권한에 대한 토큰을 발급한 후, 이를 이용해 내 서버에서 인증이 가능해진다.

ex) 페이스북으로 소셜 로그인을 해서 유저의 페이스북 프로필 이미지를 받아오고 싶은 경우

![](https://blog.kakaocdn.net/dn/d5RvpB/btrwfco4fW9/Xi48RvOTZIIQkxnZNl0o01/img.png)

→ 앱이 페이스북 서버에 액세스 토큰을 가져왔음을 요청하고, 페이스북 서버에서는 그것이 진짜 서버에서 발급한 토큰이 맞는지 확인한 후 인증이 되면 이미지를 전송한다.

![](https://blog.kakaocdn.net/dn/dhz6X2/btrzJ3aDz7e/D0RKMhJqg9k7CzhCGlRHK1/img.png)

✷ OAuth에서 꼭 알아야 할 용어

‣ Resource Owner: 액세스 중인 리소스의 유저. 김코딩의 구글 계정을 이용하여 App에 로그인할 경우, 이때 Resource owner은 김코딩이 된다.

‣ Client: Resource owner를 대신하여 보호된 리소스에 액세스하는 응용프로그램. 클라이언트는 서버, 데스크탑, 모바일 또는 기타 장치에서 호스팅 할 수 있다.

‣ Resource server: 유저의 리소스들을 가지고 있는 서버. client의 요청을 수락하고 응답할 수 있는 서버.

‣ Authorization server: Resource server가 액세스 토큰을 발급받는 서버. ⇒ 클라이언트 및 리소스 소유자를 성공적으로 인증한 후 액세스 토큰을 발급하는 서버를 말한다.

‣ Authorization grant: 클라이언트가 액세스 토큰을 얻을 때 사용하는 자격 증명의 유형.

✷ grant type: client application이 access token을 얻는 여러가지 방법들.

‣ authorization code grant type

![](https://blog.kakaocdn.net/dn/dycANM/btrwbq2WXna/KK8OLk1SmpjBSJiaTOCP3k/img.png)

![](https://blog.kakaocdn.net/dn/bx1C3Y/btrwgjVNqIW/da9NJgDW9ElS2rzzYDb981/img.png)

유저가 승인을 한 후에 인증 서버에서 액세스 토큰을 받아오기 위해 먼저 authorization code를 받아 액세스 토큰과 교환하는 방법

→ authorization code 절차를 거치는 이유는 보안성 강화 목적.

⇒ client에서 client-secret을 공유하고 액세스 토큰을 가져오는 것은 탈취 위험이 있기 때문에

client에서는 client ID를 이용해서 받아올 수 있는 authorization code를 먼저 받아오고 server에서 client secret을 포함하여 access token 요청을 진행한다.

‣ refresh token grant type

![](https://blog.kakaocdn.net/dn/cjjhMM/btrwiyqVcCu/HYEgJfSCFKJfNs6oFGsDiK/img.png)

일정 기간 유효시간이 지나 만료된 액세스 토큰을 편리하게 다시 받아오기 위해 사용하는 방법

→ access token보다 refresh token의 유효시간이 대체로 조금 더 길게 설정하기 때문에 가능한 방법.

→ 서버마다 refresh token에 대한 정책이 다르므로 refresh token을 사용하기 위해서는 사용하고자 하는 서버의 정책을 살펴보아야 한다.

‣ implicit grant type

‣ client credentials grant type

‣ resource owner credentials grant type

‣ Authorization code: access token을 발급받기 전에 필요한 code. client ID로 이 code를 받아온 후, client secret과 code를 이용해 Access token을 받아온다.

‣ Access token: 보호된 리소스에 액세스하는 데 사용되는 credentials. Authorization code와 client secret을 이용해 받아온 이 Access token은 문자열 타입으로 되어있다. 이것으로 resource server에 접근 할 수 있다.

‣ Scope: 액세스 토큰의 권한을 정의한다. 주어진 액세스 토큰을 사용하여 액세스할 수 있는 사용자 리소스의 범위를 제한한다.

|                      |                                                                                                       설명                                                                                                       | 접속 상태 저장은 어디에 하는 지 |                                 단점                                 |
| :------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------: | :------------------------------------------------------------------: |
|         쿠키         | 쿠키는 그저 http의 stateless한 것을 보완해주는 도구이다. 클라이언트 쿠키 그 자체는 인증이 아니다. 세션 접속 상태를 서버가 갖고 있다(stateful). 접속 상태와 권한 부여를 위해 세션 아이디(토큰)를 쿠키로 전송한다. |              서버               |     하나의 서버에서만 접속 상태를 가지기 때문에 분산에 불리하다.     |
| 토큰(jwt가 대표적임) |                                                       토큰 자체가 무결성(integrity)을 증명할 수 있다. 서버가 접속 상태를 갖고 있지 않아도 된다(stateless)                                                        |           클라이언트            | (쿠키, localStorage, in-memory) 모든 요청에 토큰을 실어 보내야 한다. |
|      OAuth 2.0       |                                                     제 3자로부터 인증을 대행하고 access token을 받는다. 인증을 대신할 뿐, 권한 관리는 토큰 방식과 유사하다.                                                      |           클라이언트            | (쿠키, localStorage, in-memory) 모든 요청에 토큰을 실어 보내야 한다. |

## 4. oauth app을 통해 access token을 받아오는 과정

![](https://blog.kakaocdn.net/dn/qe9wy/btrwixS5pSq/jPFoIdik90XRsNqcdgTVq0/img.png)

![](https://blog.kakaocdn.net/dn/cgpBPy/btrwMGqce0w/MadBxnmienzK0v04K0uGWk/img.png)

![](https://blog.kakaocdn.net/dn/pN0nx/btrxkLXlHzR/NPMbYv3TDOB6g5Rv3TV2iK/img.png)

‣ github oauth app 생성 과정

```
https://github.com/settings/developers

- New Oauth App
- 생성
- Client ID, Client Secret 필요함
```
