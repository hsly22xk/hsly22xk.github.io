---
layout: single
title: "[CSS] NavLink에서 밑줄 없애기 & 스타일 지정(with styled-components)"
categories: React
tag: [기록, 리액트, react, css, styled-components]
author_profile: false
---

NavLink를 사용할 때 밑줄 없애기와 스타일 지정하기.

## 개요

Link의 밑줄을 없애는 방법까지 알아냈는데, 똑같은 방법으로 NavLink를 넣었을 때는 제대로 동작하지 않았다.

NavLink는 Link와 다르게 isActive라는 속성이 있어 삼항연산자를 활용하여 스타일을 지정해 줄 수 있는데, NavLink를 사용했을 때 밑줄이 나오지 않게 하면서 클릭했을 때 글씨 색깔도 바꿀 수 있는 방법이 없을까?

## 해결 방법

styled-components의 &(ampersand)를 활용하여 해결했다.

```react
import { NavLink } from "react-router-dom";
import styled from "styled-components";

const AllNavLink = styled(NavLink)`
  color: black;
  &:link {
    text-decoration: none;
  }
  &.active {
    color: #0c6efd;
    font-weight: 900;
  }
`;

...

const Component = () => {
  return (
    <>
      <AllNavLink
        style={({ isActive }) => (isActive ? "active" : "")}
        to="/a-page"
      >
        <h5>PageA</h5>
      </AllNavLink>
    </>
  )
}
```
