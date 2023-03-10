---
layout: single
title: "D+40(41, 42) Web Server 기초, Express, Middleware"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

웹 서버 기초와 express.

## 1. COSR

[Cross-Origin Resource Sharing](https://hannut91.github.io/blogs/infra/cors)

브라우저에서는 보안적인 이유로 cross-origin HTTP 요청들을 기본적으로는 제한하지만,(요청을 열어 놓으면 서버에 어떤 리소스를 생성할지 확인할 수 없기 때문에 보안적인 이유가 있음) 웹 애플리케이션 고도화를 위해 개선을 요청한다.

⇒ 서버가 허용(allow)한 범위 내에서의 cross origin 요청을 허용한다.

cross-origin 요청을 하려면 서버의 동의가 필요, 동의한다면 브라우저에서 요청 허락, 비동의 시 브라우저에서 거절. 이러한 허락을 구하고 거절하는 메커니즘을 HTTP-header를 이용해서 가능한데 이를 CORS라고 부른다.

⇒ 브라우저에서 cross-origin 요청을 안전하게 할 수 있도록 하는 메커니즘.

⇒ cross origin에서 다른 서버에 있는 리소스(서버 자원)를 요청하여 사용하기 위해 필요함.

✷ cross-origin

다음 중 한 가지라도 다른 경우를 말한다.

‣ 프로토콜 - http와 https는 프로토콜이 다르다.

‣ 도메인 - domain.com과 other-domain.com은 다르다.

‣ 포트 번호 → 8080 포트와 3000 포트는 다르다.

ex)

```js
const defaultCorsHeaders = {
  // 어떤 origin을 접근할 수 있게 허용할 것인가
  // 모든 도메인(*, 와일드카드)을 허용한다
  'access-control-allow-origin': '*',

  // 이 메소드들만 허용한다
  'access-control-allow-method': 'GET, POST, PUT, DELETE, OPTIONS',

  // 헤더에는 content-type과 accept만 쓸 수 있다
  'access-control-allow-headers': 'content-type', 'accept',

  // preflight request는 10초까지 허용된다
  'access-control-max-age': 10
};
```

✷ SOP(Same Origin Policy): (AJAX 요청 시) 같은 오리진끼리만 리소스가 공유된다.

### 1-1. OPTIONS

[OPTIONS](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/OPTIONS)

![](https://blog.kakaocdn.net/dn/AgO7Z/btrpdoCsPk1/6NMsF20L6PhwcLbL1OScdK/img.png)

→ 어떤 서버가 특정 오리진(abcd.com)에만 cross origin 요청을 허용해주었다고 한다면 이 오리진은 OPTIONS라는 preflight request를 통해 서버에 request 정보를 확인하고, 그 다음에는 브라우저가 자동으로 OPTIONS라는 요청을 서버로 보내 cross origin 요청에 대한 허가를 받은 다음 POST 요청을 보내주는 방식으로 cross origin을 요청한다.

⇒ OPTIONS는 CORS 설정을 위해 넣어야 하는 것이라고 이해해도 괜찮다.

✷ preflight request: CORS 허용했는지 미리 확인하려고 보내는 요청(예비 요청)

## 2. HTTP 트랜잭션 해부

[HTTP 트랜잭션 해부](https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction/)

Node.js HTTP 처리 과정을 잘 이해하는 것.

```js
const http = require("http");
const PORT = 4999;
const ip = "localhost";

const server = http.createServer((request, response) => {
  if (request.method === "OPTIONS") {
    // do something
  }
  if (request.method === "POST") {
    let body = [];
    request
      .on("data", (chunk) => {
        body.push(chunk);
      })
      .on("end", () => {
        body = Buffer.concat(body).toString();
        response.writeHead(200, defaultCorsHeader);
        if (reponse.url === "/upper") {
          // do something
        } else if (response.url === "/lower") {
          // do something
        } else {
          // do something
        }
      });
  }
});

app.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});

// 응답 헤더
// 서버가 클라이언트에게 보내주는 예비응답 세팅의 역할을 한다
const defaultCorsHeader = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type, Accept",
  "Access-Control-Max-Age": 10,
};
```

‣ 에코 서버: 요청과 응답이 같음.

ex)

