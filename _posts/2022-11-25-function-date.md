---
layout: single
title: "[function] Date.prototype.toISOString() 활용하기"
categories: React
tag: [기록, react, 리액트, Date.prototype.toISOString()]
author_profile: false
---

(자세한 설명은 [mdn Date.prototype.toISOString()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString)에서 확인 가능)

## 개요

new Date() 함수를 console.log()로 찍어보면 Fri Nov 25 2022 22:13:26 GMT+0900 (한국 표준시) 같은 형식으로 나온다. 하지만 대부분 사람들이(아닐 수도 있지만) 원하는 형태는 yyyy-MM-dd 처럼 년도-월-일의 형태일 것이다.

잘 몰랐을 때는 나도 그냥 new Date()만 사용했었는데, 우연찮게 유데미에서 리액트 관련 강의를 보다가 toISOString()함수를 사용하는 것을 보게 되었다.

## 적용 방법

```javascript
const getDate = (date) => {
  return date.toISOString().slice(0, 10);
};
```

뒤에 붙은 slice함수는, 원래 toISOString()함수로 표현하면 2022-11-25T14:48:00.000Z 형태로 나오는데, 내가 원하는 형태는 년-월-일 형태까지였기 때문에 slice를 사용하여 남겨준 것이다.

Date 관련한 함수는 getYear, getHours, getMinutes, getSeconds까지만 알고 있었는데, 이번에 새로 알게된 함수인 toISOString 함수를 꽤 유용하게 쓸 수 있었다.
