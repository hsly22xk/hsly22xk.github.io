---
layout: single
title: "[React] 리액트 컴포넌트 메모리 누수"
categories: Error-Handling-Logs
tag: [기록, react, 리액트, 에러핸들링]
author_profile: false
---

리액트 상태 업데이트에 따른 메모리 누수.

## 경고 메시지

[(레퍼런스)](https://kyounghwan01.github.io/blog/React/cant-perform-a-React-state-update-on-an-unmounted-component/#%E1%84%86%E1%85%AE%E1%86%AB%E1%84%8C%E1%85%A6-%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3)

```
Warning: Can't perform a React state update on an unmounted component.
This is a no-op, but it indicates a memory leak in your application.
To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
```

개발을 하다가 상기와 같은 경고 메시지를 콘솔에서 발견했다.

솔직히 에러 메시지만큼이나 거슬리는게 Warning이지만, 구글링과 해석을 통해 하나씩 해결해나갔다.

## 메시지 해석 및 해결

```
unmounted된 컴포넌트에 대해서는 상태 업데이트를 수행할 수 없다.

해당 작업은 수행되지 않지만 메모리 누수가 발생된다. 해결방법으로 useEffect의 cleanup function을 이용해라.
```

```javascript
const [loading, setLoading] = useState(false);

const handleClick = async() => {
  try {

    ...
    setLoading(false);
    ...

  } catch(err) {
    console.log(err);
  }
}
```

상기 코드는 처음 작성했던 코드다. 비동기 작업 처리 과정에서 발생했다.

해당 경고 메시지를 구글링하던 중, 제일 상단에 작성해둔 레퍼런스 링크를 보고 해결을 할 수 있었다.

```javascript
const [loading, setLoading] = useState(false);

const handleClick = async() => {
  try {

    ...
    setLoading(true);
    ...

  } catch(err) {
    console.log(err);
  }
}

useEffect(() => {
  return () => setLoading(false);
}, []);
```

일단 handleClick() 함수에서는 Loading 상태를 true로 변경한 뒤,

경고 메시지에서 알려준대로 useEffect의 cleanup함수를 활용하는 방식으로 해결했다.

사실 레퍼런스 링크에서 말한대로 단순 메모리 누수만을 해결하기 위한 useEffect 함수 작성이 옳은 것인지 모르겠다.

시간적 여유가 될 때 다음과 같은 방법에 대해 더 알아보고 정리하고 싶다.
