---
layout: single
title: "D+24 React 초급"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

React 관련 내용 정리(초반부)

## 1. React

프론트엔드 개발을 위한 자바스크립트 오픈 소스 라이브러리.

✷ 프론트엔드: 웹 개발에서 유저에게 보이는 뷰(view)에 대한 코드를 작성하고 개발하는 것

✅ Why React? 리액트의 3가지 특징

① 리액트는 선언형이다

코드를 자세히 분석하지 않고도 코드의 의도를 분명히 작성할 수 있는 방법.

⇒ 리액트는 한 페이지를 보여주기 위해 HTML, CSS, JS를 넘나들지 않고 하나의 파일에 명시적으로 작성할 수 있게 JSX를 활용한 선언형 프로그래밍이다.

✷ JSX: HTML 문법을 JavaScript 코드 내부에 쓴 것. HTML과 JS가 결합한 문법을 기반으로 직관적으로 코드를 작성한다.

⇒ 즉, 코드만 보고도 어떤 모습일지 어떤 기능일지 상상할 수 있는 명시적이고 직관적이다.

② 컴포넌트 기반(component-based)이다

✷ 컴포넌트(component): 하나의 기능 구현을 위해 여러 종류의 코드를 묶어놓은 것. 구조와 동작에 대한 코드를 한 뭉치로 적은 코드셋

리액트는 컴포넌트를 기반으로 개발한다. 컴포넌트로 분리하면 의존성이 없어져서 서로 독립적으로 작동하기 때문에 유닛 테스트를 할 때 유용하다.

이전에 작성된 기능을 구현할 때 해당 컴포넌트의 재사용이 가능하기 때문에 기능 자체에 집중하여 개발할 수 있다.

기능이 작동하지 않을 때 그 기능을 구현한 컴포넌트의 코드를 보고 에러를 찾을 수 있어 유지보수가 편하다.

③ 다양한 곳에서 활용할 수 있다(범용성)

대부분의 프레임워크들은 다른 프레임워크와 같이 사용할 수 없는 구조이다. 해당 생태계에 종속되는 형태.

**<mark>리액트는 라이브러리</mark>**이기 때문에 기존에 개발하던 코드를 전부 뒤엎지 않고 일부만 고칠 수 있어 어디에나 사용할 수 있다.

버그가 적고 유지보수가 잘 되고 있다. 리액트 네이티브로 모바일 개발도 가능하다.

## 2. JSX(JavaScript XML)

React에서 UI를 구성할 때 사용하는 문법으로, 이를 이용해서 React 엘리먼트를 만들 수 있다.

JavaScript를 확장한 문법이긴 하지만 브라우저가 바로 실행할 수 있는 것은 아니다.

브라우저가 이해할 수 있는 자바스크립트 코드로 변환을 해주어야 하는데, 이 때 사용하는 것이 Babel이다.

Babel은 브라우저가 이해할 수 있는 자바스크립트로 컴파일한 후, 브라우저가 읽고 화면에 렌더링 할 수 있다.

⇒ JSX는 HTML 처럼 생긴 거지 HTML 그 자체가 아니기 때문에 컴파일 과정이 필수!

리액트에서는 DOM과 다르게 CSS, JSX 문법만을 가지고 웹 애플리케이션을 개발할 수 있다.

컴포넌트 하나를 구현하기 위해서 필요한 파일이 줄어들었고, 한눈에 컴포넌트를 확인할 수 있게 되었다.

JSX를 사용하면 JavaScript만으로 마크업(markup) 형태의 코드를 작성하여 DOM에 배치할 수 있게 된다.

✷ JSX가 없으면 리액트 요소를 만들 수 없을까? ⇒ 만들 수는 있지만 코드가 복잡하고 가독성이 떨어진다.

## 3. JSX의 활용법과 꼭 알아야할 주요 문법

① 여러 엘리먼트를 작성할 때는 opening tag와 closing tag로 감싸주어야 한다.

ex)

