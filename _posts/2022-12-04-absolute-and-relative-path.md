---
layout: single
title: "[React] 절대경로와 상대경로"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

리액트 파일 상대경로로 불러오는 방법.

## 개요

항상 리액트에서 경로를 지정하여 import 해올 때 상대경로를 사용하게 될 때가 많은데, 경로를 불러오는 게 너무 헷갈려서 애를 먹다가, 아예 절대경로로 사용하는 방법을 쓰고 있다.

[리액트에서 절대경로 사용하는 방법](https://hsly22xk.github.io/react/react-absolute-path/)

하지만 항상 절대경로로 지정해두는 것은 그다지 좋은 방법이 아니기 때문에, 이번 기회에 상대경로로 불러오는 방법에 대해 알아보고, 그 방법을 기술해보고자 한다.

## 파일 구조

```
App.js
src
ㄴ components
  ㄴ Modal
    ㄴ LoginModal.js
    ㄴ LogoutModal.js
  ㄴ Nav
    ㄴ Header.js
ㄴ pages
  ㄴ Login.js
  ㄴ Logout.js
```

## 상대경로로 불러오는 방법

만약 Login 페이지에 Header 컴포넌트를 import 해온다고 가정해보자.

```javascript
// Login.js
import Header from '../components/Nav/Header';

...

return (
  <>
    <Header />
  </>
)
```

이렇게 가져올 수 있다.

(나는 vs code를 사용하기 때문에)vs code에서 사용하게 되면 자동완성으로 내가 어떤 파일에서 가져오게 될 것인지 뜨게 되는데, ../ 이라고 사용하는 것은 내가 바깥쪽에 있는 컴포넌트를 가져오겠다는 의미가 된다.

그렇기 때문에 ../ 을 타이핑하게 되면, 바깥쪽부터 가까운 순서로 컴포넌트를 가져올 수 있다.

Header 컴포넌트의 위치는 components/Nav 폴더 안에 있기 때문에, ../ 을 사용하여 순서대로 가져올 수 있는 것이다.

그렇다면 이번에는 App.js에서 Header 컴포넌트를 가져온다고 가정해보자.

```javascript
// App.js
import Header from './components/Nav/Header';

...

return (
  <>
    <Header />
  </>
)
```

이번에는 ./ 을 사용하여 가져올 수 있었다. 그렇다면 차이가 무엇일까.

App.js는 해당 구조에서 제일 최상단에 위치해있다. 그 말은, 가장 바깥쪽에 있는 App 컴포넌트가 안쪽에 있는 컴포넌트를 가져오겠다는 의미이므로 ./을 사용한다.

./ 은 바깥쪽에서 안쪽에 있는 컴포넌트를 가져올 때,

../은 안쪽에서 바깥쪽에 있는 컴포넌트를 가져올 때 사용할 수 있다는 것을 알 수 있다.

이 절대경로와 상대경로가 처음에는 굉장히 헷갈리고, 어쩔 때는 상대경로를 작성할 때 ../../../ 같은 형식으로 가장 깊게 들어가기도 하는데, 한 번 알고 계속 사용하고 나면 정말 별 것 아니다.

경로를 사용할 때 중요한 것은 내 프로젝트의 구조가 어떻게 되어있는지 내 스스로 잘 알고 있어야 한다.
