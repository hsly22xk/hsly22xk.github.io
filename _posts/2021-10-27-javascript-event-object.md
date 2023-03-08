---
layout: single
title: "D+22 이벤트 객체"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

이벤트 객체 관련 정리 내용

## 1. 이벤트 객체

사용자 입력(onclick, onkeyup, onscroll 등)을 트리거로 발생한 이벤트 정보를 담은 객체.

ex) 이벤트 객체를 설명하기 위한 html파일 예시

![](https://blog.kakaocdn.net/dn/bcPejM/btriTwnUZ1w/CLnMi3KDNA0xoXq1kDBack/img.png)

버튼의 이벤트 핸들러가 동일한 함수에 의해 동작한다.

✷ 이벤트 핸들러: 이벤트가 발생했을 때 그 처리를 담당하는 함수

어떤 메뉴가 추가되더라도 하나의 함수를 추가하여 작성하면 함수 재사용이 가능하다.

사용자가 버튼을 클릭하면 그 버튼의 textContent(혹은 innerHTML)를 이용해 해당 요소의 정보를 가져올 수 있다.

![](https://blog.kakaocdn.net/dn/Sz3mm/btri0curUu8/tFQUqycG9lKfEjNj14oLbk/img.png)

(개발자 도구 콘솔창에 직접 실행해본 결과)

모든 이벤트 객체는 **이벤트의 타입을 나타내는 type속성과 이벤트의 대상을 나타내는 target속성을 가진다.** 이러한 이벤트 객체는 이벤트 리스너가 호출할 때 인수로 전달된다.

## 2. 이벤트 리스너

DOM 객체에서 이벤트가 발생할 경우 해당 이벤트 처리 핸들러를 추가할 수 있는 오브젝트로, 이러한 이벤트 리스너를 등록하고 삭제할 수 있다.

① addEventListener

기본구문 // DOM객체. addEventListener(이벤트명, 실행할 함수명, 옵션)

ex)

```html
<script>
  const button = document.querySelector("button");
  button.addEventListener("click", showConsole);
  function showConscole() {
    console.log("콘솔로그 실행");
  }
</script>
```

이렇게 이벤트 리스너를 등록하면 사용자 이벤트마다 특정 코드를 실행하는 것이 가능하다.

이벤트 리스너를 이용할 경우 특정 스크롤 이벤트 발생 시 이벤트를 실행, input 태그에 글자 수를 확인하는 등의 코드로도 활용이 가능하다.

② removeEventListenr

더 이상 해당 이벤트 리스너가 필요 없으면 추가된 이벤트 리스너는 반드시 삭제해준다.

특정 페이지에서만 사용하는 이벤트 리스너일 경우, 해당 페이지를 떠날 때 이벤트 리스너를 삭제해준다.

기본구문 // DOM객체.removeEventListener(이벤트명, 실행했던 함수명);

ex)

```html
<script>
  export default {
    ...mounted() { // 해당 페이지가 렌더링 되었을 때 실행됨
      button.addEventListener('click', this.showConsole);
    },
    beforeDestroy() { // 페이지를 떠나기 전에 실행되는 코드
      button.removeEventListener('click', this.showConsole);
    },
    ...
  }
</script>
```

[이벤트 리스너에 관한 참고 링크](https://www.zerocho.com/category/JavaScript/post/57432d2aa48729787807c3fc)

[브라우저 이벤트 소개](https://ko.javascript.info/introduction-browser-events)

[event.stopPropagation();](https://developer.mozilla.org/ko/docs/Web/API/Event/stopPropagation)

현재 이벤트가 캡처링/버블링 단계에서 더 이상 전파되지 않도록 방지한다. 전파를 방지해도 이벤트의 기본 동작은 실행함.
