---
layout: single
title: "[React] 리액트로 체크박스/카테고리 선택 및 해제 기능 구현"
categories: React
tag: [기록, 리액트, react, 체크박스, 카테고리]
author_profile: false
---

## 체크박스 구현

1. 체크박스를 선택하면 해당하는 값이 체크됨

2. 해제하면 해당 값을 삭제하는 것처럼 보이게 하기

## 카테고리

1. 카테고리 지정이 아예 되어있지 않을 때는 '지정해주세요' 등의 메시지를 출력시키기

→ 지정 여부에 따른 조건부 렌더링 작성?

## 구현 과정

체크박스의 내용에 대한 리스팅을 위한 상수 데이터 만들기(배열 형태로 / 데이터 내용은 임의로 만듦)

‣ 실제 데이터를 이 내용으로 사용하지는 않았지만, 글 정리를 위해 내용을 바꿈.

```javascript
const category = [
  { id: 0, data: "a" },
  { id: 1, data: "b" },
];
```

상수 데이터는 렌더링 될 때마다 불러올 필요 없으니 함수 바깥으로 빼기

```javascript
const category = [
{id: 0, data: 'a'},
{id: 1, data: 'b'},
];

const function = () => {

...

return (
<>
...
</>
)
}
```

데이터를 저장할 빈 배열을 초기값으로 잡고, useState를 활용한 상태 관리

```javascript
const category = [
{id: 0, data: 'a'},
{id: 1, data: 'b'},
];

const function = () => {
const [checked, setChecked] = useState([]);

    ...

return (
<>
...
</>
)
}
```

체크박스가 체크되는 이벤트 함수와 체크 해제되는 이벤트 함수 작성

‣ onChange 이벤트로 체크박스 이벤트를 감지한다. → 체크되면 데이터 저장, 해제되면 filter함수로 데이터를 삭제

‣ 선택하지 않을 경우 선택해주세요 등의 메시지를 출력시킴. 이 때는 빈 배열일 경우 길이가 0이기 때문에 checked 배열의 길이를 이용.