```html
<div>
  <div>
    <h1>Hello</h1>
  </div>
  <div>
    <h2>World</h2>
  </div>
</div>
```

예시처럼 요소가 여러 개 있다면 반드시 부모요소 하나로 감싸주어야 한다.

② CSS class 속성을 지정할 때에는 className으로 표기한다.

그냥 class로 쓰면 html 속성이 아닌 js클래스로 받아들인다. 꼭 Name까지 붙여줄 것!

ex)

```html
<div className="greeting">Hello!</div>
```

③ Javascript 표현식을 쓰고 싶을 때는 꼭 {} 중괄호를 이용한다. 만약 중괄호를 안쓰면 일반 텍스트로 인식한다.

ex)

```js
function A() {
  const name = "Emily Johnson"; // 중괄호를 쓰지 않은 일반 텍스트
  return <div>Hello, {name} // 중괄호를 써서 js표현식을 나타낸 것</div>;
}
```

④ 무조건 대문자로 시작해야 한다. 소문자로 시작하면 일반적인 HTML 엘리먼트로 인식한다.

✷ 사용자 정의 컴포넌트: 이렇게 대문자로 작성된 JSX 컴포넌트

ex)

```js
function Hello() {
  return <div>Hello!</div>;
}

function HelloWorld() {
  return <Hello />;
}

// 전부 앞의 문자인 H를 대문자로 써주었음
```

⑤ 조건부 렌더링은 삼항연산자를 이용한다(jsx내에서 if문을 사용할 수 없음)

✷ 삼항연산자

조건문 ? 선택문1 : 선택문2

⇒ 조건문이 참이면 선택문1을 실행하고, 거짓이면 선택문 2를 실행한다.

ex1)

```js
<div>{1 + 1 === 2 ? <p>정답</p> : <p>탈락</p>}</div>
```

ex2)

```js
<div>{name === "Harvey" ? <p>Yes, I'm Harvey</p> : <p>No, I'm not</p>}</div>
```

⑥ 여러 개의 HTML 엘리먼트를 표시할 때는 map() 함수 이용

map() 함수 사용 시 반드시 'key' JSX 속성을 넣는다. 안 넣으면 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시된다.

key 속성의 위치는 map 메소드 내부에 있는 엘리먼트, 즉 첫 엘리먼트에 넣는다.

ex)

```js
const posts = [
{id: 1, title: "I love coffee", content: "I love tea"},
{id: 2, title: "I need coffee", content: "I need tea"}
];

function AllPostings() {
const content = (post) =>

<div key = {post.id}> // key를 넣어주는 것 중요함
<h3>{post.title}</h3>
<p>{post.content}</p>
</div>
);

const blogs = posts.map(content);
return <div className="post-wrapper">{blogs}</div>
```

이 예시는 블로그 포스팅에 관련된 코드이다. 그런데 지금 예시에서는 2개만 썼지만, 앞으로 쓸 포스팅이 100개가 넘는다면? 1000개가 넘는다면?

그래서 우리는 map()함수를 써준다.

```
현재 posts의 요소는 블로그 포스트의 id, title, content로 나눌 수 있다.
// 배열의 각 요소(post)를 특정 논리(content함수)에 의해 다른 요소로 지정(map)한다.
```

이 말을 코드로 적어놓은 것이 위의 예시이다.

반복적으로 작성해야 하는 부분만 골라서 배열의 요소로 넣으면 React가 이를 인지하고 모든 요소를 렌더링한다.

✷key 속성 값이 반드시 id가 되어야 하는건가? 만약 id가 없다면? key 속성값은 가능하면 데이터에서 제공하는 id를 할당해야 한다.

key 속성값은 id와 마찬가지로 변하지 않고, 예상 가능하며, 유일해야 하기 때문이다. 정 고유한 id가 없는 경우에만 배열 인덱스를 넣어서 해결할 수 있다.

배열 인덱스는 최후의 수단(as a last resort)으로만 사용한다.

