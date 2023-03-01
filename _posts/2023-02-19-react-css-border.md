---
layout: single
title: "[CSS] 밑줄과 밑줄의 길이를 변경하고 싶을 때"
categories: React
tag: [기록, 리액트, react, css]
author_profile: false
---

CSS의 border 속성에 관하여.

## 개요

항상 Header와 Footer를 구분 지을 때는 색상으로 구분을 지었었는데, 생각해 보면 항상 그렇게 해야만 구분을 지을 수 있었던 것은 아니었다.

그래서 밑줄(이라는 표현이 맞는지는 모르겠지만)을 그어 Header와 Sidebar, Footer를 구분짓고 길이를 조절할 수 있는 방법에 대해 찾아보기로 했다.

## border 속성

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/border-bottom)을 찾아보면서, border 속성으로 할 수 있다는 것을 알게 되었다.

단순 border속성은 테두리를 지정할 수 있는 속성이지만 top, bottom, left, right의 위치를 지정해 줌에 따라 내가 원하는 대로 줄을 지정할 수 있다.

```css
.classNameOne {
  ...
  border-bottom: thick double #32a1ce;
}
```

이렇게 순서를 맞추어 줄의 두께, 종류, 색깔까지 지정해줄 수 있다.

만약 위치를 조정해주고 싶을 때는 margin과 padding을 이용하여 원하는 곳으로 위치시킬 수 있다.

```css
.classNameTwo {
  ...
  margin: 80px 0px;
  padding: 30px;
  border-right: 1px solid black;
  ...
}
```

상기 코드와 같이 margin과 padding 속성을 이용하여 위치시킬 수 있다.

(조금 더 자세한 내용은 이 [링크](https://www.codingfactory.net/10778)를 참조했다)

(border-bottom에 대한 자세한 [링크](https://homzzang.com/b/css-45))
