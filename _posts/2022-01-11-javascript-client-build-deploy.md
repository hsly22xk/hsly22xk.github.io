---
layout: single
title: "D+49 클라이언트 빌드와 배포"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

## 1. SSR / CSR

[참고링크](https://hsly22xk.github.io/javascript/javascript-http-rest-api/)

![](https://blog.kakaocdn.net/dn/5QGhq/btrt0MFr60i/3iOGgEKEabYLhsJnKVsK5K/img.png)

ex)

```js
// server

var express = require("express");
var app = express();

const username = db.findOne({ where: { id: 1 } });

app.get("/", function (req, res) {
  res.status(200).send(username);
});
```

```js
// client

function Userinfo(prop) {
  const [username, setUsername] = useState("");

  function getUsername() {
    axios
      .get("http://localhost:4000")
      .then((data) => {
        return data.json();
      })
      .then((json) => {
        setUsername(json.username);
      });
  }

  return (
    <div>
      <span class="username">{username}</span>
    </div>
  );
}
```

## 2. 정적 / 동적 웹사이트

![](https://blog.kakaocdn.net/dn/bHI84H/btrtVpygU43/cCBN8BKXJyd81WzUczKqgk/img.png)

① 정적 웹사이트(static website): HTML 파일(코드) 자체로 배포되는 사이트(CSR, Client Side Rendering)

→ 자바스크립트가 동적인 렌더링을 지원하지만, 결국 서버가 웹 페이지를 렌더링하지 않는다.

→ HTML/CSS/JS 파일의 소스 코드 그대로 작동한다.

→ 현대의 2-tier Architecture에서는 정적 웹사이트의 사용이 더욱 보편적임.

⇒ 서버는 미리 만들어진 HTML, JS 파일을 전달하기만 한다. 즉, 서버 자원과 무관하다.

② 동적 웹사이트(dynamic website): 서버에 의해 HTML 파일이 동적으로 생성되는 사이트(SSR, Server Side Rendering) ⇒ 서버는 늘 HTM파일을 만들어서 응답해주어야 한다. 즉, 서버 자원에 따라 페이지의 형태가 바뀐다.

→ 서버가 HTML의 형태로 브라우저에 제공해 주어야만 했기 때문에 헤더나 푸터 등의 페이지 구성요소의 중복 요청 / 응답이 빈번해 네트워크 상에서 주고받는 패킷의 크기가 컸다.

```js
// 동적 웹페이지 예제 (node.js)
const http = require("http");

const server = http.createServer((req, res) => {
  // HTML 문서의 형태로 전달됨
  res.setHeader("Content-Type", "text/html");

  // 서버에 의해서 동적으로 바뀜
  res.end("<h1>동적 웹페이지</h1><p>with 랜덤한 값</p>" + Math.random());
});

server.listen(3000);
```

⇒ 클라이언트 사이드가 고도화된 것은 사실이지만 SSR의 장점을 살리기 위한 다양한 방법의 동적 웹사이트가 만들어지기도 하며, 성능 향상 극대화를 위한 CSR, SSR의 하이브리드 형태로 구성하는 경우도 많다.

## 3. 빌드

소스 코드를 실행 가능한 결과물로 변환하는 작업.

① 정적 웹사이트의 빌드

⇒ 현대의 웹 앱은 정적 웹페이지와 AJAX 기술을 함께 사용하며, SPA(Single Page Application)으로 변모함에 따라 클라이언트 사이드의 규모가 커지게 되었고, 이때 웹사이트 구성요소를 각 파일로 분리하는 모듈화가 이뤄지게 되며, React와 같은 클라이언트 기술이 발전하면서 단일 파일로 자바스크립트 / 페이지를 만드는 작업은 고도화되었다.

![](https://blog.kakaocdn.net/dn/cTkOz5/btrqkTuUWrX/G4KkOeYzspTaI2REwc3Avk/img.png)

(수많은 모듈을 하나의 정적 파일로 만들어내는 번들링 과정 (webpack))

‣ 번들링(bundling): 고도화된 클라이언트 웹 앱들의 수많은 모듈들을 하나로 묶어주는 작업.

![](https://blog.kakaocdn.net/dn/pcT98/btrp8rGMCza/CGkZTT3Xjnr9TJWTtBjSzK/img.png)

(하나의 파일로 합쳐진 수많은 모듈의 시각화)

‣ 소프트웨어 빌드: 소스코드를 실행 가능한 결과물로 변환하는 작업.

→ JSX 파일과 같이 브라우저에서 자체적으로 해석 불가능한 다양한 보조 기술들을 브라우저가 해석할 수 있도록 만들어주는 작업들이 수반되는 과정을 통칭하는 말.

⇒ 다양한 모듈은 정적 파일들로 결과가 만들어져야만 하며, 이러한 빌드 과정은 배포에 필수적이다.

ex) React 프로젝트를 내 로컬 컴퓨터에서 자체적으로 실행하기 위해 npm start로 개발 서버를 실행해 줘야 하지만, 넷상에 배포하기 위해서는 개발 서버를 실행할 필요 없고 정적 파일을 호스팅 하는 서비스에 결과물만 업로드한다.

Create React App 등으로 생성한 React 프로젝트의 경우 npm build 명령어가 package.json 파일에 포함되어 있고, 이는 모듈을 정적인 파일로 만들어주게 된다.

## 4. React 프로젝트 생성 툴

React 생태계에는 다양한 프로젝트를 생성 툴이 존재하는데, 이러한 프로젝트 생성 툴의 대표적인 예는 Create React App, [<font color="blue">Next.js</font>](https://kyounghwan01.github.io/blog/React/next/basic/#next-js%E1%84%80%E1%85%A1-%E1%84%8C%E1%85%A6%E1%84%80%E1%85%A9%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%8C%E1%85%AE%E1%84%8B%E1%85%AD-%E1%84%80%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC) 등이 있다.

Create React App으로 만든 프로젝트의 경우 react-scripts라는 모듈이 사용되고 있으며, Next.js의 경우 next 모듈이 사용된다.

## 5. 빌드 툴

프로젝트 생성 툴의 구성은 내부적으로 다양한 툴의 조합으로 이뤄져 있다.

‣ webpack: 모듈 번들러.

‣ babel: TypeScript, JSX 등과 같이 브라우저가 지원하지 않는 언어를 Javascript로 바꿔주는 컴파일러.

‣ ESLint: 자바스크립트 Code convention 및 문법 검사기

‣ Sass, less: CSS Preprocessor

![](https://blog.kakaocdn.net/dn/dvtlAN/btrqd4p12m3/IW2IVJerRMV3eOKxaL2sO0/img.png)

(webpack 및 다른 빌드 툴이 하나의 파일로 번들링하는 과정)

⇒ 다양한 종류의 빌드 툴이 있음을 알고 있어야 하지만 모든 설정을 외울 필요는 없지만 각각의 설정 파일을 수정해야 할 때는 공식 문서를 통해 문제를 찾아낼 수 있어야 한다.

## 6. 클라이언트 웹 앱 배포

**로컬 환경에서 개발한 코드를 실제 서비스로 만들기 위해서 <mark>빌드 과정과 이를 웹에 노출시키는 배포 과정을 필요로 한다.빌드를 통해 만든 정적 파일이 웹을 통해 제공(serve)되려면 정적 파일을 제공하는 웹 서버가 필요하다.</mark>**

✷ 배포(Deploy): 웹 애플리케이션을 웹에 노출시키는 작업. ⇒ 웹에 노출시켜 사용자에게 웹 프로그램, 웹 앱, 서비스, 애플리케이션 등등을 전달한다.

✷ 호스팅 서비스: 일반적으로 웹 서버라고 하면 웹 서비스를 제공하는 모든 종류의 서버가 웹 서버일 수 있으나, 특별히 정적 파일을 제공할 수 있도록 서버의 공간을 대여해 주는 서비스를 호스팅 서비스라고 부른다.

→ 단순 파일을 웹에서 접근 가능하게 만들어준다.

→ 동적 웹사이트나 (express 등을 사용한) API 서버를 제공하려면 별도의 클라우드 컴퓨팅 서비스가 필요하다.(지금은 클라이언트 웹 앱만을 배포하므로, 호스팅 서비스로도 충분함).

⇒ 클라이언트 앱이 아닌 서버 앱(API 서버)의 경우는, 실제로 node.js를 실행할 수 있는 컴퓨터가 필요하다.

### 6-1. 다양한 웹 호스팅 서비스

‣ 개발자들이 선호하고, 비교적 낮은 가격에 사용할 수 있는 웹 호스팅 서비스들

```
→ Amazon Web Service (AWS) S3(Infrastructure 자체를 제공하는, 다소 복잡한 서비스들의 집합)
→ Google Cloud Storage
→ Vercel(코드 연결과 빌드, 배포까지의 과정을 매우 단순하게 만들어 주는 웹 호스팅 서비스)
→ GitHub Pages
→ Netlify
→ Heroku
```

## 7. Vercel을 이용한 클라이언트 배포

[vercel](https://vercel.com/new)

![](https://blog.kakaocdn.net/dn/oHTEv/btrqmOmnPsL/0IJ0kBvH90V7oaG3wsKd10/img.png)

```
① Vercel 홈페이지 들어가기
② sign up 버튼을 누르고 Continue with Github 누르기
③ 로그인에 성공하면 Import Git Repository라는 화면을 볼 수 있는데, 이를 통해 배포할 Repository를 즉시 선택할 수 있다.
④ Add GitHub Org or Account를 클릭해서 내 GitHub 계정을 연결한다.
⑤ 본인의 계정을 클릭하여 GitHub에 Vercel 앱을 설치한다. ⇒ Vercel은 자체 GitHub 앱을 제공한다. GitHub 플랫폼에 설치하면, 앱이 내 repository에 접근할 수 있다. 내 Repository 목록에 접근할 때 특정 Repository, 혹은 전체 Repository에 접근하게 할 수 있다.
⑥ 연동이 끝나면 본인의 레포지토리 목록들이 표시된다.
⑦ 배포하고 싶은 프로젝트의 레포지토리를 포크한다.
⑧ (프로젝트를 수정해본다)
⑨ Vercel의 첫 화면으로 가서, fork한 Repository가 목록에 표시되는지 확인하고, Import 버튼을 눌러 해당 Git Repository를 배포한다. 배포를 위한 계정 선택 화면에서 개인 계정을 선택한다.

‣ 프로젝트 이름을 원하는 대로 작성한다.
‣ 우리가 fork하고 배포하려는 프로젝트는, Create React App을 이용해서 만들어졌기 때문에, Framework는 Create React App을 선택한다.
‣ build command는 빌드에 필요한 CLI 명령어를 의미한다.
"yarn run build"가 기본값이며, 기본값 그대로 두어도 빌드는 성공적으로 이뤄진다.

‣ "yarn run build" 이후 빌드 결과물이 어떤 디렉토리에 생기는지에 따라 이 값이 변할 수 있다. "build"가 기본값이며, 그대로 두어도 된다.
‣ Deploy 버튼을 눌러 배포를 시작한다.

⑩ 빌드가 성공적으로 이뤄지면, Vercel이 제공하는 URL을 통해 내 프로젝트가 호스팅 된다.
그전에 Open dashboard를 통해 대시보드를 살펴본다.

대시보드에는, 개발 환경이 아닌 프로덕션 환경에서의 배포 현황을 프로젝트 별로 볼 수 있다.

① DEPLOYMENT를 클릭해, 배포 현황과 관련된 CLI 출력을 볼 수 있다.
② DOMAIN을 눌러, 실제 배포된 URL에 접속이 가능하다.
③ STATE를 통해 현재 배포 상태에 대한 확인이 가능하다.
⇒ DOMAIN을 눌러, 실제 배포된 URL을 확인한다.

⇒ fork된 레포지토리에 변경사항을 만들고 푸시하면, 앞으로는 자동으로 빌드 및 배포 과정이 진행될 것이다.
```
