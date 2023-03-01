---
layout: single
title: "[CSS] text-decration: none;(with styled-components)"
categories: React
tag: [기록, 리액트, react, css, styled-components]
author_profile: false
---

React에서 styled-components를 활용하여 링크 밑줄을 없애는 방법.

## 개요

리액트를 사용할 때, Link 혹은 NavLink를 활용하여 내가 이동하고자 하는 url을 링크할 수 있다.

이때, 밑줄이 그어져 있는 것이 기본이라 없애려고 많은 사람들이 text-decoration: none;을 활용하는데, 이상하게 내가 똑같이 하면 안 된다.

똑같은 상황이 생겼을 때 구글링이 아닌 내 블로그에서 찾아볼 수 있도록, 그리고 혹여 누군가가 구글링을 하다가 흘러들어오게 되었을 때 도움이 되길 바라면서 정리해두기로 했다.

## text-decoration: none;의 정의

[text-decoration](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration) 속성은 말 그대로 텍스트를 꾸며주는 속성이다.

기본값이 none이며, 다른 상황에서도 필요에 맞게 사용할 수 있다.

## text-decoration: none;이 되지 않을 때

처음 작성한 코드

```react
import { Link } from "react-router-dom";
import styled from "styled-components";

const Menu = styled.div`
  ...
  text-decoration: none;
`;

...

return (
  <>
    <Link to='/a'>
      <Menu>A</Menu>
    </Link>
  </>
)
```

수정한 코드

```react
import { Link } from "react-router-dom";
import styled from "styled-components";

const MenuConatiner = styled.div`
  padding: 10%;
  display: flex;
  align-items: center;
`;

const NavLink = styled(Link)`
  text-decoration: none;
`;

return (
  <>
    <NavLink to='/a'>
      <Menu>A</Menu>
    </NavLink>
  </>
)
```

단순 CSS 파일 안에서는 a 링크에 들어있다면 바로 text-decoration: none; 속성을 사용하면 해결이 되었지만, styled components를 사용할 때는 Link 안에 a 태그 역할을 하기 때문에 Link 자체로 넣어주어 해결되었다.
