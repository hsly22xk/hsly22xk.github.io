---
layout: single
title: "D+28 React state & props"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

state와 props 관련 내용 정리.

## 1. state(상태)

컴포넌트 사용 중 컴포넌트 안에서 변할 수 있는(변화하는) 값

ex) toggle switch의 on/off 여부

```js
{
  isOn: true;
}
{
  isOff: false;
} // boolean타입
```

‣ 숫자 카운트

(-)minus button 3 (+)plus button 플러스 버튼을 눌렀을 때 1씩 증가하고, 마이너스 버튼을 눌렀을 때 1씩 감소한다고 하면

여기서의 state는 현재 숫자값

```js
{
  count: 3;
}
```

① useState

변수처럼 저장할 수 있는 공간을 만들어주는 함수.

② state hook 사용 방법

예시로, 체크박스에 체크했을 때 "Checked", 체크를 하지 않았을 때는 "Unchecked"라는 문자열이 나오도록 한다.

‣ 먼저 useState를 사용하기 위한 import를 사용해준다.

```js
import { useState } from react;
```

‣ useState를 컴포넌트 안에서 호출해준다.

✷useState 를 호출한다는 것은 "state" 라는 변수를 선언하는 것과 같고, 이 변수의 이름은 아무 이름으로 지어도 된다.

일반적인 변수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 함수가 끝나도 사라지지 않는다.

호출하면 배열을 반환하는데 배열의 0번째 요소는 현재 state 변수(데이터)이고, 1번째 요소는 이 변수(데이터)를 갱신할 수 있는 함수이다.

useState 의 인자로 넘겨주는 값은 state의 초기값이다.

```js
function Checkbox() {
  let [isChecked, setIsChecked] = useState(false);
}
// isChecked = 현재 state의 변수(state를 담는/저장하는 변수)
// setIsChecked = 현재 state의 변수를 변경 할 수 있는 함수(갱신/변경함수)
// false = state의 초기값
```

예시와 함께 해석을 해보자면

isChecked, 즉 체크를 해준것과 체크를 해준 것에 대한 상태를 바꾼 함수(체크를 안할 수도 있으니까), 그에 대한 초기값은 false(boolean타입)이라는 것이다.

```js
// 저 위의 위의 const [isChecked, setIsChecked] = useState(false); 를 풀어쓰면

let stateHookArray = useState(false);
let isChecked = stateHookArray[0];
let setIsChecked = stateHookArray[1];
```

‣ state변수에 저장된 값을 불러온다.

예시에서는 isChecked 가 boolean 값을 가지기 때문에 true or false 여부에 따라 다른 결과가 보이도록 삼항연산자를 사용한다.

```js
function Checkbox() {
  let [isChecked, setIsChecked] = useState(false);
}

return (
  <div>
    <input type="checkbox" checked={isChecked} />
    <span>{isChecked ? "Checked" : "Unchecked"}</span>
  </div>
);
```

✅ 예시에서는 초기값으로 boolean타입을 사용했지만, 문자열도 가능하고 숫자도 가능하며 배열, 객체도 상황에 따라 가능하다.

‣ state 갱신하는 방법

state를 갱신하려면 state변수를 갱신할 수 있는 함수를 호출한다. 예시에는 setIsChecked가 되겠다.

```js
function Checkbox() {
  let [isChecked, setIsChecked] = useState(false);
  let handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  // state를 갱신할 수 있는 함수 setIsCheked함수를 호출하여 이벤트 핸들러 함수 handleChecked를 넣어준다.

  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      // setIsChecked함수가 호출되면서 onChange 이벤트 함수가 호출되고 // 그 결과에
      따라 isChecked변수가 갱신된다.
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}
```

위의 예시의 경우, checkbox가 체크되어 Checked로 값이 변경되었다면 리액트의 isChecked도 변경되어야 한다.

input type="checkbox"엘리먼트의 값이 변경되면 onChange 이벤트가 발생한다.

(onChange 함수: 작성한 Javascript를 통해 변화가 일어났는지 탐지해주는 함수)

리액트는 새로운 isChecked 변수를 Checkbox 컴포넌트에 넘겨 해당 컴포넌트를 다시 렌더링한다.

✷ state hook 사용 시 주의점

① React 컴포넌트는 컴포넌트의 상태가 변경 될 때 마다 새롭게 호출되고, 리렌더링 된다. 이것이 바로 우리가 useState를 쓰는 이유다.

