---
layout: single
title: "D+38(39) React 데이터 흐름, Effect Hook"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

React의 데이터 흐름과 effect hook

## 1. React에서의 데이터 흐름

[참고링크](https://hsly22xk.github.io/javascript/javascript-react3/)

✷ React 개발 방식의 큰 특징: **컴포넌트 단위로 시작한다**는 점.

① React는 상향식(bottom-up)으로 앱을 만든다

→ 페이지를 만들기 전에 컴포넌트를 먼저 만들고 조립한다.

→ 테스트가 쉽고 확장성이 좋다(디자인을 받으면 컴포넌트 계층 구조로 나누어야 한다).

② 컴포넌트는 컴포넌트 바깥에서 props를 이용해 데이터를 인자(arguments) / 속성(attributes)처럼 전달받을 수 있다.

→ 데이터를 전달하는 주체는 부모 컴포넌트가 된다. === 데이터 흐름이 하향식(top-down)이다.

⇒ React는 단방향 데이터 흐름(One-way data flow)을 따른다

→ 컴포넌트는 props를 통해 전달받은 데이터가 어디서 왔는지 전혀 알지 못한다.

⇒ 하위 컴포넌트는 상위 컴포넌트로부터 전달받은 데이터의 형태 혹은 타입이 무엇인지만 알 수 있다.

⇒ 동일한 props를 전달하면 동일한 화면이 렌더링 되어야 한다. 한 함수는 동일한 input에 동일한 output이 나와야 한다.

⇒ 이 원칙을 지키려면 데이터 흐름을 강제한다. props는 상위 컴포넌트에서만 전달되도록 한다.

③ 모든 데이터를 state(변할 수 있는 상태값)으로 둘 필요는 없다. → 상태는 최소화하는 것이 가장 좋다. 상태가 많아질수록 애플리케이션은 복잡해진다.

④ 상태를 어디에 위치시켜야 하는 지 봐야한다.

→ 상태가 특정 컴포넌트에서만 유의미하다면 특정 컴포넌트에만 두면 된다.

→ 하나의 상태를 기반으로 두 컴포넌트가 영향을 받는다면(= 두 개의 자식 컴포넌트가 하나의 상태에 접근하고자 할 때) 공통 소유 컴포넌트(= 두 자식의 공통 부모 컴포넌트)를 찾아 그 곳에 상태를 위치해야 한다.

## 2. 상태 끌어올리기(Lifting state up / 역방향 데이터 흐름 추가)

[상태 끌어올리기](https://ko.reactjs.org/docs/lifting-state-up.html)

상위 컴포넌트의 "상태를 변경하는 함수(handler)" 그 자체를 하위 컴포넌트에 props로 전달하고, 이 함수를 하위 컴포넌트가 실행한다(콜백 함수를 사용하는 방법과 비슷하다).

→ 하위 컴포넌트의 어떠한 이벤트가 부모의 상태를 바꾸어야 하는 상황일 때 사용한다.

⇒ 동일한 데이터에 대한 변경사항을 여러 컴포넌트에 반영해야 할 필요가 있을 때 상태 끌어올리기를 사용한다.

ex) 하위 컴포넌트가 전달받은 함수를 버튼 클릭 이벤트가 발생할 때 실행하여 폼 엘리먼트에 입력된 값으로 상위 컴포넌트의 상태를 갱신한다.

```js
// 상위 컴포넌트
function messageBoard() {
  const [messages, setMessages] = useState([]);

  // 상태 변경 함수
  const addNewMessage = (newMessage) => {
    setMessages([...messages, newMessage]);
  };

  return (
    <div>
      // props로 전달
      <NewMessageForm onButtonClick={addNewMessage} />
      <ul id="messages">
        {messages.map((m) => (
          <SingleMessage key={m.id}>{m.content}</SingleMessage>
        ))}
      </ul>
    </div>
  );
}

let messageId = 0;

// 하위 컴포넌트
// 비구조화 할당
function NewMessageForm({ onButtonClick }) {
  const [newMessageContent, setNewMessageContent] = useState("");

  const onTextChange = (e) => {
    setNewMessageContent(e.target.value);
  };

  const onClickSubmit = () => {
    let newMessage = {
      id: messageId++,
      content: newMessageContent,
    };

    // 전달받은 함수 실행, 상태 갱신
    onButtonClick(newMessage);
  };

  return (
    <div id="writing-area">
      <textarea id="new-message-content" onChange={onTextChange}></textarea>
      <button id="submit-new-message" onClick={onClickSubmit}>
        등록
      </button>
    </div>
  );
}

function SingleMessage({ children }) {
  return (
    <li className="message">
      <div>{children}</div>
    </li>
  );
}
```

## 3. Side Effect(부수 효과)

함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우 그 함수는 side effect가 있다고 얘기한다.

ex)

