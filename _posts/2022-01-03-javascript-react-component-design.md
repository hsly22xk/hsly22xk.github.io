---
layout: single
title: "D+43(44, 45) React Component Design(Storybook, CSS-in-JS, useRef, UI Component)"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

React component design(feat. CSS-in-JS)

## 1. Component-Driven Development(CDD)

부품 단위로 UI 컴포넌트를 만들어 나가는 개발. UI(User Interface) 컴포넌트 제작 방식.

![](https://blog.kakaocdn.net/dn/nmOfV/btrpIyROitv/CuOkvkyZawPzgkyYzFUXD0/img.png)

### ① storybook

[storybook](https://www.daleseo.com/storybook/)

CDD를 하기 위한 UI 개발 도구의 일종.

Component Driven Development 가 트렌드로 자리 잡게 되면서 이를 지원하는 도구 중 하나인 Component Explorer(컴포넌트 탐색기)가 등장했는데, 그 안의 많은 UI 개발도구 중 하나.

### ② stroybook을 사용하는 이유

[storybook](https://storybook.js.org/docs/react/get-started/introduction)

→ Storybook은 기본적으로 독립적인 개발환경에서 실행되기 때문에 개발자는 애플리케이션의 다양한 상황에 구애받지 않고 UI 컴포넌트를 집중적으로 개발 할 수 있다.

→ 각각의 컴포넌트들을 따로 볼 수 있게 구성해주어 <mark>한 번에 하나의 컴포넌트에서 작업할 수 있다.</mark>

→ 복잡한 개발 스택을 시작하거나, 특정 데이터를 데이터베이스로 강제 이동하거나, 애플리케이션을 탐색할 필요 없이 <mark>전체 UI를 한눈에 보고 개발할 수 있다.</mark>

→ <mark>재사용성을 확대</mark>하기 위해 컴포넌트를 문서화하고, 자동으로 컴포넌트를 시각화하여 시뮬레이션할 수 있는 다양한 테스트 상태를 확인하여 <mark>버그를 사전에 방지</mark>할 수 있도록 도와준다.

→ <mark>테스트 및 개발 속도를 향상</mark>시키는 장점이 있으며, 애플리케이션 또한 **의존성 걱정 없이 빌드할 수 있다.**

### ③ 주요 기능

‣ UI 컴포넌트들을 카탈로그화 하기

‣ 컴포넌트 변화를 Stories로 저장하기

‣ 핫 모듈 리로딩과 같은 개발 툴 경험 제공하기

‣ 리액트를 포함한 다양한 뷰 레이어 지원하기

### ④ 설치 및 세팅 방법

[공식문서](https://storybook.js.org/tutorials/intro-to-storybook/react/en/get-started/)

```
# Clone the template
npx degit chromaui/intro-storybook-react-template taskbox

cd taskbox

# Install dependencies
yarn
```

### ⑤ 예시

```js
import React from "react";
import { Button } from "@storybook/react/demo";

// 버튼 컴포넌트
export default {
  title: "Button",
  component: Button,
};

// 버튼 컴포넌트를 커스텀한 컴포넌트들인 Primary와 Secondary
// 이 function components를 export하면 storybook에서 UI 목업을 확인할 수 있음
export const Primary = () => <Button>Hello Button</Button>;

export const Secondary = () => <Button>Bye Button</Button>;
```

## 2. CSS-in-JS 방법론

### ① 구조적인 CSS 작성 방법의 발전

‣ 구조적인 CSS 작성 방법이 필요해진 이유 : 프로젝트의 규모와 복잡도, 그것을 함께 작업 할 팀원 수의 증가에 따라 CSS 작성의 일관된 패턴이 없는 것과 모바일 / 태블릿 포함 다양한 디바이스들의 등장으로 웹사이트들의 다양한 디스플레이 커버로 인한 CSS의 복잡성.

⇒ CSS 작업을 효율적으로 하기 위해 CSS를 구조화하는 방법에 대한 연구의 필요성 대두.

#### ①-1. CSS 전처리기(CSS Preprocessor)

CSS의 구조적 작성을 도와주는 도구로, 흔히 CSS문서를 작성할 때 생기는 문제점들을 프로그래밍 개념 활용으로 해결할 수 있음

ex) CSS문서작업에서의 반복적이고 번거로운 작업들(Color값 찾기, tag 닫기 등) 클래스 상속 등의 사항으로 인한 문서의 양이 많아지며 유지관리에 영향을 미치는 것.

‣ CSS 전처리기(CSS Preprocessor) 자체만으로는 웹 서버가 인지하지 못함 → 각 CSS 전처리기에 맞는 Compiler를 사용해야 하고 컴파일 하면 실제 사용하는 CSS 문서로 변환됨.

→ CSS 파일들을 잘 구조화 할 수 있게 됐고, 최소한 CSS 파일을 몇 개의 작은 파일로 분리할 수 있는 방법이 생김.

✅ SASS(Syntactically Awesome Style Sheets)

CSS를 확장해 주는 스크립팅 언어. CSS를 만들어주는 언어.

→ 특정 속성의 값(color, margin, width 등)(#ffffff, 25rem, 100px 등)을 자바스크립트처럼 변수로 선언하여 필요한 곳에 선언된 변수를 적용할 수도 있고, 반복되는 코드를 한 번의 선언으로 여러 곳에서 재사용할 수 있도록 해 주는 등의 기능.

⇒ SCSS 코드를 읽어 전처리한 후 컴파일해 전역 CSS 번들 파일을 만들어 주는 전처리기(preprocessor)역할을 함.

ex) CSS와 SASS 사용 예제

```css
/* 일반적인 CSS 사용 예제 */
.alert {
  border: 1px solid rgba(188, 83, 140, 0.89);
}

.button {
  color: rgba(188, 83, 140, 0.89);
}
```

**<mark>반복되는 CSS 코드가 있을 때 변수를 활용할 수 있으며, 변수 선언 시 $ 기호로 표시한다.</mark>**

```
/* SASS 사용 예제 */

$base color: rgba(188, 83, 140, 0.89)

.alert {
  border: 1px solid $border-dark
}

.button {
  color: $border-dark
}
```

⇒ 결국 SASS가 CSS의 구조화를 해결해 주는 것의 장점보다 다른 문제들을 더 많이 만들어낸다는 것이 밝혀지고, 전처리기(preprocessor)가 내부에서 어떤 작업을 하는지는 알지 못한 채 스타일이 겹치는 문제를 해결하기 위해 단순히 계층 구조를 만들어 내는 것에 의지하게 되었고, 컴파일된 CSS의 용량이 커지게 되었다.

⇒ CSS 전처리기의 문제를 보완하기 위해 BEM, OOCSS, SMACSS 같은 CSS 방법론이 대두되었다. 각각의 장단점이 있으나 세 방법론 모두 같은 지향점을 가지고 있다.

⇒ CSS 방법론들은 같이 일하는 팀 동료들의 팀워크와도 연결되기 때문에 여러 팀원이 함께 작업하는 상황에서 CSS 작성에 있어서 방법들을 규칙으로 정해두는 것은 매우 중요한 요소다.

✷ 방법론의 공통 지향점

‣ 코드의 재사용

‣ 코드의 간결화(유지보수 용이)

‣ 코드의 확장성(확장 가능)

‣ 코드의 예측성(클래스 명으로 의미 예측 가능)

#### ①-2. BEM(Block, Element, Modifier)

Block, Element, Modifier로 구분하여 클래스를 작명하는 방법.

‣ Block: 전체를 감싸고 있는 블록 요소

‣ Element: 블록이 포함하고 있는 한 조각의 요소

‣ Modifier: 블록 / 요소의 속성(블록 / 엘리먼트의 외관이나 상태를 변화 가능하게 하는 부분)

→ Block, Element, Modifier 각각은 '--'와 '\_\_'로 구분한다.

ex)

```
/Block/   /Element/  /Modifier/
.header__navigation--navi-text {
  color: red;
}
```

→ 클래스명은 BEM 방식의 이름을 여러 번 반복하여 재사용할 수 있도록 한다.

→ HTML/CSS/SASS 파일에서 더 일관된 코딩 구조를 만들어준다.

: 클래스명 선택자가 장황해지고 마크업이 불필요하게 커지며 재사용 시 모든 UI 컴포넌트를 명시적으로 확장해야함. SASS와 BEM도 고치지 못했던 몇 가지 문제들은 언어 로직 상에 진정한 캡슐화의 개념이 없다는 것.

(✷ 캡슐화(encapsulation): 객체의 속성과 행위를 하나로 묶고 실제 구현 내용 일부를 외부에 감추어 은닉하는 개념)

이로 인한 유일한 클래스명을 선택한다는 것에 의존해야만 했음.

→ 어플리케이션으로 개발 방향이 진화하면서 컴포넌트 단위의 개발은 캡슐화의 중요성을 불러왔지만 CSS는 컴포넌트 기반의 방식을 위해 만들어진 적이 한번도 없었다.

**<mark>⇒ CSS도 컴포넌트 영역으로 불러들이기 위해 CSS-in-JS가 탄생.</mark>**

**<mark style='background-color: #dcffe4'>✷ CSS-in-JS는 그때 그때 필요한 만큼만 style 태그를 생성</mark>**

✅ [CSS-in-JS의 장점](https://blueshw.github.io/2020/09/14/why-css-in-css/)

→ Global namespace: class명이 build time에 유니크한 해시값으로 변경되기 때문에 별도의 명명 규칙이 필요하지 않다.이는 협업과 유지보수에 용이하다는 장점이 있다.

→ Dependencies: CSS가 컴포넌트 단위로 추상화되기 때문에 CSS 파일(모듈)간에 의존성을 신경 쓰지 않아도 된다.

→ Dead Code Elimination: 컴포넌트와 CSS가 동일한 구조로 관리되므로(다른 컴포넌트에게 영향을 주지 않음) 수정 및 삭제가 용이하다.

→ Minification: 네임스페이스 충돌을 막기위해 BEM 같은 방법론을 사용하면 class 명이 길어질 수 있지만 CSS-in-JS는 짧은 길이의 유니크한 클래스를 자동으로 생성한다.

→ Sharing Constants: CSS 코드를 JS에 작성하므로 컴포넌트의 상태에 따른 동적 코딩이 가능하다.

→ Non-deterministic Resolution: CSS가 컴포넌트 스코프에서만 적용되기 때문에 우선순위에 따른 문제가 발생하지 않는다.

→ Isolation: CSS가 JS와 결합해 있기 때문에 상속에 관한 문제를 신경 쓰지 않아도 된다.

‣ CSS-in-JS의 단점

→ 러닝 커브(learning curve): 무언가를 습득하는 데 드는 시간.

새로운 기술을 배울 때 처음에는 더디다가 어느 지점을 지나면 배움에 가속도가 붙고, 다시 더뎌지는 것.

→ 새로운 의존성

→ 별도의 라이브러리를 설치해야 하므로 번들 크기가 커진다.

→ 인터랙션한 페이지일 경우 CSS 파일을 따로 관리하는 방법에 비해 느린 성능을 보여줄 수 있다.

## 3. Tailwind CSS

[tailwind](https://tailwindcss.com/)

Utility-first CSS로서 각 class가 담당할 스타일을 미리 정의하고 필요한 class들을 조합해서 적용하는 식으로 사용.

```html
// 기본 HTML, CSS 를 활용한 코드 작성 예시
<div class="chat-notification">
  <div class="chat-notification-logo-wrapper">
    <img
      class="chat-notification-logo"
      src="/img/logo.svg"
      alt="ChitChat Logo"
    />
  </div>
  <div class="chat-notification-content">
    <h4 class="chat-notification-title">ChitChat</h4>
    <p class="chat-notification-message">You have a new message!</p>
  </div>
</div>

<style>
  .chat-notification {
    display: flex;
    max-width: 24rem;
    margin: 0 auto;
    padding: 1.5rem;
    border-radius: 0.5rem;
    background-color: #fff;
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  }
  .chat-notification-logo-wrapper {
    flex-shrink: 0;
  }
  .chat-notification-logo {
    height: 3rem;
    width: 3rem;
  }
  .chat-notification-content {
    margin-left: 1.5rem;
    padding-top: 0.25rem;
  }
  .chat-notification-title {
    color: #1a202c;
    font-size: 1.25rem;
    line-height: 1.25;
  }
  .chat-notification-message {
    color: #718096;
    font-size: 1rem;
    line-height: 1.5;
  }
</style>
```

```html
// Tailwind CSS를 활용한 코드 작성 예시
<div class="max-w-sm mx-auto flex p-6 bg-white rounded-lg shadow-xl">
  <div class="flex-shrink-0">
    <img class="h-12 w-12" src="/img/logo.svg" alt="ChitChat Logo" />
  </div>
  <div class="ml-6 pt-1">
    <h4 class="text-xl text-gray-900 leading-tight">ChitChat</h4>
    <p class="text-base text-gray-600 leading-normal">
      You have a new message!
    </p>
  </div>
</div>
```

[✷ Tailwind Cheat Sheet](https://nerdcave.com/tailwind-cheat-sheet)

## 4. Styled-Component

기능적(Functional) / 상태를 가진 컴포넌트들로부터 UI를 완전 분리해 사용할 수 있는 아주 단순한 패턴 제공.

‣ 설치 방법

```
npm install --save styled-components

// package.json에 다음 코드 추가
// 여러 버전의 Styled Component가 설치되어 발생하는 문제를 줄여줌.
{
  "resolutions": {
    "styled-components": "^5"
  }
}
```

‣ 특징 → Automatic critical CSS: 화면에 어떤 컴포넌트가 렌더링 되었는지 추적하여 해당하는 컴포넌트에 대한 스타일 자동 삽입.

코드의 적절한 분해로 사용자가 어플리케이션 사용 시 최소한의 코드만으로 화면이 띄워지도록 할 수 있음.

→ No class name bugs: 스스로 유니크한 className 생성, className의 중복 / 오타로 인한 버그를 줄여줌.

→ Easier deletion of CSS: 기존에는 사용하지 않거나 삭제한 컴포넌트에 해당하는 스타일 속성 제거를 위해 파일 안의 className을 찾았으나, Styled Component는 모든 스타일 속성이 특정 컴포넌트와 연결되어 있어 <mark>컴포넌트를 더 이상 사용하지 않아 삭제한 경우 이에 대한 스타일 속성도 함께 삭제됨.</mark>

→ Simple dynamic styling: className을 일일이 수동으로 관리할 필요 없음. React의 props나 전역 속성을 기반으로 컴포넌트에 스타일 속성 부여, 간단하고 직관적.

→ Painless maintenance: 컴포넌트에 스타일을 상속하는 속성을 찾아 다른 CSS 파일들을 검색하지 않아도 됨. 코드의 크기가 커지더라도 유지 보수가 어렵지 않음.

→ Automatic vendor prefixing: 개별 컴포넌트마다 기존의 CSS를 이용하여 스타일 속성을 정의함. 이외의 것들은 Styled Component가 알아서 처리함.

→ 중첩 스타일링을 위해 SCSS 와 같은 전처리 기능을 자동으로 지원한다. 중첩 스타일링을 하기 위해 ampersand(<mark>&</mark>) 기호를 사용.

ex)

```js
import styled from "styled-components";
import React from "react";

const Thing = styled.div`
  color: blue;

  &:hover {
    color: red; // <Thing> when hovered
  }

  & ~ & {
    background: tomato; // <Thing> as a sibling of <Thing>, but maybe not directly next to it
  }

  & + & {
    background: lime; // <Thing> next to <Thing>
  }

  &.apple {
    background: orange; // <Thing> tagged with an additional CSS class ".apple"
  }

  .banana & {
    border: 1px solid; // <Thing> inside another element labeled ".banana"
  }

  .blueberry {
    background-color: yellow; // an element labeled ".blueberry" inside <Thing> without ampersand(&)
  }
`;

export default function App() {
  return (
    <React.Fragment>
      <Thing>기본 Thing Styled-Component</Thing>
      <Thing>
        Thing Styled-Component와 붙어 있는 Thing Styled-Component (& + &)
      </Thing>
      <Thing className="apple">
        Thing Styled-Component에 apple 클래스 적용한 예제 (&.apple)
      </Thing>
      <div>기본 div 태그입니다.</div>
      <Thing>Thing Styled-Component의 형제 컴포넌트 (& ~ &)</Thing>
      <div className="banana">
        <Thing>
          banana 클래스를 가진 엘리먼트를 부모로 가진 Thing Styled-Component
          (.banana &)
        </Thing>
      </div>
      <Thing>
        <span className="blueberry">
          ampersand(&)를 사용하지 않은 예제입니다.
        </span>
      </Thing>
    </React.Fragment>
  );
}
```

⇒ 만약 & 기호를 사용하지 않으면 평범한 후손 셀렉터로 동작.

ex)

```js
import styled from "styled-components";
import React from "react";

const Thing = styled.div`
  color: blue;

  .something {
    border: 2px solid orangered;
    margin: 5px;
    padding: 3px;
  }
  #something-else {
    border: 2px solid black;
    margin: 5px;
    padding: 3px;
  }
`;

export default function App() {
  return (
    <>
      <Thing>
        <div className="something">className</div>
        <div id="something-else">id</div>
      </Thing>
    </>
  );
}
```

⇒ ampersand(&)는 컴포넌트 안에서 적용되는 CSS 규칙을 확장해 줌으로써, 특히 순수 CSS 와 Styled Component 를 혼용해서 사용해야 하는 경우에 각 스타일 간의 충돌을 피하는 데에 유용하게 사용할 수 있다.

‣ Styled Component는 [tagged template literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals) 라는 ES6 문법을 이용한다.

컴포넌트를 만들 때에 해당 문법을 사용하여 컴포넌트의 스타일 속성을 정의하면 별도의 CSS 파일 없이 스타일 속성을 지닌 컴포넌트를 만들 수 있다.

ex)

```js
import styled from "styled-components";

// <h1> 태그를 렌더링 할 title component를 만든다
// ``백틱 써주는 것은 필수
// Title과 Wrapper 안의 CSS 속성들을 바꿔가며 연습 가능
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// <section> 태그를 렌더링 할 Wrapper component를 만든다
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

export default function App() {
  // 일반적으로 컴포넌트를 사용하는 것처럼 Title과 Wrapper를 사용한다
  return (
    <Wrapper>
      <Title>Hello World!</Title>
    </Wrapper>
  );
}
```

✷ **Styled Component 의 정의는 리턴문 밖에서 이루어져야 한다.**

만약 Styled Component 가 리턴문 안에 정의되면 리렌더링 될 때마다 스타일 속성을 지닌 컴포넌트가 매번 새로 정의되고, 이는 렌더링 속도 저하에 큰 영향을 끼친다.

‣ Adapting based on props & Extending Styles: 스타일 속성을 지닌 컴포넌트를 정의할 때에 함수를 전달하고 그 함수 안에서 props 를 사용할 수도 있다.

ex) Button 컴포넌트의 background 와 color 속성은 primary라는 props의 전달 여부에 따라 컬러값을 정의하고 있다.