✅ useState를 쓰는 이유는 한 마디로 정리하면 웹이 앱처럼 동작하게 하기 위함이다.

예시를 하나 들어보자. 블로그에 글을 쓸 때, 1~2개만 쓰고 끝나는 것이 아니고, 가끔 게시글 제목이 변경되기도 하며, 제목에 따라 글의 순서가 바뀌기도 한다.

만약 이 제목들을 단지 변수에 저장해놓고 사용하게 되면 상태가 변화할 때 리렌더링 되지 않고 새로고침이 된다.

그런데 제목들을 state라는 변수에 저장을 해놓고 쓰게 되면, state가 변경되었을 때,(제목을 수정한다거나 ㄱㄴㄷ순으로 제목을 정렬한다거나 하는 식의 변경이 될 때) HTML은 자동으로, 새로고침 없이 리렌더링된다.

그래서 자주 바뀌는(중요한) 데이터는 state에 저장하여 쓴다.

② React state는 상태 변경 함수 호출로 변경해야 한다. 강제 변경 시도 시 리렌더링이 되지 않거나 state가 제대로 변경되지 않는다.

## 2. props

‣ props의 특징

① 컴포넌트의 속성(property), 외부로부터 전달받은 값. 즉, 웹 어플리케이션에서 해당 컴포넌트가 가진 속성

② 상위 컴포넌트(부모 컨포넌트)로부터 전달받은 값

React 컴포넌트는 JavaScript 함수와 클래스로, props를 함수의 전달인자(arguments)처럼 전달받아 이를 기반으로 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.

즉, 컴포넌트가 최초 렌더링될 때에 화면에 출력하고자 하는 데이터를 담은 초기값으로 사용할 수 있다.

③ props로 어떤 타입의 값도 넣어 전달할 수 있도록 props는 객체의 형태를 가진다.

④props는 외부로부터 전달받아 변하지 않는 값. 그래서 props는 함부로 변경될 수 없는 읽기 전용(read-only) 객체가 되었다. 함부로 변경되지 않아야 하기 때문이다.

‣ props를 사용하는 방법(How to use props)

① 하위 컴포넌트에 전달하고자 하는 값(data)과 속성을 정의한다.

② props를 이용하여 정의된 값과 속성을 전달한다.

③ 전달받은 props를 렌더링한다.

ex)

```js
function Parent() {
  // ① Parent컴포넌트를 하나 만들고
  return (
    <div className="Parent">
      <h1>Hi, I'm Parent</h1>
      <Child /> // ③ Parent 컴포넌트에 Child컴포넌트를 작성한다.
    </div>
  );
}

function Child() {
  // ② Child 컴포넌트를 하나 만든다.
  return <div className="Child"></div>;
}
```

```js
function Parent() {
  return (
    <div className="Parent">
      <h1>Hi, I'm Parent</h1>
      <a href="www.abcd.com">Click to visit here</a>
      // ④ 전달하고자 하는 속성을 정의한다. // HTML에서의 속성, 값 할당 방식과
      똑같이 한다.
      <Child />
    </div>
  );
}
```

이제 Child컴포넌트에서의 속성도 정의한다.

기본 구문은

```js
<Child attribute={value} />
```

```js
function Parent() {
  return (
    <div className="Parent">
      <h1>Hi, I'm Parent</h1>
      <Child text={"I'm your first child"} />
      // ⑤ text속성을 부여하여 값인 문자열을 써준다.
      <Child />
    </div>
  );
}
```

이제 ⑤번에서 써준 속성을 Child 컴포넌트로 불러온다.

props는 객체이고, 이 객체의 {key : value}는 {attribute : value}와 같은 형태를 띄게 된다.

따라서 js에서 객체의 값에 접근할 때 dot notation을 쓰는 것처럼, props의 값 또한 dot notation으로 접근하여 쓸 수 있다.

```js
function Child() {
  return (
    <div className="Child">
      <p>{props.text}</p>
      // ⑥Parent 컴포넌트에 쓰인 text속성을 쓴 값을 dot notation을 이용하여 불러올
      수 있다.
    </div>
  );
}
```

굳이 Parent 컴포넌트에서 Child 컴포넌트에 text속성을 주지 않고 바로 쓰는 방법도 있다.

```js
function Child() {
  return (
    <div className="Child">
      <p>{props.text}</p>
    </div>
  );
}
```

or

