---
layout: single
title: "D+27 React SPA & Router"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

SPA와 Router에 대한 전반적인 설명.

## 1. SPA(Single Page Application)

서버로부터 완전히 새로운 페이지를 불러오는 것이 아닌, 화면을 업데이트하기 위해 필요한 데이터만 서버에서 전달받아 브라우저에서 해당하는 부분만 업데이트하는 방식으로 작동하는 웹 애플리케이션이나 웹 사이트.

① SPA의 장점

• 전체 페이지가 아닌 필요한 부분의 데이터만 받아서 화면을 업데이트하면 되어서 사용자와의 상호작용에 빠르게 반응한다.

• 서버에서 요청한 데이터만 넘겨주기 때문에 서버 과부하가 현저하게 줄어든다.

• 전체 페이지를 렌더링 할 필요가 없어 더 나은 유저 경험을 제공한다.

‣ SPA의 예시: 유튜브, 페이스북, 지메일, 에어비앤비, 넷플릭스 등

②SPA의 단점

• 첫 화면 로딩 시 HTML 파일을 읽어 들이고 그 안의 script안에 있는 JavaScript 파일을 다시 받아오는 과정을 거친다.

HTML파일은 거의 비어있고 대부분의 코드는 JS 파일 안에 들어있다. 자연스럽게 JS 파일이 무거워진다.

즉, Javascript 파일 크기가 크기 때문에 파일을 기다리는 시간으로 인한 첫 화면 로딩 시간이 길어진다.

• 검색 엔진 최적화가 좋지 않다.

구글이나 네이버 같은 검색 엔진은 HTML 파일에 있는 자료를 분석하는 방식으로 구동하는데, SPA는 HTML파일 자료가 별로 없기 때문에 검색 엔진이 적절히 구동하지 못한다.

(다만 SPA에서도 검색 엔진 최적화에 대응할 수 있도록 검색 엔진이 발전하고 있어 점차 사라지고 있는 추세)

## 2. 와이어 프레임과 목업

‣ 와이어 프레임: 웹 페이지의 레이아웃과 UI 요소 등에 대한 뼈대 ⇒ 디자인 컨셉과 사이트 기능에 대한 이해를 할 수 있다.

‣ 목업: 데모 시연, 평가를 위해 최소한의 기능만을 담아놓은 모형 ⇒ 데스크톱/스마트폰의 프레임을 덧씌워 직관적으로 이해하기 쉽게 디자인한 것

이 개념을 바탕으로 웹 페이지의 와이어 프레임을 만들어본다고 생각하자. 리액트는 컴포넌트를 기반으로 만든다고 항상 머리속에서 기억해두자.

① 어떤 컴포넌트를 만들고 어떻게 조합할 지 생각한다.(유튜브 클론 코딩)

② 화면 상단에 <Header />와 <Search />, <Setting />을 만들기로 한다.(각 컴포넌트의 첫글자는 대문자로 써준다)

어떤 페이지를 가더라도 이것들은 전부 상단에 위치하니 그것을 염두에 두며 설계한다.

③ 화면 중앙에는 <Content /> 리스트들이 있을 것이다. 컨텐츠는 디테일만 다른 것 뿐이니 재사용이 가능하겠다.

이렇게 어떤 컴포넌트를 만들 것인지, 어떻게 조합을 할 것인지에 대한 와이어 프레임이다.

그런데 이게 여기서 그대로 끝나는 것이 아니다.

유튜브에 들어가보면 컨텐츠는 썸네일도 있고, 영상 제목도 있고, 영상 올린 사람의 프로필 사진과 채널명, 조회수, 해당 컨텐츠를 올린 날짜, 클릭을 하면 재생이 되는 기능도 들어가 있다.

이 데이터는 영상이 대기 목록에 있을 때도, 혹은 재생 중일 때에도 동일한 내용이 화면에 출력된다. 어떤 상태로 있느냐에 따라 출력되는 위치만 조금씩 달라질 뿐이다.

컴포넌트가 UI 의 필수 요소란 정의도 맞고, 각자 고유의 기능을 가지고 있다는 정의도 맞지만, 어플리케이션 안에서 다뤄지는 데이터를 컴포넌트들끼리 보다 유기적으로 주고 받을 수 있도록 설계해야 한다.

그것을 위해 라우터를 배운다.

## 3. 라우팅(Routing)

SPA는 하나의 페이지를 갖고 있지만 한 종류의 화면만을 사용하지는 않는다는걸 먼저 알고 넘어가야 한다.

예를 들어 인스타그램에는 한 페이지에 여러 게시글이 나오지만, 그 화면만이 인스타그램의 전부는 아니다.

