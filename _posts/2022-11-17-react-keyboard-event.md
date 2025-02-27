---
layout: single
title: "[React] 리액트 키보드 이벤트"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

리액트 키보드 이벤트 핸들러에 관한 글.

## 개요

보통 회원가입을 할 때 아이디가 중복되었거나, 혹은 입력하지 않았을 때 값을 입력하라고 나오는 메시지들이 있다.

그런 메시지들이 제대로 된 값을 입력했을 때에는 없어져야하는데, 이 부분을 키보드 이벤트로 구현할 수 있었다.

## onKeyUp()

(onKeyPress 이벤트도 있었으나 현재는 deprecated되어 권장하지 않는다고 한다)

```javascript
import React, { useState } from 'react';

const 내가하고싶은컴포넌트 = () => {
  const [입력값, set입력값] = useState('');
  const [중복메시지, set중복메시지] = useState('');

  const 키보드이벤트핸들러 = (e) => {
    if(e.key) {
      set중복메시지('');
    }
    if(입력값 === '') {
      set중복메시지('값을 입력해야지');
    }
  }

  return (
    <>
      <div>
        <textarea
          ~ other event handler ~
          onKeyUp={키보드이벤트핸들러}
        />
      </div>
    </>
  )
}

export default 내가하고싶은컴포넌트;\
```

일단 위에서 작성한 코드는 값을 입력하지 않은 상태로 가입을 하려 했을 때 메시지가 나올 수 있도록 작성하고, 키보드가 눌릴 때 입력값을 작성하고 있다는 것으로 인식하여 메시지를 없어지게 하는 내용이다.

이벤트 함수이기 때문에 e.key인 조건에서, 즉 키보드를 눌렀을 때 빈 문자열인 상태로 바꿔주고, 입력값 자체를 빈 문자열인 경우를 생각하여 메시지를 띄울 수 있게 만들었다.

수강생 시절 키보드 이벤트에 대한 내용을 봤을 때, 실습을 제대로 해볼 일이 없어 내가 원하는 이벤트를 어떻게 실행시킬지에 대해 고민을 많이 했는데 개발을 실무에서 해보면서 이것 저것 많이 배우고 해볼 수 있어 좋다.