```js
function Child() {
  return (
    <div className="Child">
      <p>{props.children}</p>
      // props.children을 이용하여 바로 Parent 컴포넌트에서 속성값을 불러올 수 있음
      // props.children은 정해진 그 자체의 프레임이기 때문에 그대로 외울 것
    </div>
  );
}
```

![](https://blog.kakaocdn.net/dn/JPy6V/btrjLw6AMqR/nSn5JkV3S9RhYmTY9IXwaK/img.png)

## 3. React의 이벤트 처리(이벤트 핸들러 / Event handler)방식

DOM에서의 처리 방식과 비슷하지만 조금 다르다.

‣ HTML에서의 이벤트 핸들러 방식

```html
<button onclick="handleEvent()">Event</button> // 문자열을 사용하여 이벤트
핸들러 전달, 소문자를 써서 이벤트를 사용함
```

‣ React에서의 이벤트 핸들러 방식

```js
<button onClick={handleEvent}>Event</button>
// {}중괄호 안에 이밴트 핸들러 함수 이름 자체를 불러오는 식이고, 카멜 케이스(앞에는 소문자, 뒤에는 대문자 쓰는 방식 / camel case)로 이벤트를 사용한다.
```

① onChange

작성한 Javascript를 통해 변화가 일어났는지 탐지해주는 함수로 input, textarea, select와 같은 폼(Form) 엘리먼트는 사용자의 입력값을 제어하는데 사용된다.

React에서는 변경될 수 있는 입력값을 일반적으로 컴포넌트의 state로 관리하고 업데이트한다.

ex)

```js
function NameForm() {
  let [name, setName] = useState("");
  let handleChange = (event) => {
    setName(event.target.value);
  };
  // onChange 이벤트가 발생하면 event.target.value를 통해
  // 이벤트 객체에 담겨 있는 input값을 읽어올 수 있다.
  // onChange 는 input의 텍스트가 바뀔 때 마다 발생하는 이벤트

  return (
    <div>
      <input type="text" value={name} onChange={handleChange}></input>
      // 이벤트가 발생하면 handleChange함수가 작동한다 // 이벤트 객체에 담긴
      input값을 setState를 통해 새로운 state로 갱신한다.
      <h1>{name}</h1>
    </div>
  );
}
```

② onClick

사용자가 '클릭'이라는 행동을 했을 때 나타나는 이벤트로, 링크 이동 등의 사용자의 행동에 따라 애플리케이션이 반응해야 할 때 자주 사용하는 이벤트

```js
function NameForm() {
  let [name, setName] = useState("");
  let handleChange = (event) => {
    setName(event.target.value);
  };

  return (
    <div>
      <input type="text" value={name} onChange={handleChange}></input>
      <button onClick={alert(name)}>Button</button>
      // 위의 예시에서 버튼을 누르면 팝업창으로 name입력값이 뜨도록 추가 지정해놓았다.
      <h1>{name}</h1>
    </div>
  );
}
```

그런데 이렇게 하면 원하는 대로 결과가 나오지 않는다.

왜냐하면 onClick 이벤트에 alert(name) 함수를 바로 호출하면 함수 호출 결과가 onClick에 적용된다.

이 alert(name)함수는 컴포넌트가 렌더링될 때 함수 자체가 아니라는 뜻이다.

그래서 버튼을 클릭할 때가 아닌 컴포넌트가 렌더링될 때에 alert 이 실행되고 그 결과인 undefined가 적용된다.(함수는 리턴값이 없을 때 undefined 를 반환하기 때문에 undefined가 적용된다)

onClick 이벤트에 함수를 전달할 때는 리턴문 안에서 함수를 정의하거나 리턴문 외부에서 함수를 정의 후 이벤트에 함수 자체를 전달해야 한다.

단, 둘 다 <mark>화살표 함수(arrow function)</mark>를 사용하여 함수를 정의해야 해당 컴포넌트가 가진 state에 함수들이 접근할 수 있다.

```js
function NameForm() {
  let [name, setName] = useState("");
  return (
    <div>
      <input type="text" value={name} onChange={handleChange}></input>
      <button onClick={() => alert(name)}>Button</button>
      // {() => alert(name)} --> 리턴문 안에서 함수 정의하기
      <h1>{name}</h1>
    </div>
  );
}
```

```js
function NameForm() {
  let [name, setName] = useState("");
  let handleChange = (event) => {
  setName(event.target.value);
};

let handleClick = () => {
  alert(name);
};
// 리턴문 외부에서 함수를 정의하고

  return (
    <div>
      <input type="text" value={name} onChange={handleChange}></input>
      <button onClick={handleClick}>Button</button>
      // 이벤트에 함수 자체 전달하기 <-- {handleClick}
      <h1>{name}</h1>
    </div>
  )
};
```

