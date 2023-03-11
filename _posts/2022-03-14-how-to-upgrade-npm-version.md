---
layout: single
title: "node.js, npm 버전 업그레이드 & 다운그레이드"
categories: Information
author_profile: false
---

node.js와 npm 버전은 업그레이드 혹은 다운그레이드가 필요할 때가 있는데, 매번 구글링으로 찾기 힘들어 정리해두었다.

```
node -v
명령어로 노드 버전 확인

npm cache clean -f
npm 캐시 삭제

npm install -g n
노드 버전관리 n 플러그인 설치

n latest // 최신버전 설치
n lts // lts버전 설치
n stable // 안정된 버전 설치

// nvm으로 원하는 버전 깔기
nvm install 버전
```

```
npm -v // npm 현재 버전 확인

npm i -g npm
// npm 업데이트
// -g 옵션이 없으면 현재 프로젝트에만 적용됨

npm i -g npm@버전
// npm 다운그레이드
```