```js
// Button component
...
  background: ${(props) => (props.primary ? "palevioletred" : "white")};
  color: ${(props) => (props.primary ? "white" : "palevioletred")};
...

// App component
...
  <Button>Normal</Button>
  <Button primary>Primary</Button>
...
```

또한 같은 스타일 속성을 지닌 여러개의 컴포넌트들 중 몇 개의 컴포넌트에는 약간의 변화를 주고 싶은 경우도 있다.

그런 경우 상속받고자 하는 스타일 속성을 지닌 컴포넌트를 styled() 로 감싼 뒤, 변경하고 싶은 속성만 새로 정의해 주면 기존 속성을 확장하여 사용할 수 있다.

```js
// 기존의 Button 컴포넌트에 Tomato 컴포넌트만을 위한 새로운 속성 추가
const Tomato = styled(Button)`
  color: tomato;
  border-color: tomato;
`;
```

<mark style='background-color: #ffdce0'>✷ 컴포넌트 정의 시 상황(새로운 컴포넌트 생성 혹은 기존 컴포넌트 상속)에 따라 . 온점이나 () 중 하나만 사용할 것.</mark>

‣ Styled Component와 React Component

→ <mark>Styled Component는 앞에 Styled 접두사를 꼭 붙여준다.</mark>

이를 통해 React Component와 Styled Component가 컴포넌트 이름으로 인해 서로 충돌하지 않고 React Developer Tools 및 Web Inspector 에서 쉽게 구분될 수 있다.

