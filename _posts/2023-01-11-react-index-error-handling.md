---
layout: single
title: "[React] 배열에서 인덱스가 밀리는 이유"
categories: Error-Handling-Logs
tag: [기록, React, 리액트, 에러핸들링]
author_profile: false
---

수강생의 질문을 받다가, 어김없이 내가 학습하게 된 내용에 대한 작성글.

## 원인

질문내용은 항목을 수정할 때 처음 입력했던 내용이 나오지 않고 새로고침하기 이전의 내용으로 나온다는 것이었다.

소스코드를 제공받아 직접 레포지토리를 포크하고 클론하여 코드를 살펴보았는데, 페이지네이션을 활용하여 인덱스를 주고 있었는데 map을 활용하는 과정에서 key값이 문제가 되었다.

```javascript
import React, { useState, useEffect } from "react";
import Board from "./Board";
import dummyData from "../dummyData";
import uuid from "react-uuid";

function MainPage() {
  ...

  const [content, setContent] = useState(dummyData);

  // 페이지 당 표시할 데이터 수 상태(기본값으로 5개의 게시글만 표시되도록)
  const [limit, setLimit] = useState(5);

  // 현재 페이지 번호 상태
  const [page, setPage] = useState(1);

  // 각 페이지에서 첫 데이터의 위치(편의상 index로 표현)계산
  const offset = (page - 1) * limit;

  ...

  return (
   ...
   {content.slice(offset, offset + limit).map(value, index) => (
     <Board
       list={value}
       key={index}
       ...
     />
   )
   ...
  )
}
```

리액트에서 map을 활용할 때 key 속성을 주는 이유는 불필요한 렌더링을 줄이고 상태를 효율적으로 관리하기 위함이다.

그러나 원본 코드를 살펴보았을 때 해당 현상이 발생하는 과정은 다음과 같다.

> key 값으로 index를 준다.
>
> 항목을 추가했을 때 기존 컴포넌트들의 index값이 밀린다.
>
> 정해줬던 key 속성과 index 값이 꼬인다.
>
> 수정할 때 내용에서의 상태값이 꼬인다(코드를 따로 작성하진 않음).

key값으로 index를 주면 새로운 데이터가 추가 됐을 때, 즉 항목의 순서가 바뀔 경우 index 값이 다시 매핑된다.

## 해결 방법(1)

> key값을 value.id로 바꾸어준다.

기존 코드는 배열의 앞에서부터 요소를 추가하기 때문에 하나씩 밀리게 된다.

그래서 요소 자체의 index값이 아닌 고유한 값인 value의 id를 넣어주었을 때 밀리지 않고 제대로 수정이 된다.

## 해결 방법(2)

> reverse() 메서드를 사용한다.

1번 방법 처럼, 기존코드는 배열의 앞에서부터 추가하지만 reverse()를 해주면 배열의 뒤에다 추가하는 것과 같은 결과가 되기 때문에 index 값이 밀릴 일이 없어진다.

즉,
기존 코드: [a, b, c] → <mark>d</mark>를 추가 → [<mark>d</mark>, a, b, c]

reverse(): 원래 배열 [a, b, c] → reverse 했을 때 [c, b, a]

→ <mark>d</mark>를 추가

→ 원래 배열 [<mark>d</mark>, a, b, c]

⇒ reverse 하면 [c, b, a, <mark>d</mark>]

이 되는 것이다.

누군가에게 설명을 해주기 위해 나부터 잘 알고 있어야 하고, 이유가 납득이 되어야 하는데, 이번 질문으로 인해 또 하나 알게 되었다. 역시 공부는 끝이 없어...
