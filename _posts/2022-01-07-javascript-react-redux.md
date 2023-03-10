---
layout: single
title: "D+46(47, 48) React 상태 관리, Redux"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

리액트의 상태 관리.

## 1. 프론트엔드 개발에서의 상태 관리(State Management)

① state(상태): 동적인(변하는) 데이터. UI에서 동적으로 표현될 데이터. ⇒ class component 내에서 관리함

② Side Effect: 함수의 입력 외에도 함수의 결과에 영향을 미치는 요인. 대표적으로 네트워크 요청, API 호출이 있다.

⇒ side effect를 최대한 배제하고 컴포넌트를 구성하더라도, 불가피한 경우가 있다.

⇒ 로딩 중을 나타낼 것인지 아닌지에 대한 여부는 데이터 전송 여부에 따라 다르다. 앱을 만들고, UI를 구성할 때에는 항상 이러한 로딩 중 상태를 고려한다.

③ 상태의 적절한 위치

‣ 상태의 두 가지 구분

→ 로컬 상태: 특정 컴포넌트 안에서만 관리되는 상태. 컴포넌트 내에서만 영향을 끼치는 상태.

다른 컴포넌트와 데이터를 공유하지 않는 폼(form)데이터(=radio button)는 대부분 로컬 상태이다. input box, select box 등과 같이 입력값을 받는 경우가 이에 해당한다.

→ 전역 상태: 다른 컴포넌트와 상태를 공유하고 영향을 끼치는 상태. 프로덕트 전체 혹은 여러가지 컴포넌트가 동시에 관리하는 상태.

데이터 로딩 여부(로딩중) 상태도 앱 전반에 영향을 미친다.

✷ 전역 변수의 남용은 좋지 않지만, 경우에 따라 전역 상태가 필요하다.

‣ 전역 상태가 필요한 경우

- 라이트 / 다크모드 설정

→ 모든 페이지, 모든 컴포넌트에 다크 모드 혹은 라이트 모드가 적용이 되어야 하기 때문에 이러한 테마 설정을 전역으로 관리할 수 있다.

- 국제화(Globalization) 설정

→ 사용자가 사용하는 브라우저나, 운영체제가 특정 언어를 사용하고 있음을 알아내어 UI에 필요한 텍스트 리소스를 따로 저장한 후, 전역 상태로 관리하기도 한다.

⇒ 모든 컴포넌트에서 사용자 언어로 표현이 되어야 하기 때문에 전역에서 상태 관리 필요

✷ 형제 컴포넌트끼리 데이터를 주고 받을 때 부모 컴포넌트를 통해서 주고 받는다.

→ 자식 컴포넌트들끼리의 데이터를 주고 받는 것은 불가능하다.

→ 이러한 자식 컴포넌트들이 더 많아진다면 상태 관리가 복잡하다.