ex)

```js
import React from "react";
import styled from "styled-components";

const StyledCounter = styled.div`
  /* ... */
`;
const Paragraph = styled.p`
  /* ... */
`;
const Button = styled.button`
  /* ... */
`;

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };
  const decrement = () => {
    setCount(count - 1);
  };

  return (
    <StyledCounter>
      <Paragraph>{count}</Paragraph>
      <Button onClick={increment}>+</Button>
      <Button onClick={decrement}>-</Button>
    </StyledCounter>
  );
}

export default Counter;
```

‣ Passed props

컴포넌트에 props로 스타일 속성이 전달된다면 해당 컴포넌트는 props 로 전달된 속성을 우선 적용, 전달되는 속성이 없다면 기본으로 설정된 속성을 적용한다.

Styled Component가 개발자에 의해 설정된 속성과 기본 속성을 구분할 수 있기 때문이다.

ex)

```js
import styled from "styled-components";

// Styled Component로 만들어진 Input 컴포넌트
const Input = styled.input`
  padding: 0.5em;
  margin: 0.5em;
  color: ${(props) => props.inputColor || "red"};
  background: papayawhip;
  border: none;
  border-radius: 3px;
`;

export default function App() {
  return (
    <div>
      {/* 아래 Input 컴포넌트는 styled component인 Input 컴포넌트에 지정된 inputColor(red)가 적용됨  */}
      <Input defaultValue="Haley" type="text" />

      {/* 아래 Input 컴포넌트는 props로 전달된 커스텀 inputColor(blue)가 적용됨 */}
      <Input defaultValue="Emily" type="text" inputColor="blue" />
    </div>
  );
}
```

