---
layout: single
title: "[React] NavLink에 styled-components 적용하기"
categories: React
tag: [기록, 리액트, react, NavLink, styled-components]
author_profile: false
---

NavLink에 styled-components 적용하는 방법

해당 [(reference)](https://velog.io/@jm1225/styled-components-NavLink-active-styled-input)를 참고함.

원래 NavLink를 활용하여 header에 로고를 클릭하면 바로 루트 페이지로 이동할 수 있게끔 만들었다.

그런데 다른 컴포넌트들은 styled components를 활용하여 css를 적용했는데, header만 따로 css파일을 만드는 것이 거슬려서 NavLink를 활용하면서 styled components를 적용할 수 있는 방법을 찾아보았다.

```javascript
import { NavLink } from 'react-router-dom'; // ① NavLink import
import styled from 'styled-components'; // ② styled-components import

export const NavStyle = styled(NavLink)`
  color: black;
  font-size: 20px;
  position: absolute;
  top: 10px;
  left: 600px;
  &:link {
    transition: 0.5s;
    text-decoration: none;
  }`; // ③ styled components로 NavLink css 적용

...

// ④ 위에서 css 적용했던 NavStyle 적용
return (
<>
  <NavStyle className={({ isActive }) => (isActive ? 'active' : '')} to='/' >
    <h3>타이틀(로고)</h3>
  </NavStyle>
</>
)
```
