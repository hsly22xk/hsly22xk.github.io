---
layout: single
title: "[React] 특정 페이지에서 Header 안나오게 하기"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

한 번 시도했지만, 제대로 해결된 방법이 아님을 추후에 알고 다시 파고들어 해결한 방법을 기록했다.

## 처음 시도해본 방법

[첫번째 시도](https://hsly22xk.github.io/react/header-footer/)

단순히 헤더를 보이지 않게 하는 데에는 성공했지만, 임의로 새로고침을 해주어야지만 헤더가 없어지는 사이드 이펙트가 있었다.

## 해결 방법

```javascript
// App.js
import React, { useEffect, useState } from 'react';
import { Route, Routes, useLocation } from 'react-router-dom';

...

function App() {
  const [path, setPath] = useState(false);
  const location = useLocation();

    useEffect(() => {
    if (location.pathname === '/' && path) {
      setPath(false);
    } else if (location.pathname !== '/' && !path) {
      setPath(true);
    }
  });
}

return (
  <>
    {path === true ? <Header /> : null}
    <Routes>
      <Route />
    </Routes>
  </>
)
```

```javascript
// index.js
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>,
  document.getElementById('root')
);

...

```

같이 일하는 분이 알려주신 방법으로 해결했다.

먼저 useState()를 사용하여 상태를 만들어주고, useLocation을 활용했다.

(알려주신 방법을 토대로 [useLocation](https://velog.io/@nemo/useLocation) 사용법을 추가로 알아보았다.)

useEffect()를 활용하여 조건을 달아 헤더가 나오는 상태값을 변경시켜주었고, return문 안에 삼항연산자를 활용하여 상태에 따른 헤더 존재 유무 코드를 작성했다.

여기까지만 했을 때는 상태가 계속 바뀌어서 왜 그런가에 대해 고민해봤는데, useEffect안에 있는 조건에서 상태를 넣지 않으면 자동으로 상태값이 바뀌는 바람에 바뀌지 않는 것처럼 보이는 것이었다.

또한, index.js로 BrowserRouter를 빼주지 않았을 때는

Uncaught Error: useLocation() may be used only in the context of a <Router> component.

라는 에러 메시지가 뜬다.

에러 메시지의 의미는 useLocation()은 <Router> 컨텍스트 안에서만 사용할 수 있다는 것이다.

이는 App 컴포넌트가 자식 컴포넌트가 될 수 있도록 해야한다는 의미와 같은데, 이유는 useLocation()이 BrowserRouter 안에 있어야만 사용할 수 있기 때문이다.

처음에는

```javascript
return (
  <BrowserRouter>
    <Routes>
      <Route></Route>
    </Routes>
  </BrowserRouter>
);
```

상기 구조로 되어있었기때문에, App 컴포넌트는 BrowserRouter의 자식 컴포넌트가 될 수 없었다.

그래서 자식 컴포넌트로 만들어주기 위해는 App 컴포넌트를 BrowswerRouter로 감싸주어야한다.

```javascript
// index.js
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>,
  document.getElementById('root')
);

...

```

그래서 위에 적었던 대로 index.js에서 BrowserRouter를 import 해온 후 App 컴포넌트를 감싸주는 형태로 만든 것이다.

처음에는 어떻게 해야할 지에 대해 너무 난감했고, 감 조차 잡히지 않았는데 역시 배워야할 것들이 산더미처럼 넘쳐나고 있다는 것을 다시금 실감할 수 있었다.