## 5. DOM Reference 활용을 위한 useRef Hook

[useRef로 특정 DOM 선택하기](https://react.vlpt.us/basic/10-useRef.html)

[useRef로 컴포넌트 안의 변수 만들기](https://react.vlpt.us/basic/12-variable-with-useRef.html)

[useRef란?](https://devrappers.tistory.com/55)

[useRef 공식문서](https://ko.reactjs.org/docs/refs-and-the-dom.html)

→ React로 모든 개발 요구 사항을 충족할 수는 없다. React는 예외적인 상황에서 useRef으로 DOM 노드, 엘리먼트, 리액트 컴포넌트 주소값을 참조할 수 있다.

ex) DOM 엘리먼트의 주소값을 활용해야 하는 경우

```
‣ focus
‣ text selection
‣ media playback
‣ 에니메이션 적용
‣ d3.js, greensock 등 DOM 기반 라이브러리 활용
```

✷ useRef는 단순히 DOM 변경뿐만 아니라 데이터의 저장 용도로도 사용한다.

함수형 컴포넌트의 경우 class-based 컴포넌트와는 다르게 데이터를 저장할 방법이 없기 때문에 useRef를 사용한다.

ex) state가 변경되기 이전의 state값을 기억하기를 원한다면 useRef를 이용해 저장하는 방식.

✷ chart.js 라이브러리 / DOM 애니메이션

→ 엘리먼트를 외부에서 접근해서 조작해야 하는 상황이 있다. 외부적으로 접근해서 사용할 수 있는 방법이 없기 때문에 useRef가 생겼다.

ex) 주소값 활용의 예시 틀

```js
const 주소값을_담는_그릇 = useRef(참조자료형);

// 이제 주소값을_담는_그릇 변수에 어떤 주소값이든 담을 수 있다.
return (
  <div>
    <input ref={주소값을_담는_그릇} type="text" />
    {/* React에서 사용 가능한 ref라는 속성에 주소값을_담는_그릇을 값으로 할당하면*/}
    {/* 주소값을_담는_그릇 변수에는 input DOM 엘리먼트의 주소가 담긴다. */}
    {/* 향후 다른 컴포넌트에서 input DOM 엘리먼트를 활용할 수 있다. */}
  </div>
);
```

→ <mark>이 주소값은 리렌더링 되어도 변하지 않는다.</mark> 이런 특징을 활용하여 제한된 상황에서의 useRef를 사용할 수 있다.

ex)

