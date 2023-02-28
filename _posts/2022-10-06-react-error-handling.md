---
layout: single
title: "[React] 리액트 관련 에러 및 핸들링"
categories: Error-Handling-Logs
tag: [기록, 리액트, react, 에러핸들링]
author_profile: false
---

(22.09.28 ~ 22.10.06)

## mui(material ui) 설치 못하는 에러

react-create-app을 선행할 때 리액트 버전이 18로 설치가 되며, material ui는 16 버전부터 적용 가능하다.

→ 해결책

```
npm install --save react@^17.0.2 react-dom@17.0.2 // react, react-dom 버전 낮추기
npm install @material-ui/core --legacy-peer-deps // --legacy-peer-deps 옵션으로 설치
npm install @mui/icons-material --legacy-peer-deps
```

혹은

```
npm install @material-ui/core --force // --force 옵션으로 설치
npm install @mui/icons-material --force
```

--force와 --legacy-peer-deps의 차이는
의존 모듈을 강제 설치하느냐, 아니면 의존 모듈 없이도 일단 설치가 가능하게 하느냐의 차이다.
[(reference1)](https://d-life93.tistory.com/309)

[(reference2)](https://seantech.tistory.com/160)

[(reference3)](https://velog.io/@aneb/MUIError)
리액트 버전을 17.0.2로 다운그레이드한 이유는 단순히 그 버전으로 했을 때 에러가 나오지 않았기 때문에...

16 버전으로 낮추었을 때는 18 버전과 같은 에러 메시지가 출력되었다.

## react-dom/client 모듈을 찾을 수 없습니다

```
Module not found: Error: Can't resolve 'react-dom/client'
```

react-dom/client는 리액트 18 버전에 맞추어 나온 것이기 때문에,

앞에서 이미 버전을 17.0.2로 낮추었기 때문에 나온 에러였다.

index.js에서 버전에 맞게 코드를 수정해주어 해결했다.

```
// react v18 버전용
// import ReactDOM from 'react-dom/client';
import ReactDOM from 'react-dom'; // react v17 버전용

// react v18 버전용
// const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);
// root.render(
// <React.StrictMode>
// <App />
// </React.StrictMode>
// );

// react v17 버전용
ReactDOM.render(
<React.StrictMode>
<App />
</React.StrictMode>,
document.getElementById('root')
);
```

[(reference3)](https://curryyou.tistory.com/468)

## React 사용하여 클라이언트 실행 시 콘솔에 값이 두 번씩 찍히는 경우

에러 상황은 아니지만 왜 두 번씩 찍히는 지에 대해 궁금해서 구글링 후 정리해봤다.

index.js에 App 컴포넌트를 React.StrictMode가 감싸고 있을경우 개발 오류를 잡기위해 두 번씩 렌더링 된다.

```
// index.js
// 원래 코드
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
<React.StrictMode>
<App />
</React.StrictMode>
);

// 수정 코드
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

## 파싱 에러

```
Parsing error: 'import' and 'export' may only appear at the top level.
```

기능을 작성하다가 갑자기 export default 부분에서 에러가 발생했다.

이유는 기능을 작성하면서 } 를 하나 빠뜨렸기 때문이었다...닫는 중괄호를 하나 빠뜨려서 이하 함수들이 내부 함수가 되었다.

최하단까지 도달하여 export default 키워드가 등장했는데 닫침 괄호가 없어서 export default가 함수 내부에 위치한 것. 그래서 에러 메시지가 출력되었던 것이다.

닫는 중괄호를 추가해서 해결되었다.

[(reference)](https://velog.io/@hwang-eunji/Syntax-error-import-and-export-may-only-appear-at-the-top-level)

## 리액트 버전 문제

[(reference)](https://velog.io/@citron03/React-18%EC%97%90%EC%84%9C-ReactDOM.render%EC%99%80-createRoot)

```
Warning: ReactDOM.render is no longer supported in React 18. Use createRoot instead. Until you switch to the new API, your app will behave as if it's running React 17. Learn more: https://reactjs.org/link/switch-to-createroot
```

이 경고 문구는 ReactDOM은 18버전의 리액트에서 지원하지 않으며 createRoot를 써야한다는 문구였다.

그런데 분명 나는 17.0.2버전으로 바꾼 것 같은데...갑자기 이 경고 메시지가 왜 뜰까 하는 의문이 들었다.

package.json을 확인해보니 18버전이었다(?)

분명 바꿨는데...리액트 버전을 바꿔주는 것은 어렵지 않으니 바로 react와 react-dom의 버전을 바꿔주었다.

```
npm install react@17.0.2 react-dom@17.0.2
```

아래는 18버전을 쓸 때 index.js 코드를 어떻게 바꿔주어야 하는 지에 대해서 작성했다.
[(reference)](https://dev.to/osmanforhad/react-js-warning-reactdomrender-is-no-longer-supported-in-react-18-use-createroot-instead-until-you-switch-to-the-new-api-1jhh)

```
// 리액트 17버전 코드
import React from 'react';
import ReactDOM from 'react-dom';
import 'index.css';
import App from 'App';
import reportWebVitals from 'reportWebVitals';

ReactDOM.render(
<React.StrictMode>
<App />
</React.StrictMode>,
document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

// 리액트 18버전 코드
import React from "react";
import ReactDOM from "react-dom/client";
import "index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

## 리액트 컴포넌트 이름 관련 에러

```
React Hook "useParams" is called in function "a" that is neither a React function component nor a custom React Hook function. React component names must start with an uppercase letter. React Hook names must start with the word "use"
```

갑자기 왜 이런 에러가 나오는가 싶어 에러 메시지를 해석해보던 중에 React component names must start with an uppercase letter. 라는 문장이 눈에 띄었다. '리액트 컴포넌트의 이름은 무조건 대문자로 시작해야한다.'

코드를 살펴보니 export한 함수의 이름의 시작이 소문자다. 대문자로 고쳐주니 해결되었다.