## 4. React 데이터 흐름

① 컴포넌트를 먼저 만들고 조립한다. ⇒ 컴포넌트 계층 구조로 나누는 것이 먼저다.

상향식(bottom-up)으로 앱을 만든다. ⇒ 확장성이 좋고 테스트 하기 쉽다.

② 데이터는 위에서 아래로 흐른다. ⇒ 데이터의 흐름은 하향식(top-down)이다.

트위틀러의 예시를 들어 트리 구조로 짜고, 데이터를 집어넣어 보자.

![](https://blog.kakaocdn.net/dn/bFcmW3/btrjDhJBu3V/KufCt8nWkYaqBss5QDka41/img.png)

![](https://blog.kakaocdn.net/dn/lMWQy/btrjDhv0XRg/99K8LcVWE3zUSCcEimILmk/img.png)

![](https://blog.kakaocdn.net/dn/b542e6/btrjFzWWY1a/Lm4U2249zFyrjdf5YMBquk/img.png)

SingleTweet 컴포넌트에 2021년 11월 2일 하비가 쓴 "난 고소공포증이 있어" 라는 트윗을 보이게 하려면 어떤 과정을 거칠까?

일단 관련된 데이터가 있어야겠다. 작성자의 이름은 "하비", 날짜는 "오늘 날짜", 컨텐트는 "난 고소공포증이 있어"라는 데이터가 SingleTweet 컴포넌트를 통해 우리가 눈으로 볼 수 있는 컨텐츠로 된다.

![](https://blog.kakaocdn.net/dn/bj02fN/btrjCR5qpUb/kiboQn7CXqukF4VKTXgUmK/img.png)

컴포넌트는 컴포넌트 바깥에서 props를 이용해 데이터를 마치 인자(arg)혹은 속성(attributes)처럼 전달 받을 수 있다.

즉 데이터를 전달하는 주체는 부모 컴포넌트가 된다. 이 말이 데이터의 흐름은 하향식이라는 것을 의미한다.

⇒ 데이터의 흐름이 하향식이라는 것은 React는 단방향 데이터 흐름을 따른다는 말로 통한다.

⇒ 컴포넌트는 props(부모로부터 받는 데이터)를 통해 전달받은 데이터가 어디서 왔는지 전혀 알지 못한다.

③ 상태 위치 정하기

트위틀러를 계속 이어서 생각해보자. 우리가 트위틀러를 만들기 위해 가장 필요한 데이터에는 무엇이 있을까?

```
전체 트윗 목록
사용자가 새롭게 작성 중인 트윗 내용
```

그런데 상태가 하나의 특정한 컴포넌트에만 유의미하다면 그렇게 하면 되지만, 상태가 하나인데 두 개 이상의 컴포넌트가 영향을 받는다면 공통 소유 컴포넌트를 찾아 그곳에 상태를 위치해야 한다.

⇒ 두 개 이상의 자식 컴포넌트가 하나의 상태에 접근하고자 할 때는 공통 부모 컴포넌트에 상태를 위치해야 한다.

그러니 전체 트윗 목록은 공통 부모 컴포넌트에 상태를 위치하고, 사용자가 새롭게 작성 중인 트윗 내용은 그냥 SingleTweet에 위치하면 된다는 거다.

![](https://blog.kakaocdn.net/dn/Ik34R/btrjHTOwOv1/koOEFL0aOjMCbP84sLRDbk/img.png)

그렇다면 위에서 전체 트윗 목록 상태는 Tweets에서 필요한 목록이고, SingleTweet들은 모두 Tweets에 의존하는 자식 컴포넌트들이다. 즉, 이들의 부모 컴포넌트는 Tweets이다.

그렇기 때문에 전체 트윗 목록 상태는 Tweets에 넣는다.(데이터 전달 주체는 부모 컴포넌트)

⇒ React에서 데이터를 다룰 때는 컴포넌트들간의 상호 관계와 데이터의 역할, 데이터의 흐름을 고려하여 위치를 설정한다.

✷ state로 두어야 하는지 여부

‣ 부모로부터 props를 통해 전달되면 state가 아니고

‣ 시간이 지나도 변하지 않으면 state가 아니고

‣ 컴포넌트 안의 다른 state나 props를 가지고 계산 가능하다면 state가 아니다.