```js
req;
("hello");

res;
("hello");
```

‣ stream과 Buffer

![](https://blog.kakaocdn.net/dn/bkYsBr/btrpeIvvYpL/e5vsNttoKkjKGiWA7JdqK1/img.png)

⇒ 대역폭이 좁아지면 버퍼링이 생긴다.

✷ [<font color="purple">웹 서버와 앱 서버의 차이</font>](https://chrisjune-13837.medium.com/web-%EC%9B%B9%EC%84%9C%EB%B2%84-%EC%95%B1%EC%84%9C%EB%B2%84-was-app%EC%9D%B4%EB%9E%80-692909a0d363)

✷ nodemon 설치 명령어

```
npm install nodemon --save-dev
```

## 3. How to debug node app

[참고링크](https://nodejs.org/en/docs/guides/debugging-getting-started/)

①

```
node(mon) --inspect server/basic-server.js
node(mon) --inspect-brk server/basic-server.js ⇒ 파일 실행 전 break
(basic-server.js는 진행한 스프린트의 서버 파일 이름)
```

② vs code에서 debugging 하기

왼쪽 사이드바에 보면 실행 및 디버거하기 아이콘이 있는데, 내가 원하는 곳에 break point(빨간 점)을 찍어놓고 디버깅 돌리기.

## 4. Refactor Express

① [Node.js Express](https://expressjs.com/en/resources/middleware/cors.html)

Express framework는 npm을 통해 다운로드할 수 있다.

```
npm install cors --save
npm install express --save
```

✷ Express로 구현한 서버가 http 모듈로 작성한 서버와 다른 점

‣ 미들웨어 추가가 편리하다.

‣ [자체 라우터](https://expressjs.com/en/guide/routing.html)를 제공한다.

② [라우팅(Routing)](https://expressjs.com/en/guide/routing.html)

메소드와 URL(/lower, /upper 등)로 분기점을 만드는 것.

→ 클라이언트는 특정한 HTTP 요청 메소드(GET, POST 등)나 서버의 특정 URI(또는 경로)로 HTTP 요청을 보낸다. 라우팅은 클라이언트의 요청에 해당하는 메소드와 Endpoint에 따라 서버가 응답하는 방법을 결정하는 것이다.

ex) 추가 라이브러리를 사용하지 않은 순수 node.js 코드로 라우팅을 구현한 예시

```js
// request를 req, response를 res라고 써도 상관 없음

const requestHandler = (request, response) => {
  if (request.url === "/lower") {
    if (request.method === "GET") {
      request.end(data);
    } else if (request.method === "POST") {
      request.on("data", (request, response) => {
        // do something ...
      });
    }
  }
};
```

ex) Express 라우터를 활용하여 구현한 코드

```js
const router = express.Router();

router.get("/lower", (request, response) => {
  response.send(data);
});

router.post("/lower", (request, response) => {
  // do something
});
```

③ Middleware: 프로세스 중간에 관여하여 특정 역할을 수행함.

![](https://blog.kakaocdn.net/dn/XejEh/btrpjzwSzar/KAy9FTvEWxt6TkX4Hr2f30/img.jpg)

express의 가장 큰 장점인 미들웨어는 request에 필요한 기능을 더하거나, 에러를 밖으로 걷어내는 역할을 한다.

미들웨어를 이용하면 node.js만으로 구현한 서버에서는 다소 번거로울 수 있는 작업을 보다 쉽게 적용할 수 있다.

✷ 미들웨어를 사용하는 상황

‣ POST 요청 등에 포함된 body(payload)를 구조화할 때(쉽게 얻어내고자 할 때) → 순수 node.js로 HTTP body(payload)를 받을 때에는 Buffer를 조합해서 다소 복잡한 방식으로 body를 얻을 수 있다.

ex) 네트워크 상의 chunk를 합치고 buffer를 body로 변환하는 작업이 필요함.

```js
let body = [];
request
  .on("data", (chunk) => {
    body.push(chunk);
  })
  .on("end", () => {
    body = Buffer.concat(body).toString();
    // body 변수에는 문자열 형태로 payload가 담겨져 있다.
  });
```

body-parser 미들웨어를 사용하면 간단하게 과정을 처리할 수 있다. 여기서 다룰 수 있는 body 형식은 json, text(기본 텍스트), buffer 등이 있다.

ex) body-parser로 요청받은 데이터를 json 형태로 변환하기

```js
const jsonParser = express.json();

// 생략
app.post("/api/users", jsonParser, function (req, res) {
  // req.body에는 JSON의 형태로 payload가 담겨져 있습니다.
});
```

**<mark>✷ 최신 버전에는 express안에 body-parser의 역할을 할 수 있게 업데이트되었기 때문에 사용할 필요는 없어졌으나 그래도 알고는 있어야 함.</mark>**

‣ 모든 요청 / 응답에 CORS 헤더를 붙여야 할 때

순수 node.js 코드에 CORS 헤더를 붙이려면, 응답 객체의 writeHead 메소드 등을 이용한다.

이런 메소드를 이용하더라도 Access-Control-Allow-\* 헤더를 매번 재정의해야 하고, OPTIONS 메소드에 대한 라우팅도 따로 구현해야 한다.

ex) 순수 node.js에 CORS를 적용하는 예시

```js
const defaultCorsHeader = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type, Accept",
  "Access-Control-Max-Age": 10,
};

// 생략
if (req.method === "OPTIONS") {
  res.writeHead(200, defaultCorsHeader);
  response.end();
}
```

이것을 [<font color="blue">cors 미들웨어</font>](https://github.com/expressjs/cors)로 사용하면 간단하게 처리할 수 있다.

```js
const cors = require("cors");

// 생략
app.use(cors()); // 모든 요청에 대해 CORS 허용
```

ex) 특정 요청에만 cors 모듈 적용하기

```js
const cors = require("cors");

// 생략
// 특정 요청에 대해 CORS 허용
app.get("/products/:id", cors(), function (request, response, next) {
  response.json({ msg: "This is CORS-enabled for a Single Route" });
});
```

[<font color="blue">✷ express.json()-공식문서</font>](http://expressjs.com/ko/api.html#express.json)

[<font color="red">✷ express.json() -쉽게 설명된 블로그</font>](https://blog.naver.com/PostView.nhn?blogId=dlaxodud2388&logNo=221708863522)

[<font color="blue">✷ express.static()-공식문서</font>](http://expressjs.com/ko/api.html#express.static)

[<font color="red">✷ express.static() -쉽게 설명된 블로그</font>](https://backback.tistory.com/338)

[‣ 모든 요청에 대해 url이나 메소드를 확인할 때](https://expressjs.com/ko/guide/writing-middleware.html)

로거(logger): 미들웨어 중 하나, 디버깅이나 서버 관리에 도움이 되기 위해 console.log로 적절한 데이터 / 정보를 출력한다.

데이터가 여러 미들웨어를 거치는 동안 응답할 결과를 만들어야 한다면 미들웨어 사이사이에 로거를 삽입하여 현재 데이터를 확인하거나 디버깅에 사용할 수 있다.

![](https://blog.kakaocdn.net/dn/TSWyI/btrpfgdvm3O/9gQo3UswkVrYeKKHl93Ulk/img.png)

(공식문서에서 확인할 수 있는 미들웨어의 구성)

endpoint가 /이면서, 클라이언트로부터 GET 요청을 받았을 때 적용되는 미들웨어다(파라미터 순서에 유의).

req, res는 우리가 잘 아는 요청(request)/응답(response)이고, next는 다음 미들웨어를 실행한다.

최상단에 나오는 이미지에서 next의 역할을 확인할 수 있다. 미들웨어 내부에서는 아무런 작업을 하고 있지 않고, next() 함수를 호출하여 다음 미들웨어로 데이터를 전달하고 있다.

만약 특정 enpoint가 아니라 모든 요청에 동일한 미들웨어를 적용하려면 메소드 app.use를 사용한다.

ex) 모든 요청에 대해 LOGGED가 출력되는 예시

```js
const express = require("express");
const app = express();

const myLogger = function (req, res, next) {
  // 이 부분을 req, res 객체를 이용해 고치면 모든 요청에 대한 로그를 찍을 수 있다.
  console.log("LOGGED");
  next();
};

app.use(myLogger);

app.get("/", function (req, res) {
  res.send("Hello World!");
});

app.listen(3000);
```

‣ 요청 헤더에 사용자 인증 정보(토큰, token)가 담겨있는지 확인할 때

✷ 토큰(Token): 주로 사용자 인증에 사용함.

ex) HTTP 요청에서 토큰이 있는지 여부를 판단하고, 이미 로그인한 사용자일 경우 성공, 아닐 경우 에러를 보내는 미들웨어 예제

```js
app.use((req, res, next) => {
  // 만약 토큰이 있다면 로그인에 성공함
  if (req.headers.token) {
    req.isLoggedIn = true;
    next();

    // 만약 토큰이 없다면 bad request와 함께 invalid user 메시지를 전송함
  } else {
    res.status(400).send("invalid user");
  }
});
```

서버에서는 요청에 포함된 데이터를 통해 미들웨어가 요구하는 조건에 맞지 않으면, 불량품으로 판단하고 돌려보내도록 구현할 수 있다.

‣ Morgan(format, options): 로그를 찍는 모듈.

client에서 요청한 메소들나 상태코드 같은 것들이 로그로 찍힌다. 로그를 어떠한 방식으로 찍힐 것인지에 대한 옵션을 파라미터로 넣을 수 있다.

→ format은 문자열이나 콜백함수를 넣어야 한다.

직접 원하는 정보만을 넣어 커스텀할 때는 콜백함수를 넣어 토큰 값을 원하는 것들로 수정하면 되지만 그냥 로그를 찍기 위한 용도이면 문자열을 넣어 적용시키면 된다. 넣을 수 있는 문자열의 종류는 다양하게 있다.

→ option은 객체 형식에 값을 넣어 적용해야 한다. 안에 넣는 값은 대표적으로 스킵이 있다.

[<font color="blue">morgan 공식 문서</font>](https://www.npmjs.com/package/morgan)

[<font color="red">morgan 블로그 설명</font>](https://burkui-developer.tistory.com/2)

## 4. Node.js Architecture & 5. How Node.js Works

{% include video id="XUSHH0E-7zk" provider="youtube" %}
{% include video id="jOupHNvDIq8" provider="youtube" %}

[Node.js가 무엇이며 이것으로 무엇을 할 수 있는가?작동방식 등등](https://velog.io/@onikss793/Node.js...)

✷ <mark>Node는 Javascript 코드를 실행하기 위한 런타임 환경.</mark>

⇒ 자바스크립트 코드를 브라우저 밖에서 실행시키도록 해준다. 이전까지는 브라우저에 종속되어 있었던 자바스크립트가 node.js 환경을 만나면서 서버-사이드에서도 자바스크립트를 활용할 수 있게 되었다.

## 6. 쿼리 스트링? 파람?(What is query string & params)

[<font color="red">query string & params</font>](https://velog.io/@pear/Query-String-%EC%BF%BC%EB%A6%AC%EC%8A%A4%ED%8A%B8%EB%A7%81%EC%9D%B4%EB%9E%80)

[<font color="blue">req.query, req.params, req.body</font>](https://wooooooak.github.io/web/2018/11/10/req.params-vs-req.query/)