```js
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  // null을 쓰는 이유
  // js 관련 = react js 라이브러리
  // useRef는 배열, 객체, 함수 등의 참조자료형이 들어가는데
  // null = 객체 타입으로 인식(js의 초기 버그 / 이미 수많은 코드들이 기존에 이렇게 사용했기 때문에 고칠 수 없음)
  // 보통 useRef에 null을 자주 사용한다

  // null이 아닌 다른 것이 들어가는 경우
  // 참조하고자 하는 변수의 형태가 배열이거나 객체 혹은 함수인 경우

  // useRef는 남용하면 안된다(=== 쓰지 않으면 개발이 되지 않을 것 같을 때, 써야할 때만 써야한다)

  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

✷ (제시된 예시 제외) **대부분의 경우 기본 리액트 문법을 벗어나 useRef를 남용하는 것은 부적절**하고, React의 특징이자 장점인 선언적 프로그래밍 원칙과 배치되기 때문에 useRef 사용 시 조심해야함.

✷ useRef는 참조자료형을 초기값으로 받아와야 하는데 이 참조자료형에는 배열, 객체, 함수가 있다.

<mark>자바스크립트는 null을 객체 타입으로 인식하기 때문에 useRef(null)을 쓰는 것은 틀린 것이 아니다. 암묵적 동의.</mark>

```js
// 타자치기 연습 예제
import React, { useRef } from "react";

