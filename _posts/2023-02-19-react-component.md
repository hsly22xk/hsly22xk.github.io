---
layout: single
title: "[React] 특정 컴포넌트를 특정 페이지에서 안보이게 하기"
categories: React
tag: [기록, 리액트, react]
author_profile: false
---

헤더나 푸터를 특정 페이지에서 보이지 않게 하기.

## 개요

이전에도 정리해둔 [글](https://hsly22xk.github.io/react/react-header/)이 있었는데, 리액트 17 버전이라 useLocation()과 index.js 파일 구조를 BrowserRouter로 감싸줌으로서 해결했었다.

하지만 지금은 리액트 버전이 18이기 때문에 해당 방법으로는 해결할 수 없었다.

## 해결 방법

이번에는 조금 더 간단한 방법으로 해결하면 좋을 것 같아 구글링하다 해결한 방법으로 정리해보았다.

일단, 현재 경우에서는 로그인을 할 때는 Header와 Sidebar를 나오지 않도록 하는 것이다.

[(Outlet을 활용하여 상위 컴포넌트 레이아웃화 시키기는 여기 정리해두었다)](https://hsly22xk.github.io/react/react-outlet/)

이제 로그인 화면에서 Header와 Sidebar를 나오지 않게 하는 것은 더 쉽다.

```react
// App.js

...

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/login" element={<Login />} />
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

/login 으로 들어갔을 때 더 이상 Header와 Sidebar 컴포넌트가 나오지 않는다.
