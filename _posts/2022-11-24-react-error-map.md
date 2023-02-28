---
layout: single
title: "[React] TypeError: map() is not a function"
categories: Error-Handling-Logs
tag: [기록, react, 리액트, 에러핸들링]
author_profile: false
---

vercel 배포 시도 시 나오는 에러 핸들링.

[(레퍼런스)](https://bobbyhadz.com/blog/react-map-is-not-a-function)

Vercel로 배포를 시도해서, 도메인을 들어가 페이지를 들어가려 했을 때 하얀 화면이 뜨면서 콘솔에 찍힌 에러 메시지였다.

레퍼런스 링크를 참조하여 해결할 수 있었다.

나는 객체를 맵핑해주려고 map을 사용했기 때문에, Array.from()메소드를 사용하여 해결하였다.