const Focus = () => {
  const firstRef = useRef(null);
  const secondRef = useRef(null);
  const thirdRef = useRef(null);

  const handleInput = (event) => {
    // console.log(event.key, event);
    if (event.key === "Enter") {
      if (event.target === firstRef.current) {
        secondRef.current.focus();
        event.target.value = "";
      } else if (event.target === secondRef.current) {
        thirdRef.current.focus();
        event.target.value = "";
      } else if (event.target === thirdRef.current) {
        firstRef.current.focus();
        event.target.value = "";
      } else {
        return;
      }
    }
  };

  return (
    <div>
      <h1>타자연습</h1>
      <h3>각 단어를 바르게 입력하고 엔터를 누르세요.</h3>
      <div>
        <label>hello </label>
        <input ref={firstRef} onKeyUp={handleInput} />
      </div>
      <div>
        <label>world </label>
        <input ref={secondRef} onKeyUp={handleInput} />
      </div>
      <div>
        <label>codestates </label>
        <input ref={thirdRef} onKeyUp={handleInput} />
      </div>
    </div>
  );
};

export default Focus;
```

```js
// 애니메이션 영상 재생 예제
import { useRef } from "react";

export default function App() {
  const videoRef = useRef(null);

  const playVideo = () => {
    videoRef.current.play();
    console.log(videoRef.current);
  };

  const pauseVideo = () => {
    videoRef.current.pause();

    // 주석처리 된 코드를 주석해제하면
    // pause버튼을 눌렀을 때 일시정지와 동시에 영상이 제거된다
    // videoRef.current.remove();
  };

  return (
    <div className="App">
      <div>
        <button onClick={playVideo}>Play</button>
        <button onClick={pauseVideo}>Pause</button>
      </div>
      <video ref={videoRef} width="320" height="240" controls>
        <source
          type="video/mp4"
          src="https://player.vimeo.com/external/544643152.sd.mp4?s=7dbf132a4774254dde51f4f9baabbd92f6941282&profile_id=165"
        />
      </video>
    </div>
  );
}
```

## 6. UI 컴포넌트의 필요성

### ① UI 개발이 까다로운 이유

프로젝트의 상황에서 절대적으로 많은 수의 화면과 복잡한 화면이 문제가 된다.

![](https://blog.kakaocdn.net/dn/n2fTr/btrpykgG56l/KU9h9DBXJMnjoidCRKoDrK/img.png)

(프로젝트 내부에서 자주 사용되는 UI들의 모음 / 출처: 코드스테이츠)

화면이 복잡하고 다양해도 기본적인 레이아웃 구성 내부에서 사용되는 UI들은 반복적으로 재사용되는 경우가 많다.

UI 컴포넌트를 도입함으로서 **절대적인 코드량을 줄일 수 있고,** 화면이 절대적으로 많고 복잡도가 있는 프로젝트에서 **개발 기간 단축에 절대적으로 기여할 수 있는 장점이 있다.**

⇒ UI들은 다양한 유저 경험 제공을 위해 수백 개의 모듈식 UI 컴포넌트가 재배열된 구조로 이루어져 있음.

### ② 디자인 시스템

‣ 서비스를 만드는 데 사용한 공통 컬러, 서체, 인터랙션, 각종 정책 및 규정에 관한 모든 컴포넌트를 정리해놓은 것, **불필요한 커뮤니케이션을 없애기 위해 체계적으로 정리한 시스템.**

‣ 디자인과 개발 두 분야를 연결하는 다리 역할(= 디자이너와 개발자 모두 UI 컴포넌트를 다루기 때문에).

→ 회사들은 시간과 비용 절약을 위해 UI 패턴 재사용 방식을 도입한다.

→ UI 컴포넌트는 유저 인터페이스(UI)를 이루는 조각들의 시각적 / 기능적 속성을 캡슐화한다.

→ 재사용 가능한 UI 컴포넌트들로 이루어져 있음

⇒ 복잡하고 견고하며 유저가 접근하기 용이한 UI 구축 가능.

### ✷ 빌드 컴포넌트

📚 [스토리북(Storybook)](http://storybook.js.org/): UI 컴포넌트 개발과 자동으로 문서를 생성할 때 사용한다.

⚛️ [리액트(React)](https://reactjs.org/): 선언 중심 컴포넌트 UI(create-react-app)를 사용한다.

💅 [스타일 컴포넌트(Styled-components)](https://www.styled-components.com/): 컴포넌트 단위의 스타일링에 사용한다.

✨ [프리티어(Prettier)](https://prettier.io/): 자동화된 코드 포맷팅에 사용한다.

## 모달(Modal UI Component)

[✷ 모달(Modal UI Component)](http://design.gabia.com/wordpress/?p=33075)

→ 이목을 집중해야 하는 화면을 다른 화면 위로 띄워(Presenting) 표현하는 방식.

→ 모달로 보이는 화면을 사라지게 하려면 반드시 특정 선택을 해야한다.

→ 되도록 단순하고 유저가 빠르게 처리할 수 있는 내용을 표현한다.

[⇒ 모달 화면의 예시](https://material.io/components/dialogs#usage)

모달창의 배경에서 z-index에 999'의 숫자(줄 수 있는 최대한 큰 숫자)를 주는 이유는 모달창은 모든 페이지의 컨텐츠 위에 불투명한 검은 뷰가 깔려야 하고, 그 위로 대화 상자가 보여야 하기 때문이다.

⇒ 숫자를 가장 크게 가져야만이 모달창의 백드롭(검은 부분)이 제일 위로 올라옴.

## ✅ 리액트의 조건문에 대하여

[참고링크](https://velog.io/@zero_mountain/React-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%A1%B0%EA%B1%B4%EB%AC%B8)

[✷ `](https://polaris.shopify.com/components/forms/autocomplete#navigation)

[✷ attr메소드](https://www.codingfactory.net/10208)

[✷ role: dialog;](https://velog.io/@wow/role-%EC%86%8D%EC%84%B1)

[✷ Event.stopPropagation()](https://developer.mozilla.org/ko/docs/Web/API/Event/stopPropagation)

[✷ CSS flex-wrap](https://developer.mozilla.org/ko/docs/Web/CSS/flex-wrap)