![](https://blog.kakaocdn.net/dn/bMoE7a/btrp002ivs2/oSqKs0cq26D62wsrBrtwHk/img.png)

⇒ 이런 복잡한 상태 관리를 위해 상태 관리 라이브러리인 리덕스가 나왔다.

## 2. Redux(리덕스)

[리덕스1](https://bestalign.github.io/translation/cartoon-intro-to-redux/)
[리덕스2](https://13akstjq.github.io/redux/2019/12/14/redux-redux%EC%99%84%EB%B2%BD%EC%A0%95%EB%A6%AC.html)

→ 자바스크립트에서 예측 가능한 상태 관리를 해주는 라이브러리. Flux를 개선한 아키텍쳐.

핫 리로딩(Hot Reloading)과 시간여행 디버깅(Time-travel debugging)을 지원하는 개발자 도구가 구현되어있다.Flux와 비슷하지만 리듀서(Reducer)를 추가해서 상태 변경의 개념 자체를 바꿔버렸다.

[✷ Flux는 무엇인가?](https://baeharam.netlify.app/posts/architecture/flux-redux)

‣ Flux: 단방향 데이터 흐름으로 만들어낸 아키텍쳐.

⇒ Flux pattern

Action → Dispatcher → Store → View

### ① 상태 관리 라이브러리가 필요한 이유

‣ 전역 상태를 위한 저장소(store)를 제공

‣ Props drilling(프로퍼티 내려꽂기)이슈 해결 ⇒ 전역 상태 저장소가 있고, 어디서든 해당 저장소에 접근할 수 있다면 이러한 문제는 해결될 것이다.

![](https://blog.kakaocdn.net/dn/W50hf/btrpLsTDSWF/7KGdoRHAlxAwdmnmYVVUS0/img.png)

✷ Props drilling(프로퍼티 내려꽂기): 최상위 컴포넌트에 상태가 있고, 가장 아래에 있는 자식 컴포넌트가 해당 상태를 사용할 때 중간에 존재하는 컴포넌트들이 굳이 상태가 필요하지 않아도 props를 만들어 자식 컴포넌트에 넘겨주어야 하는 것.

⇒ 상태 관리 툴이 있어야만 애플리케이션을 만들 수 있는 것은 아니지만, 장단점을 고려하여 사용할 것

### ② 리덕스의 기본 개념(세 가지 원칙)

‣ 한 곳에서만 상태를 저장하고 접근하기(Single Source of truth / Store).

⇒ 데이터 무결성을 위해 동일한 데이터는 항상 같은 곳에서 가져오기.

→ 데이터를 저장하는 store라는 하나뿐인 공간이 있다는 의미이다.

⇒ 서로 다른 컴포넌트가 사용하는 상태의 종류가 다르면, 꼭 전역 상태일 필요가 없고 출처(source)가 달라도 된다.

⇒ 서로 다른 컴포넌트가 동일한 상태를 다룬다면, 이 출처는 오직 한 곳이어야 한다. 사본이 있을 경우 두 데이터는 서로 동기화(sync)하는 과정이 필요한데, 이는 문제를 어렵게 만든다.

✷ 하나의 출처 === 전역 공간

![](https://blog.kakaocdn.net/dn/14hG7/btrrF16C5J5/IRA0TOzL81dekbssgd8AM0/img.png)

✅ Store: 컴포넌트와는 별개인, 상태가 관리되는 오직 하나뿐인 공간. 전역 상태를 담고 있음.

⇒ store라는 별개의 공간 안에서 앱에 필요한 state를 두고 컴포넌트들에서 state 정보가 필요할 때, store에 접근해서 state 정보를 가져올 수 있다.

⇒ createStore 메서드를 활용해 reducer를 연결할 수 있는 방법. createStore와 더불어 다른 리듀서의 조합을 인자로 넣어서 스토어를 생성할 수 있다.

```js
const store = createStore(rootReducer);
```

‣ State is read-only(Action)

⇒ 리액트에서 state를 변경하기 위해 setState를 사용했던 것처럼, 리덕스에서는 state를 변경하기 위해 action이라는 객체를 활용할 수 있다.

✅ action: 자바스크립트 객체. 어떤 액션을 취할 것인지 정의해 놓은 객체.

⇒ store에게 애플리케이션의 데이터를 운반해주는 역할로, 객체 안에 타입을 비롯한 다양한 데이터들이 담긴다.

⇒ 모든 변화를 action을 통해 취하는 것은 앱에서 무슨 일이 일어나는지 직관적으로 알기 쉽게 하는 역할.

ex) action의 형태 예시

```js
// 타입은 무조건 써줘야한다
// 정보를 객체 형태로 써줘야한다
{
  type: "ORDER",
  drink: {
    menu: "Vanilla Latte",
    size: "Tall",
    iced: true
  }
}
```

```js
{
  // ANYTHING,
  type: payload: {
    // Something
  }
}
```

✷ Dispatch: Action을 전달하는 메소드. → dispatch의 전달인자로 Action 객체가 전달된다.

‣ 변경은 순수함수로만 가능하다(Changes are made with pure functions / Reducer)

① 동일한 인자값을 받으면 항상 동일한 값 리턴

② 어디서 호출이 되든 동일한 결과를 보여준다

③ 외부(함수 스코프)에 영향을 받지도 주지도 말아야 한다

✅ Reducer(리듀서)

현재의 state와 Action을 이용해서 새로운 state를 만들어 내는 pure function.

→ store에는 현재의 state가 있고, 그 현재 상태와 action을 이용하여 새로운 state를 만들어낼 수 있다.

→ action을 통해 데이터를 store로 운반하는 과정 중간에 reducer가 있다.

⇒ Reducer를 호출해 state의 값을 바꾸는 역할을 한다.

![](https://blog.kakaocdn.net/dn/bpl0Pa/btrpWzQO1Tw/ZmRrDo45nO4NDy9yaZ3A30/img.png)

**<mark>⇒ 데이터가 한 방향으로만 흘러야 하기 때문에 그림 속 문장의 공식을 따라야만 한다.</mark>**

[Redux 공식문서](https://react-redux.js.org/7.1/api/hooks)

![](https://blog.kakaocdn.net/dn/ldL2a/btrpPw2nRRW/BwCsTM70RdKGeBOkYR61O1/img.png)

⇒ UI에서 + 버튼을 클릭하는 이벤트가 발생하면 Dispatch의 전달인자로 Action 객체를 담아 Reducer로 전달된다.

Reducer는 Action객체의 타입에 따라 다른 동작을 수행하며, 그 수행의 결과로 새로운 state가 반환된다.

### ③ Redux의 장점

‣ 상태를 예측 가능하게 만들어준다.

‣ 테스트를 붙이기 쉽다.

⇒ Reducer는 순수 함수이기 때문에 이런 것들이 가능하다.

‣ 유지 보수에 용이하다. ⇒ 버그가 나타났을 때, props를 내려준 모든 컴포넌트들을 수정할 필요가 없음.

‣ action / state의 log에 기록 시 디버깅에 유리하다. ⇒ action이 생겼을 때 어떤 일이 일어났는지 추적이 가능하고, 크롬 스토어에서 Redux Dev Tools를 설치하면 알아볼 수 있다.

✷ Reducer의 Immutability(불변성)

‣ Redux의 state 업데이트는 immutable한 방식으로 변경해야 한다.

→ 변경된 state를 log로 남기기 위해 '꼭' 필요한 작업.

① shallow equality checking을 위해

② 궁극적으로 데이터 핸들링을 안전하게 만들어 준다

③ 시간여행 디버깅을 위해 리듀서가 순수함수로 만들어져서

사이드 이펙트가 없어야 한다. 그렇게 해야 각각 다른 state간의 이동이 가능하다.

✷ Action, Reducer, Dispatch, Store 개념들을 connect 할 수 있는 방법

‣ mapStateToProps, mapDispatchToProps 등의 메소드

### ④ Redux Hooks

① useSelector(): 컴포넌트와 state를 연결하는 역할. 이 메소드를 통해 컴포넌트에서 store의 state에 접근할 수 있다.

→ useSelector의 전달인자로는 콜백 함수를 받으며, 콜백 함수의 전달인자로는 state 값이 들어간다.

② useDispatch(): Action 객체를 Reducer로 전달해주는 메소드. Action이 일어날 만한 곳은 클릭 등의 이벤트가 일어나는 컴포넌트이다.

✷ [payload](http://melonicedlatte.com/web/2020/01/14/205200.html): 전송되는 데이터.

✷ [payload](https://hanamon.kr/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-http-%ED%8E%98%EC%9D%B4%EB%A1%9C%EB%93%9C-payload%EB%9E%80/)

[✷ switch case 조건문](https://prosto.tistory.com/119)

✷ Redux Dev Tools

① chrome store(크롬 스토어)에서 Redux Dev Tools를 검색한다.

② 프로젝트에

```
① chrome store(크롬 스토어)에서 Redux Dev Tools를 검색한다.
② 프로젝트에
yarn add redux-devtools-extension
명령어를 사용하여 extension을 설치한다.
③ 크롬 개발자 도구에서 Redux를 선택한다.
(혹은 우클릭을 하면 Redux DevTools가 나온다)
```

✷ Presentational Component와 Container Component

|                |    Presentational     |             Container             |
| :------------: | :-------------------: | :-------------------------------: |
|      기능      |   어떻게 보여지는가   |         어떻게 동작하는가         |
| Redux와 연관성 |           X           |                 O                 |
|   Read data    | props에서 data를 읽음 | Redux의 state에 접근(useSelector) |
|  Change data   |  props에서 콜백 호출  |           Redux Action            |

✷ React and Virtual DOM
{% include video id="BYbgopx44vo" provider="youtube" %}