‣ 타이머 사용 (setTimeout)

‣ 데이터 가져오기 (fetch API, localStorage)

```js
let foo = "hello";

function bar() {
  foo = "world";
}

bar(); // bar는 Side Effect를 발생시킨다
```

### 3-1. 순수 함수(Pure Function)

오직 함수의 입력만이 함수의 결과에 영향을 주는 함수.

→ 입력으로 전달된 값을 수정하지 않고, 네트워크 요청과 같은 Side Effect가 없다.

→ 함수의 입력이 아닌 다른 값이 결과에 영향을 미치면 순수 함수라고 부를 수 없다.

⇒ 어떠한 전달 인자가 주어질 경우 항상 똑같은 값이 리턴됨을 보장하기 때문에 예측 가능한 함수이기도 하다.

```js
function upper(str) {
  return str.toUpperCase(); // toUpperCase 메소드는 원본을 수정하지 않는다 (Immutable)
}

upper("hello"); // 'HELLO'
```

### 3-2. React의 함수 컴포넌트

```js
function SingleTweet({ writer, body, createdAt }) {
  return (
    <div>
      <div>{writer}</div>
      <div>{createdAt}</div>
      <div>{body}</div>
    </div>
  );
}
```

→ props가 입력으로, JSX Element가 출력으로 나간다. 여기는 그 어떤 Side Effect도 없으며, 순수 함수로 작동한다.

그러나 보통 React 애플리케이션을 작성할 때는 AJAX 요청이 필요하거나 LocalStorage 또는 타이머와 같은 React와 상관없는 API를 사용하는 경우가 발생할 수 있다.

⇒ 이는 전부 React의 입장에서는 Side Effect. React는 Side Effect를 다루기 위한 Hook인 Effect Hook을 제공한다.

## 4. Effect Hook

① useEffect: 컴포넌트 내에서 Side effect를 실행할 수 있게 하는 Hook

ex) 이 컴포넌트에서 실행하는 Side effect는 브라우저 API를 이용하여 타이틀을 변경하는 것

```js
import { useEffect, useState } from "react";
import "./styles.css";

export default function App() {
  const proverbs = [
    "좌절감으로 배움을 늦추지 마라",
    "Stay hungry, Stay foolish",
    "Memento Mori",
    "Carpe diem",
    "배움에는 끝이 없다",
  ];
  const [idx, setIdx] = useState(0);

  const handleClick = () => {
    setIdx(idx === proverbs.length - 1 ? 0 : idx + 1);
  };

  return (
    <div className="App">
      <button onClick={handleClick}>명언 제조</button>
      <Proverb saying={proverbs[idx]} />
    </div>
  );
}

function Proverb({ saying }) {
  useEffect(() => {
    document.title = saying;
  });
  return (
    <div>
      <h3>오늘의 명언</h3>
      <div>{saying}</div>
    </div>
  );
}
```

‣ useEffect의 첫번째 인자는 함수다. 해당 함수 내에서 side effect를 실행하면 된다.

이 함수는

```
→ 컴포넌트 생성 후 처음 화면에 렌더링(표시)
→ 컴포넌트에 새로운 props가 전달되며 렌더링
→ 컴포넌트에 상태(state)가 바뀌며 렌더링
```

이러한 조건들에서 실행된다.

