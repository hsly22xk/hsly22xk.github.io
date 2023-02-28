---
layout: single
title: "[React] 리액트 절대 경로 지정하기"
categories: React
tag: [기록, 리액트, react]
author_profile: false
---

리액트의 상대경로와 절대경로, 그리고 절대경로 지정하기.

## 개요

프로젝트를 진행하면서, 그리고 현재 리액트로 개발을 하면서 상대 경로와 절대 경로의 사이에서 고민을 많이 했다.

상대 경로를 지정할 때 가끔 리액트에서 경로를 읽지 못하는 경우도 있고, 현재 작성하는 기능에서 멀리 있는 컴포넌트 혹은 페이지를 import를 할 때마다 번거롭고 가독성이 자꾸 나빠졌다.

```
ex)
// 상대경로
import Page from '../../components/Page';

// 절대경로
import Page from 'components/Page';
```

상대 경로가 무조건적으로 좋지 않다, 절대 경로만 좋다는 의미로 작성하는 글은 아니지만 이론상으로는 속도도 빠르다고 하며, 경로 수정이 용이한 점 때문에 절대 경로의 장점이 더 극대화되어 체감이 된다.

## 절대경로를 지정하는 방법

나는 jsonconfig.json을 사용했다.

현재 나는 js를 사용하고 있기 때문에 jsconfig.json 파일을 루트 디렉토리에 만들었다(타입스크립트는 tsconfig.json).

```json
{
  "compilerOptions": {
    // 루트 디렉토리가 src
    "baseUrl": "src"
  },
  // import할 때 해당 루트의 포함 여부
  // include에 src를 포함하면 'components/Page'
  // include에 src를 포함하지 않으면 'src/components/Page'
  "include": ["src"]
}
```

리액트를 이용하면 src 폴더 하단에 대부분의 폴더들이 존재한다(내가 기능 작성하면서 src 폴더 외부에 무언가를 만드는 것은 조금 불편하게 느껴짐).

그래서 위의 방법대로 했을 때 절대경로로 컴포넌트가 불러와지는 것을 확인할 수 있었다.

[reference(1)](https://mingeesuh.tistory.com/8)

[reference(2)](https://dubaiyu.tistory.com/271)
