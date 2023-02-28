---
layout: single
title: "[Javascript] Zero Fill in Javascript"
categories: React
tag: [기록, react, 리액트, javascript]
author_profile: false
---

javascript에서 zero fill을 사용하는 방법.

## 개요

개발 도중 숫자 앞에 0 등의 숫자를 작성하여 여백을 표현해야 하는 상황이 생겼다.

→ 구글링을 해보니 이런 것들을 zero fill이라고 한다.

구글링을 하다 찾게 된 mdn 문서가 있었는데, 바로 [padStart()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart)였다.

그런데 문제가 있었다.

클라이언트가 input창으로 보내줄 때 데이터 타입은 string이었는데, 막상 서버에서 받아오는 데이터 타입은 number였다.

처음 생각했던 방법은 데이터베이스에 데이터를 저장하는 타입을 string으로 바꾸자고 할까? 였다.

하지만 딱히 number가 아닌 string으로 저장한다고해서 뭔가 더 좋아지는 것은 아니었다.

## String.prototype.padStart()

그렇다면 어떻게 해야할까?를 더 생각하다보니, 어쨌든 프론트엔드에서는 요청을 받아 응답이 온 데이터를 띄워주는 것이니, 보여질 때만 zero fill로 해주면 되는 것 아닐까? 라는 생각이 났다.

그렇다면 number로 응답받아오는 데이터 타입을 String()을 활용해 문자열로 바꾸고, 그 안에서 padStart()를 사용하면 될 것 같아! 그리고 정말 됐다.

```javascript
const str1 = "5";
console.log(str1.padStart(2, "0"));
// expected output: "05"
```

해당 코드는 mdn의 예시이다. 문자열인 '5'를 padStart()를 활용하여 여백을 문자열 '0'으로 채워주는 것이다.

00을 붙이고 싶다면 str1.padStart(3, '0')을 사용하면 된다.

개발을 하면서 여러가지를 더 많이 알게 된다. 어떻게 할 수 있을까 고민이 됐는데, 해결이 되어서 기분이 좋아졌다.