![](https://blog.kakaocdn.net/dn/yQwpc/btroZFYU6p6/94A1DgZwQTNwPC7RnIHwJ1/img.png)

⇒ 매번 새롭게 컴포넌트가 렌더링될 때 Effect Hook이 실행

② Hook 사용 시 주의사항

‣ 최상위에서만 Hook을 호출한다.

→ 반복문, 조건문, 중첩된 함수 내에서 Hook을 호출하지 말고 early return이 실행되기 전에 항상 React 함수의 최상위(at the top level)에서 Hook을 호출해야 한다.

→ 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 Hook이 호출되는 것이 보장되고, 이 점은 useState 와 useEffect 가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해준다.

‣ React 함수 컴포넌트에서 Hook을 호출한다. ⇒ 이 규칙을 지키면 컴포넌트의 모든 상태 관련 로직을 소스코드에서 명확하게 보이도록 할 수 있다.

③ useEffect(함수, [종속성1, 종속성2, ...])

‣ useEffect의 두 번째 인자는 배열이며, 배열은 조건(어떤 값의 변경이 일어날 때 / 표현식 X)을 담고 있다. 해당 배열엔 어떤 값의 목록이 들어 가는데, 이 배열을 특별히 종속성 배열이라고 부른다.

‣ 배열 내의 종속성1, 또는 종속성2의 값이 변할 때, 첫 번째 인자의 함수가 실행된다. 배열 내의 어떤 값이 변할 때에만, (effect가 발생하는) 함수가 실행된다.

④ 단 한번만 실행되는 Effect 함수

‣ useEffect(함수, []): 컴포넌트가 처음 생성될때만 effect 함수가 실행된다.

⇒ 처음 단 한 번, 외부 API를 통해 리소스를 받아오고 더이상 API 호출이 필요하지 않을 때에 사용할 수 있다.

‣ useEffect(함수): 컴포넌트가 처음 생성되거나, props가 업데이트되거나, 상태(state)가 업데이트될 때 effect 함수가 실행됨

## 5. 컴포넌트 내에서 AJAX 요청

목록 내 필터링을 구현하기 위해서는 다음과 같은 두가지 접근이 있을 수 있다.

① 컴포넌트 내에서 필터링: 전체 목록 데이터를 불러오고, 목록을 검색어로 filter 하는 방법

→ 처음 단 한번, 외부 API로부터 명언 목록을 받아오고, filter 함수를 이용한다.

```js
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs();
    setProverbs(result);
  }, []);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs
          .filter((prvb) => {
            return prvb.toLowerCase().includes(filter.toLowerCase());
          })
          .map((prvb, i) => (
            <Proverb saying={prvb} key={i} />
          ))}
      </ul>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

② 컴포넌트 외부에서 필터링: 컴포넌트 외부로 API 요청을 할 때, 필터링한 결과를 받아오는 방법. 보통, 서버에 매번 검색어와 함께 요청하는 경우가 이에 해당한다.

```js
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs(filter);
    setProverbs(result);
  }, [filter]);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  const handleCounterClick = () => {
    setCount(count + 1);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs.map((prvb, i) => (
          <Proverb saying={prvb} key={i} />
        ))}
      </ul>
      <button onClick={handleCounterClick}>카운터 값: {count}</button>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

‣ HTTP를 이용한 서버 요청을 가정할 때, 두 방식의 차이점

|                        |                      장점                       |                                            단점                                            |
| :--------------------: | :---------------------------------------------: | :----------------------------------------------------------------------------------------: |
| 컴포넌트 내부에서 처리 |          HTTP 요청 빈도를 줄일 수 있다          | 브라우저(클라이언트)의 메모리 상에 많은 데이터를 갖게 되므로, 클라이언트의 부담이 늘어난다 |
| 컴포넌트 외부에서 처리 | 클라이언트가 필터링 구현을 생각하지 않아도 된다 |    빈번한 HTTP 요청이 일어나게 되며, 서버가 필터링을 처리하므로 서버가 부담을 가져간다     |

③ AJAX 요청 보내기 / 요청이 느릴 경우

API의 엔드포인트가 http://서버주소/proverbs 라고 가정하면

```js
useEffect(() => {
  fetch(`http://서버주소/proverbs?q=${filter}`)
    .then((resp) => resp.json())
    .then((result) => {
      setProverbs(result);
    });
}, [filter]);
```

하지만 모든 요청이 즉각적인 응답을 주는 것은 아니기 때문에 로딩 화면(Loading Indicator)의 구현은 중요하다. 로딩화면의 구현에도 상태 처리가 필요하다.

```js
const [isLoading, setIsLoading] = useState(true);

// 생략, LoadingIndicator 컴포넌트는 별도로 구현했음을 가정한다
return {isLoading ? <LoadingIndicator /> : <div>로딩 완료 화면</div>}
```

fetch 요청의 전후로 setIsLoading을 설정해주어 보다 나은 UX를 구현할 수 있다.

```js
useEffect(() => {
  setIsLoading(true);
  fetch(`http://서버주소/proverbs?q=${filter}`)
    .then((resp) => resp.json())
    .then((result) => {
      setProverbs(result);
      setIsLoading(false);
    });
}, [filter]);
```
