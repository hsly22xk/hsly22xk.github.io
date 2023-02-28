---
layout: single
title: "[React] 특정 페이지에서 header/footer 보이지 않게 하기"
categories: React
tag: [기록, 리액트, react]
author_profile: false
---

[(reference)](https://okky.tistory.com/358)

특정 페이지에서 header/footer를 보이지 않게 하고 싶은데, 어떻게 해야할까 고민하다가 구글링을 해본 결과 정말 간단하게 할 수 있는 팁이 있어 공유하여 정리해봤다.

```javascript
const Header = () => {
 ...

 if(window.location.pathname === '/header를 숨기고 싶은 경로') return null;

 return (
   <>
   ...
   </>
 )

}

const Footer = () => {
 ...

 if(window.location.pathname === '/footer를 숨기고 싶은 경로') return null;

 return (
   <>
   ...
   </>
 )

}
```

제일 첫 페이지에 header/footer를 숨기고 싶다면 '/' , 특정 페이지에 숨기고 싶다면 그 경로를 적어주면 끝.

header를 숨길 수 있는 방법을 먼저 찾았는데, 그러면 똑같이 footer도 숨길 수 있지 않을까 하여 적용해봤을 때 잘 적용되는 것을 확인할 수 있었다.
