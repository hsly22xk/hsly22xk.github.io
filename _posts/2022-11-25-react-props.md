---
layout: single
title: "[React] props로 값 전달하여 수정 기능 구현하기"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

리액트 수정 기능 구현하기.

## 개요

react를 배울 때 항상 들었던 말. react를 배울 때 state&props 없이는 아무것도 못한다. 리액트의 꽃이다.

이번에 개발하면서 절실하게 느끼고 있다. 특히, 수강생 때 props라는 개념이 정확하게 뭔지 이해할 수가 없었는데, 이번에 실질적으로 내가 사용해보면서 알아가고 있는 것 같다.

내가 원하는 그림은 글을 수정할 때 등록했던 데이터가 게시판에 그대로 나오고, 그 내용을 바탕으로 수정할 수 있는 것이었다(사실 정확하게 게시판을 만든 것은 아니었으나, CRUD를 구현하는 것은 같기 때문에 제일 이해가 쉬울 것 같은 게시판으로 작성함).

그런데 등록한 데이터가 화면에 뜨지 않은 상태로 나왔다. 심지어 나는 날짜를 선택하는 기능도 있었기 때문에, new Date() 함수를 사용하는 과정에서 어떻게 등록된 데이터를 가져올까 고민하고 있었다.

고민하던 중, 계속해서 개념이 이해되지 않던 props가 생각났다. props로 컴포넌트에 등록된 값이 담겨있는 것을 전달해주면 될 것 같은데?

## 해결 과정

```javascript
// 실제 코드를 그대로 옮기지는 않으나, 비슷하게나마 상황 재현을 해보았다.
// SpecificPages.js

import React, { useState } from 'react';

const SpecificPages = () => {
  const [data, setData] = useState({});
  ...
  ...
  // 이하 코드들 생략
}

return (
  <>
    <div>제목</div>
    <div>{data.title}</div>
    <div>내용</div>
    <div>{data.content}</div>
    <div>날짜</div>
    <div>{data.date}</div>
    ...
    <div>
      <Edit />
    </div>
  </>
)

export default SpecificPages;
```

이러한 형식의 페이지라고 가정했을 때, 수정하는 페이지에 이미 등록된 데이터인 data.title, data.content, data.date가 찍혀 나와야 했다.

```javascript
import Edit from '../../Edit';

const SpecificPages = () => {
  const [data, setData] = useState({});
  ...
  ...
  // 이하 코드들 생략
}

return (
  <>
    <div>제목</div>
    <div>{data.title}</div>
    <div>내용</div>
    <div>{data.content}</div>
    <div>날짜</div>
    <div>{data.date}</div>
    ...
    <div>
      {/* 원하는 컴포넌트에 data를 props로 내려준다 */}
      <Edit data={data} />
    </div>
  </>
)

export default SpecificPages;
```

수정하는 페이지를 Edit 컴포넌트라고 가정하고, 원하는 값인 data를 props로 내려준다.

```javascript
import React, { useState } from 'react';

// Edit 컴포넌트에 내려줬던 props인 data를 받아온다
const Edit = ({ data }) => {
  // 상태변경함수의 초기값을 data.title 등으로 지정하여 처음 등록했던 데이터가 렌더링 될 수 있도록 한다.
  const [title, setTitle] = useState(data.title);
  const [content, setContent] = useState(data.content);
  const [date, setDate] = useState(data.date);

  // handle함수는 onChange함수에 들어갈 이벤트 함수.
  // 어떤 방식으로 e.target.value를 할당해도 상관없지만, handleTitle에 사용한 방식을 조금 더 선호함.
  const handleTitle = (e) => {
    const { value } = e.target;
    setTitle(value);
  }

  const handleContent = (e) => {
    setContent(e.target.value);
  }

  const handleDate = () => {
    const { value } = e.target;
    setDate(value);
  }
}

return (
  <>
    <div>제목</div>
    <div>
      <input
        type='text'
        value={title}
        onChange={handleTitle}
    </div>
    <div>내용</div>
    <div>
      <textarea
        value={content}
        onChange={handleContent}
      />
    </div>
    <div>날짜</div>
    <div>
      <input
        type='date'
        value={date}
        onChange={handleDate}
    </div>
  </>
)

export default Edit;
```

input 태그의 type을 date로 해줄 수 있다는 것을 처음 알았다.

원래 date-picker라는 라이브러리를 사용해서 state를 내려주었는데, input type='date'로 하니까 생각보다 css도 깔끔하게 입혀져 있고, styled component를 활용할 수도 있었다.

어쨌든, props로 값을 내려 컴포넌트에 값을 전달하는 방식으로 수정하는 기능을 구현할 수 있었다.

역시나 이해를 하면 엄청 쉬운데, 이해를 하기까지의 시간이 걸리는 것 같다.
