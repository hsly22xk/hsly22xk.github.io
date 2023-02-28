---
layout: single
title: "[React Library] Confirm Box 만들기"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

리액트 라이브러리를 활용하여 confirm box 만들어보기.

## react-confirm-alert

[(npm 공식문서)](https://www.npmjs.com/package/react-confirm-alert)

confirm box를 어떻게 만들 수 있을까에 대해 고민하며 구글링을 하던 중, react-confirm-alert라는 라이브러리를 알게 되었다.

어떻게 사용하는지에 대해 간략하게 알아본 후 적용시켰고, 결과는 95% 정도 성공인 것 같다.

5%가 빠진 이유는, 같은 페이지에 같은 코드를 삽입함에도 불구하고 기능이 제대로 작동하지 않은 페이지가 있다.

원인을 아직 발견하지 못했지만, 추후 알게 된다면 함께 작성할 예정이다.

```
npm i react-confirm-alert --save
```

```javascript
import { confirmAlert } from 'react-confirm-alert'; // alert 라이브러리 사용을 위한 import
import 'react-confirm-alert/src/react-confirm-alert.css'; // alert css 사용을 위한 import

onClick={() =>
  confirmAlert({
    message: 'Are you sure?',
    buttons: [
      {
        label: 'yes',
        onClick: () => yes에 해당하는 클릭 이벤트 삽입
      },
      {
        label: 'no',
        onClick: () => no에 해당하는 클릭 이벤트 삽입
      },
    ],
  })
}
```

## sweetalert2

[(sweetalert2 reference1)](https://sweetalert2.github.io/#usage)

[(sweetalert2 reference2)](https://inpa.tistory.com/entry/SweetAlert2-%F0%9F%93%9A-%EC%84%A4%EC%B9%98-%EC%82%AC%EC%9A%A9#SweetAlert2_%EC%82%AC%EC%9A%A9%EB%B2%95)

1번에서 작성했던 alert library는 간단하게 사용하기에는 제일 좋았으나, 내가 아직 몰라서 그런 것인지 css파일에서 css 변경을 원하는 대로 할 수 없었다.

그래서 조금 더 검색해본 결과 sweetalert2가 나왔다.

사용방법을 조금 더 검색해보자 실사용예제를 정리해둔 블로그 글을 발견할 수 있었다.

```
// 설치 및 사용 방법
npm i sweetalert2 --save
import Swal from 'sweetalert2';
```

react-confirm-alert보다는 확실히 css를 적용하기 쉬웠고, 기능의 종류도 다양했다.

하지만 조금 삽질(?)해야했던 경우가 있었는데, 유효성 체크를 할 때 그 상황에 맞는 alert를 띄워주고 싶었는데 제대로 되지 않았다.

```javascript
onClick={() => {
  Swal.fire({
    title: 'Are you sure?',
    icon: 'warning',showCancelButton: true,
    confirmButtonColor: '#3085d6', // 버튼 색상 지정
    cancelButtonColor: '#d33', // 버튼 색상 지정
    confirmButtonText: 'Yes',
    cancelButtonText: 'No',
    reverseButtons: false, // 버튼 순서 변경
  }).then((result) => {
    if (text === '') {
      Swal.fire({
        title: 'Warning!',
        text: 'Try again',
        icon: 'warning',
      });
      result.isDenied();
      } else if (result.isConfirmed) {
        onSubmit();
        Swal.fire({
          title: 'You can do it!',
          confirmButtonText: 'Ok',
        });
      } else if (result.isDismissed) {
        handleExit();
      }
    });
  }}
```
