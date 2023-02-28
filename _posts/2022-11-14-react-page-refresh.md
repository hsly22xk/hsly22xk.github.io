---
layout: single
title: "[React] 페이지 새로고침 없이 렌더링하기"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

페이지 새로고침없이 바로 렌더링하는 방법.

## 새로고침 없이 렌더링하기(with useState() & useEffect())

페이지를 일일이 새로고침 해주어야지만 응답 데이터가 렌더링되는 것이 효율적이지 못하다고 생각해서 해결법을 찾아보다 나온 방법이다(실제로 해결이 되었다).

```javascript
const [state, setState] = useState(0);
useEffect(() => {
	...
    transState();
}, [state]);
```

useState를 사용하는 방식으로 해결했다.

useEffect 두 번째 인자에 값을 넣어주면 state라는 값이 변화할 때 마다 useEffect는 함수 호출을 하게 되는 식이다.
