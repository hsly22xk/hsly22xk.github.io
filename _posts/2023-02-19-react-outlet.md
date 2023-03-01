---
layout: single
title: "[React] Outlet의 정의와 사용법"
categories: React
tag: [기록, 리액트, react, css]
author_profile: false
---

React의 Outlet

## 개요

페이지를 만들어보다가, 간단한 페이지 하나를 만들어도 레이아웃을 짤 때 계속 복잡해지고 있어 조금 더 간단하게 레이아웃을 짤 수 있는 방법을 찾게 되었다.

그리고 지금은 모든 페이지에 Header와 Sidebar 컴포넌트가 나올 수 있도록 만들지만, 추후 나오지 않을 페이지도 만들 것까지 고려하여 코드를 작성할 때 어떻게 할 수 있을까?를 고민하다 찾은 방법이 Outlet이다.

## 중접 라우팅

Outlet을 설명하기 위해서는 먼저 중첩 라우팅이 뭔지, 어떻게 사용하는 것인지에 대한 이해가 먼저다.

(지금은 중첩 라우팅을 활용하지 않는 페이지들만 있지만, 추후 들어갈 수 있게 하기 위해 설명을 같이 작성한다)

v6에서 중첩 라우팅이 컴포넌트의 children과 같은 개념으로 중첩이 가능해졌고, 더 직관적으로 변했다.

만약, /cart 와 /cart/:memberId 페이지가 있다고 한다면, 이전에는 각각 한 줄씩 차지하였는데, v6에서는 member 라우트 하위에 :memberId 가 포함된 Route를 추가하면 중첩 라우팅이 된다.

하위에 있으면 자동으로 / 로 구분되기 때문에 추가적인 / 를 path에 추가할 필요가 없어졌다.

코드로 표현하면 이렇다.

```react
<Routes>
  <Route path="/cart">
    <Route path=":memberId" /> /cart/:memberId
  </Route>
</Routes>
```

## Outlet

그렇다면 다시 레이아웃화를 조금이나마 간단하게 할 수 있게 하기 위한 방법으로 돌아와본다.

```react
// App.js

...

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Header />
        <Sidebar />
        <Route path="/a-page" element={<PageA />} />
        <Route path="/b-page" element={<PageB />} />
        <Route path="/c-page" element={<PageC />} />
      </Routes>
    </BrowserRouter>
  );
}
```

제일 처음 작성한 코드다.

이렇게 작성하면 모든 페이지들에 Header와 Sidebar 컴포넌트가 나오게 되어 원하는 화면으로 렌더링 되지 않을 뿐만 아니라, 추후 다른 페이지들을 라우팅 할 때도 굉장히 복잡해질 수 있다.

## 방법

1. 먼저 Home 컴포넌트(이름은 마음대로)를 만든다.

2. Outlet을 import 해온다.

3. 각 페이지 컴포넌트가 보여져야 하는 부분에 Outlet 컴포넌트를 넣는다.

4. App.js를 수정해준다.

5. Outlet 영역에 각 Route들에 매칭 시켜놓은 element들이 렌더링 되어 나타난다.

코드로 나타내면 이렇다.

```react
// Home.js
import { Outlet } from "react-router-dom";
import styled from "styled-components";
import Header from "./Header";
import Sidebar from "./Sidebar";

const ContentSection = styled.section`
   // 각종 CSS를 맞추어 작성한다
`;

const Home = () => {
  return (
    <>
      <Header />
      <Sidebar />
      <ContentSection>
        <Outlet />
      </ContentSection>
    </>
  );
};

export default Home;
```

```react
// App.js

...

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route exact path="/" element={<Home />}>
          <Route path="/a-page" element={<PageA />} />
          <Route path="/b-page" element={<PageB />} />
          <Route path="/c-page" element={<PageC />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```
