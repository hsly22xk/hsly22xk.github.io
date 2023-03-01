---
layout: single
title: "[React] Cannot read properties of undefined(reading 'map')"
categories: Error-Handling-Logs
tag: [기록, 리액트, react, 에러핸들링]
author_profile: false
---

```
Uncaught TypeError: Cannot read properties of undefined (reading 'map')
```

## 개요

map을 사용하고 있었는데, Uncaught TypeError: Cannot read properties of undefined (reading 'map') 에러 메시지가 콘솔에 뜨면서 코드가 작동되지 않았다.

콘솔에 찍어봤을 때 map을 돌린 배열이 찍혔는데, 왜 undefined라고 뜨는지에 대해 한참 고민했다.

## 원인

**React는 렌더링이 화면에 커밋 된 후에야 모든 효과를 실행하기 때문이다.**

즉 React는 return에서 배열.map(...)을 반복 실행할 때 첫 턴에 데이터가 아직 안들어와도 렌더링이 실행되며 당연히 그 데이터는 undefined로 정의되어 오류가 나는 것이다.

## 해결 방법

그러면 어떻게 해결할 수 있을지에 대해 구글링을 해본 결과, && 연산자를 쓰는 방법이었다.

true && expression은 항상 expression으로 실행되고 false && expression은 항상 false로 실행된다.

따라서 조건이 참이면 && 바로 뒤의 요소가 출력에 나타난다. 거짓이면 React는 무시하고 건너뛴다.

```javascript
const variable = arr && arr.map((el) => el.id);
```

다음과 같이 작성하면 해결!
