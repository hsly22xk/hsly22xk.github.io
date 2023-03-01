---
layout: single
title: "[CSS] flex: 1;"
categories: React
tag: [기록, 리액트, react, css]
author_profile: false
---

CSS flex 속성에 관하여.

## 개요

[(참고링크1)](https://hsly22xk.tistory.com/26)

[(참고링크2)](https://studiomeal.com/archives/197)

예전에 부트캠프에서 CSS flex를 학습할 때도 언급되었던 내용이었지만, 정확하게 어떤 의미인지 잘 알지 못한 채 넘어갔고, 그러다보니 제대로 활용할 수 없었다.

이번에는 뭔지 제대로 알고 넘어가기 위해 찾아보고 정리한 내용들을 글로 작성하게 되었다.

## flex 속성

flex의 세 속성을 한 번에 작성하기 위한 단축 표현이다.

세 속성은 각각 flex-grow, flex-shrink, flex-basis다.

각각의 의미는 이렇게 정리해볼 수 있다.

> flex-grow
>
> • flex-basis(flex item의 기본 크기)보다 늘어날 수 있는지 결정하는 속성
>
> • 디폴트 값은 0, inflexible한 상태를 의미 (= 화면이나 플렉스 컨테이너의 너비 변경과 상관 없이 원래의 크기 유지)
>
> • 숫자의 의미: flex-basis를 제외한 나머지 여백을 해당 비율로 나눠 갖겠다
>
> • flex-grow 속성의 값으로 1 이상의 숫자가 오게 되면, 화면의 넓이에 따라 유동적으로 변화 = flexible

> flex-shrink
>
> • flex-basis(flex item의 기본 크기)보다 줄어들 수 있는지 결정하는 속성
>
> • <mark>디폴트 값은 1로, 1 이상의 속성 값이 주어지면 해당 비율로 줄어들 수 있음을 의미 = flexible</mark>
>
> • <mark>값으로 0이 온다면, flex-basis보다 줄어들지 않으므로 고정 너비를 설정할 수 있다 = inflexible</mark>

> flex-basis
>
> • flex item의 기본 크기
>
> • 디폴트 값은 auto = 컨텐츠의 너비만큼을 의미
>
> • flex-direction이 row일 때는 너비, column일 때는 높이를 의미
> • 단위로는 px, %, rem 등 모든 단위 사용 가능

## flex: 1;의 의미

```css
flex-grow: 1;
flex-shrink: 1;
flex-basis: 0%;
```

flex-basis가 0이므로 점유 크기를 0으로 만든 후 화면 비율에 따라 유연하게 늘어나거나 줄어들 수 있음을 만드는 속성이다.
