---
layout: single
title: "[DOM] Jump target cannot cross function boundary"
categories: Error-Handling-Logs
tag: [기록, DOM, 돔, 에러핸들링]
author_profile: false
---

DOM CRUD 실습 중 나온 에러 핸들링.

## 개요

해당 글을 작성하다 나온 에러 메시지인데, if문 안에 return 대신 continue를 작성했을 때 발생했다.

## 원인

```
Jump target cannot cross function boundary.
```

직역하면 점프 대상은 함수 경계를 넘을 수 없습니다, 라는 의미인데,

이는 **when we try to use a break/continue statement outside of a for loop, e.g. inforEach()or a function**,

즉 forEach()나 함수 등 for loop 바깥쪽에 break/continue를 사용하려고 할 때 발생하는 오류인 것이다.

## 해결 방법

> try ... catch문을 사용한다.

```javascript
// ex) try catch 예제
const myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const maxValue = 4;
const errorMaxLimit = "Max limit reached";

try {
  myArray.forEach((value) => {
    if (value > maxValue) throw new Error(errorMaxLimit);

    console.log("Current value is ", value);
  });
} catch (error) {
  if (!error.property || error.property !== errorMaxLimit) {
    // another error has happened
    throw error;
  }
}
```

> return을 사용하여 원하지 않는 로직이 실행되지 않도록 한다.

```javascript
// ex) return 예제
const myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const maxValue = 4;

myArray.forEach((value) => {
  if (value > maxValue) return;
  // use the "return" keyword instead of the "break/continue" keyword

  console.log("Current value is ", value);
});
```