## 4. 컴포넌트

![](https://blog.kakaocdn.net/dn/cSFE8O/btr2TBKtxZA/eW1DBQVG8pT9BZfdYu7sHk/img.png)

각자 독립된 기능을 가지며 UI의 한 부분을 담당하기도 하는 컴포넌트를 여러 개 만들고 조합하여 웹 어플리케이션을 만들 수 있다.

이런 컴포넌트들의 관계를 트리 구조로 형상화 하여 표현할 수 있다.

![](https://blog.kakaocdn.net/dn/c4xMPo/btrjd3xrzht/EkGvUgOauEm7UJp1Ml8pBK/img.png)

(계층적 구조(hierarchy)를 트리 구조로 형상화한 것)

모든 리액트 애플리케이션은 최소 한 개의 컴포넌트를 가지고 있으며, 이 컴포넌트는 애플리케이션 내부적으로는 근원(Root)이 되는 역할을 한다.

이 최상위 컴포넌트는 근원의 역할을 하므로 다른 자식 컴포넌트를 가질 수 있다.

그림은 그 트리 구조를 설명하고 있는 것이다.

이것을 좀 더 구체적으로 그려보자면

![](https://blog.kakaocdn.net/dn/bBAHdY/btrmFpSEhCG/gHnw8auzUCEHkCcw1Hf3O0/img.png)

맨 위에 근원이 되는 root component가 있고, 그 아래 header와 content list가 온다.

header는 자신의 아래에 search와 setting같은 자식 컴포넌트를, content list는 각각의 content들을 자식 컴포넌트로 가질 수 있다.

이것으로 보아 각각의 컴포넌트는 각자 고유의 기능을 가지고 있으면서 UI의 한 부분을 담당한다.

이런 독립적인 컴포넌트들을 여러 개 만들고 이들을 한데 모아 복잡한 UI를 구성할 수도 있고, 더 나아가 최종적으로는 복잡한 애플리케이션도 만들 수 있다.

## 5. Create React App

리액트 SPA(Single Page Application)를 쉽고 빠르게 개발할 수 있도록 만들어진 툴 체인.

✷ SPA

한 개의 페이지로 만들어진 웹 어플리케이션.

서버로부터 완전한 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹 애플리케이션이나 웹사이트.

**웹 페이지가 자바스크립트로 인해 렌더링된다.**

이러한 접근은 연속되는 페이지들 간의 사용자 경험의 간섭을 막아주고 애플리케이션이 데스크톱 애플리케이션처럼 동작하도록 만들어준다.

SPA에서 HTML, 자바스크립트, CSS 등 필요한 모든 코드는 하나의 페이지로 불러오거나, 적절한 자원들을 동적으로 불러들여서 필요하면 문서에 추가하는데, 보통 사용자의 동작에 응답하게 되는 방식이다.

✅ 설치 방법

① 터미널을 켠다

‣ git --version, node --version, npm --version을 확인해준다.(버전 확인 후 업데이트가 필요하다면 해준다.)

② 현재 위치를 확인(pwd)해준다.

③ 바탕화면으로 들어간다(cd Desktop).

④ 새 폴더를 만들어준다(mkdir 만들고 싶은 파일명)

⑤ 새 폴더에 들어간다

⑦ npm install create-react-app 프로젝트명

⇒ 설치되는 패키지에는 react, react-dom(react를 실제 브라우저에서 렌더링 할 수 있도록 도와줌), react-scripts(spa구현과 복잡한 모던 프론트엔드 기술이 미리 세팅되어 있음), cra-template(관련된 패키지들)등등이 설치된다.

설치되는 데에는 시간이 조금 걸린다(엄청 오래 걸리지는 않음!)

⑧ Happy hacking! 이라는 멘트가 뜬다면 설치 성공.

(이전에는 npx 명령어를 사용하여 cra를 설치했지만, 현재는 버전 문제로 인해 npx 명령어가 되지 않는다.)