메인 피드 페이지, 알림 페이지, 내 프로필 피드 페이지, 디엠 메시지 페이지...등으로 이루어져 있다. 또한 이 화면에 따라 주소도 달라질 것이다.

다른 주소에 따라 다른 뷰를 보여주는 과정을 "경로에 따라 변경한다."라는 의미로 라우팅이라고 한다.

하지만 리액트에 라우팅이 내장되어 있지 않기 때문에, 직접 주소마다 다른 뷰를 보여줘야 한다.

이를 위해 React SPA에서는 React Routing이라는 라이브러리를 가장 많이 사용한다.

## 4. 리액트 라우터(React Router)의 활용

①리액트 라우터의 주요 컴포넌트

```
‣ 라우터 역할을 하는 <BrowserRouter>
‣경로 매칭 역할을 하는 <Switch>, <Route>
‣ 경로 변경 역할을 하는 <Link>
```

이 주요 컴포넌트들은 리액트 라우터 라이브러리에서 따로 불러와야 하는데, 명령어는 import {BrowserRouter, Switch, Route, Link} from "react-router-dom";

✷ import

필요한 모듈을 불러오는 역할로 비구조화 할당(destructuring assignment)과 비슷하게 이용할 수 있다.

✅ react-router library(리액트 라우터 라이브러리) 설치

```
npm install react-router-dom
```

잘 깔렸는지 확인하기 위해서는 package.json으로 들어가 dependencies에 react-router-dom이라는 라이브러리가 등록되어 있으면 잘 되어있는 것이다.

이제 App.js 파일로 가서 최상단에 react-router 라이브러리가 제공하는 컴포넌트들을 사용하기 위한 세팅을 진행한다.

```js
import React from "react";
import { BrowserRouter, Switch, Route, Link } from "react-router-dom";
```

최상단에 이렇게 써준다.

여기까지 했으면 이제 세팅은 끝났다.

본격적으로 시작하려면, 페이지를 표시하는 컴포넌트들을 만들어준다. App.js 하단에 써준다.

대부분의 웹 페이지는 이렇게 구성되어 있기에 나도 똑같이 따라해봤다.

```js
// Home 컴포넌트
function Home() {
  return <h1>Home</h1>;
}

// MyPage 컴포넌트
function MyPage() {
  return <h1>MyPage</h1>;
}

// Dashboard 컴포넌트
function Dashboard() {
  return <h1>Dashboard</h1>;
}
```

위에서 컴포넌트를 만들어줬으니, 이제 그 컴포넌트로 이동할 메뉴를 제작해준다.

```js
function App() {
  return (
    <div>
      <nav>
        <ul>
          <li>Home</li>
          <li>MyPage</li>
          <li>Dashboard</li>
        </ul>
      </nav>
    </div>
  );
}
```

이제 주소에 맞게 위에서 만들어 주었던 3개의 컴포넌트들을 연결해준다.

```
① <BrowserRouter></BrowserRouter>로 <Route>컴포넌트를 이용하기 위한 환경 세팅을 해준다.
<div>태그로 부모를 만들어주었던 것처럼, <BrowserRouter>로 크게 만든다고 생각하면 된다.

② 그 다음 <Switch> 와 <Route> 로 주소 경로와 3개의 컴포넌트들을 연결해준다.
③<Route>의 path(경로 주소) 속성을 이용하여 경로를 작성한다.
④<Route> 태그 안에 연결하고자 하는 컴포넌트를 넣어준다.
⑤<Link>의 to속성을 이용하여 <Route>컴포넌트에 설정해준 path주소를 연결해준다.
```

위에 써준 과정들을 전부 포함하여 전체적인 코드로 표현하면 이렇다.

```js
import React from "react";
import { BrowserRouter, Route, Switch, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">MyPage</Link>
            </li>
            <li>
              <Link to="/dashboard">Dashboard</Link>
            </li>
          </ul>
        </nav>
        <Switch>
          <Route exact path="/">
            <Home />
          </Route>
          <Route path="/about">
            <MyPage />
          </Route>
          <Route path="/dashboard">
            <Dashboard />
          </Route>
        </Switch>
      </div>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Home</h1>;
}

function MyPage() {
  return <h1>MyPage</h1>;
}

function Dashboard() {
  return <h1>Dashboard</h1>;
}

export default App;
```

✷ 왜 exact는 Home 컴포넌트 Route 에만 존재할까? 언제 쓸까?

리액트 라우터의 특성상 exact속성이 없으면 해당 경로(예시 "/")로 시작하는 중복된 Route 컴포넌트를 모두 보여준다.

