---
layout: single
title: "[React] useState()는 비동기인가 동기인가"
categories: React
tag: [기록, 리액트, react]
author_profile: false
---

React의 useState()는 비동기일까 동기일까?

## 개요

useState는 비동기인가 동기인가.

이런 주제를 왜 생각하게 되었냐면, api 요청을 patch로 하면서 상태를 변경하게 되었는데, 내가 생각한 로직대로 작성하면 제대로 상태가 변경되지 않은 채로 서버에 변경 요청이 가지 않았다.

그래서 내가 생각한대로 상태 변경이 되려면 어떻게 해야할까 생각하며 구글링을 해보다가, useState가 비동기인가 동기인가 라는 흥미로운 주제를 보게 되었다.

그래서 그 부분에 대한 내용을 찾기 시작했고, 정리한 내용을 블로그에 정리해보게 되었다.

## useState()는 비동기이다

결론부터 말하자면 useState는 비동기로 동작한다.

정확하게는, <mark>**setState가 비동기로 동작한다.**</mark>

setState가 비동기로 동작하는 이유는 리액트가 효율적으로 렌더링하기 위해 여러 개의 상태값 변경 요청을 batch(일괄 처리/배치)처리하기 때문이다.

하나의 페이지나 컴포넌트 내에도 수많은 상태값이 존재하는데, 만약 리렌더링을 발생하는 setState가 일어날 때마다 리렌더링이 일어난다면 성능 이슈가 생길 수 있다.

그렇기 때문에 아무리 많은 setState가 연속적으로 사용되었어도 batch 처리에 의해 한 번의 렌더링으로 최신 상태를 유지한다.

✸ batch(일괄 처리): React가 너 나은 성능을 위해 여러개의 state 업데이트를 하나의 리렌더링으로 묶는 것.

React는 16ms 동안 변경된 상태 값들을 하나로 묶는다(16ms 단위로 배치를 진행한다).

## 동기적인 동작을 위해

setState가 비동기로 동작한다는 것을 알았다. 그렇다면 동기적으로 동작하게 하려면 어떻게 할 수 있을까?

① setState의 인자로 함수를 집어넣으면 동기적으로 동작한다(setState내 함수의 매개변수로 이전 상태가 들어온다).

② useEffect()의 종속성 배열을 활용한다.

인데...사실 종속성 배열을 사용하여, 콘솔 로그를 찍었을 때 해당 콘솔의 내용이 제대로 나오지 않았다. 그래서 이 부분은 사실상 구글링을 통해 알아낸 방법이다. 종속성 배열을 사용했을 때 왜 동기적으로 동작하는 지에 대해서는 더 알아볼 부분인 것 같다.

①번의 방법을 사용했을 때, 일반적인 경우 해당이 되는 것 같다.

## 해결 과정

하지만 나의 경우 patch api 요청을 했을 때, 함수 형태로 전달했을 때 제대로 서버까지 변경된 데이터로 들어가지 않았다.

```javascript
import React, { useState } from "react";
import axios from "axios";

const [state, setState] = useState(false); // 초기값을 boolean

const handleChangeFunction = async () => {
  try {
    await axios.patch(`url`, {
      thing: state,
    });
    setState(state);
  } catch (err) {
    console.log(err);
  }
};
```

원래 작성했던 코드는 이런 형식이었는데, 이렇게 작성하면 비동기적으로 작동한다.

```javascript
import React, { useState } from "react";
import axios from "axios";

const [state, setState] = useState(false); // 초기값을 boolean

const handleChangeFunction = async () => {
  try {
    await axios.patch(`url`, {
      thing: state,
    });
    setState((state) => !state);
  } catch (err) {
    console.log(err);
  }
};
```

이함수 형태로 작성하고, ! 연산자를 활용하여 상태를 변경하는 것으로 코드를 수정했다.

하지만 첫 번째와 두 번째 코드에는 state, 즉 초기값 false인 상태가 그대로 patch 요청 안에 들어가있기 때문에 setState()안에 state를 넣어도 변경되지 않는다.

```javascript
import React, { useState } from "react";
import axios from "axios";

const [state, setState] = useState(true); // 초기값을 false -> true

const handleChangeFunction = async () => {
  try {
    await axios.patch(`url`, {
      thing: true,
    });
    setState(true);
  } catch (err) {
    console.log(err);
  }
};
```

임시방편으로 초기값을 true로 작성해두고, 아예 true로 바뀌도록 작성해두었다.

애초에 내가 원했던 방향은 false -> true로 상태가 변경되는 것이었기 때문이다.

하지만 궁극적으로 원하는 그림이 아니기 때문에 꽤 많이 찝찝하다.

+) 글을 작성하다 든 의문점

: patch 요청을 보내는 것 자체가 수정을 요청하는 것인데, 왜 setState를 작성하는 것으로 바뀌지 않을까?

비동기로 작동하더라도, 함수형태로 변경하여 넣어주었을 때는 동기적으로 동작할 것이기 때문에 상태가 바뀌어야하지 않나?