exact는 주어진 경로와 정확히 일치해야만 설정한 Route 컴포넌트를 보여주는 역할을 한다.

✷ Home 컴포넌트 다음으로 쓰여진 컴포넌트들은 굳이 exact 속성을 쓰지 않고도 페이지가 전환되는 이유는?

Switch를 사용하여 exact 역할을 대신해주는 경우이다.

하지만 Switch는 순서와 위치가 중요하다. 위에서 아래로 경로를 하나씩 검사하면서 해당 경로에 해당하는 라우트를 실행시키기 때문이다.

이런 경우, 비교할 라우트를 더 상단에 작성해야 한다.

하지만 만약 위의 예제처럼 Home을 위에 둔 상태에서 exact 없이 활용한다면 중복되는 경로로 인해 다른 라우트로의 이동이 불가능하다.

✷ NavLink

활성화 된 라우터에 스타일을 적용하기 위한 컴포넌트로, to에 지정된 path와 URL이 매칭되는 경우 스타일이나 클래스를 적용할 수 있음(activeStyle, activeClassName).

→ path가 "/" 일 때 겹치는 경우를 exact 속성을 사용하는 것처럼, NavLink컴포넌트에서 path가 "/" 일 때 exact="true"를 써준다.

ex)

```js
// react js 예시
<NavLink to ="/" exact="true" activeClassName="selected_icon">
  <i className="far fa-comment-dots"></i>
</NavLink>
<NavLink to="/about" activeClassName="selected_icon">
  <i className="far fa-question-circle"></i>
</NavLink>
<NavLink to="/mypage" activeClassName="selected_icon">
  <i className="far fa-user"></i>
</NavLink>
```

```js
/* react App.css 예시 */
.selected_icon > i {
color: red;
text-shadow: 3px 3px 3px rgb(243, 117, 138);
transition: 0.5s;
<-- transition은 css 속성을 변경할 때 애니메이션 속도를 조절하는 방법을 제공 -->
<-- 색깔이 나타나는 데까지 0.5초 걸린다는 뜻 -->
}
```

## 5. react history 사용 방법

App.js에 useHistory import해오고 index.js들어가서 App컴포넌트를 BrowserRouter로 감싸주기

```js
// index.js 예시
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

```js
// App.js 예시
import React from 'react';
import './App.css';
import { Route, Switch, useHistory } from 'react-router-dom';

import Sidebar from './Sidebar';
import Tweets from './Pages/Tweets';
import MyPage from './Pages/MyPage';
import About from './Pages/About';

const App () => {
const history = useHistory()

let handleFront = () => {
history.goForward()
}

let handleBack = () => {
history.goBack()
}

return (

  <div>
    <div className="App">
      <div>
        <button onClick={handleFront}>앞으로가기</button>
        <button onClick={handleBack}>뒤로가기</button>
      </div>
      <main>
        <Sidebar />
        <Section className="features">
          <Switch>
            <Route exact path="/">
              <Tweets />
            </Route>
            <Route path="/about">
              <About />
            </Route>
            <Route path="/mypage">
              <MyPage />
            </Route>
          </Switch>
        </Section>
      </main>
    </div>
  </div>
 )
}
```

✷ App.js에서가 아닌 아이콘을 눌렀을 때 history를 실현하는 방법

```js
import React from "react";
import { useHistory } from "react-router-dom"; // 넣고 싶은 컴포넌트에 useHistory import
import { NavLink } from "react-router-dom";

const Sidebar = () => {
  const history = useHistory();

  let handleBack = () => {
    history.goBack();
  };

  return (
    <section className="sidebar">
      <NavLink to="/" exact="true" activeClassName="selected_icon">
        <i className="far fa-comment-dots"></i>
      </NavLink>
      <NavLink to="/about" activeClassName="selected_icon">
        <i className="far fa-question-circle"></i>
      </NavLink>
      <NavLink to="/mypage" activeClassName="selected_icon">
        <i className="far fa-user"></i>
      </NavLink>
      <i className="far fa-arrow-alt-circle-left" onClick={handleBack}></i>
      // fontawesome에서 원하는 아이콘을 가져온 후 그 안에 클릭 이벤트 넣기
    </section>
  );
};

export default Sidebar;
```

✷ react history go()?

goBack()과 goFoward()와는 다르게 인자에 숫자를 넣어서 얼만큼 이동을 시킬 것인지 결정한다.

ex)

```js
const history = useHistory();

history.go(1); // 바로 앞페이지로 이동
history.go(-1); // 바로 뒷페이지로 이동
```
