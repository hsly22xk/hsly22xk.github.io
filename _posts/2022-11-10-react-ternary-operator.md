---
layout: single
title: "[React] 삼항연산자 사용 시 동시 이벤트 작동 방법"
categories: React
tag: [기록, react, 리액트]
author_profile: false
---

리액트에서 삼항연산자를 사용했을 때 동시 이벤트를 작동하는 방법.

## 원인

개발을 하다가 내가 원하는 그림으로 나오지 않아 한참 고민하다 해결이 되었다.

내가 원했던 그림은 클릭 이벤트를 작성했을 때, 그 안에 한 조건이 참인 경우 두 가지 이상의 이벤트를 동작시키는 것이었다.

```javascript
onClick={() => {condition1 ? value1 value2 : value3}}
```

상기 코드가 맞는 코드는 아니지만, 직관적으로 작성해본 코드다.

(근데 작성해보고 나니 정말 저렇게 작동되면 좋을 것 같은데 왜 저렇게 못하게 했을까, 리액트 형님들(?)의 큰 뜻이 있는것일까...)

## 해결방법(1)

```javascript
onClick={() => {condition1 ? () => {value1; value3}} : value2}
```

처음에는 저렇게 작성했었는데, 에러가 뜨면서 작동하지 않았다.

```javascript
onClick={condition1 ? () => { value1 value2 } : value3}
```

그래서 삼항연산자를 감싸고 있던 중괄호를 없애 해결했다.

## 해결된 이유

해결은 했는데 중괄호를 없애야만 내가 원하는 그림이 나오는 이유에 대해 궁금했다.

같이 일하는 분(header 없애는 방법에 대해 알려주신 분과 같은 분)께 물어보았더니, 중괄호로 묶으면 화살표함수에 리턴이 없기 때문에 실행이 되지 않고 그냥 넘어간다고 한다. 중괄호를 없애거나 리턴을 붙여야 제대로 실행이 된다고 한다.

물론 실제 코드가 condition1, value1 ... 의 형식은 아니지만, 실제 코드도 제대로 작동하는 것을 확인할 수 있었다.

## (1)의 방법은 안된다

22.11.09 09:20) 로컬 화면에서 동작하는 것처럼 보였지만 실제로는 동작하지 않는 코드였다.

Uncaught Error: Expected `onClick` listener to be a function, instead got a value of `object` type.

이라는 에러 메시지가 떴는데, 찾아보니 onClick 이벤트에는 함수가 들어가야하는데, 지금 나는 객체 타입으로 value를 가지고 있다고 나온다.

일단 지금까지의 결론으로는 onClick 이벤트에 함수 형태를 없애고 작성할 수 없는 것 같다.

그래서 return을 붙여봤더니 아예 화면에서조차 동작하지 않고 있다.

## 해결방법(2)

22.11.09 09:41)

아래는 내가 처음 작성했던 코드다.

```javascript
onClick={condition1 ? () => { value1 value2 } : value3}
```

클릭 이벤트에서 value3는 어떠한 기능을 하는 함수였다.

리액트에서 이벤트 함수를 전달해줄 때는 함수형태로 주어야 하는데, 기능 함수만 주면 함수 실행 후 리턴값을 넣는 것과 같아 화살표 함수로 한 번 감싸준 후 넣는, 함수 형태로 만들어야 한다는 것을 알게 되었다.

즉 나는 참일 때의 경우만 함수 형태로 감싸주고 :콜론 뒤에는 그냥 작성해주었기때문에 리액트에서는 객체 형태로 값을 그대로 넘겨준다고 판단했기 때문에 상기 에러 메시지가 뜬 것이었다.

```javascript
onClick={condition1 ? () => { value1 value2 } : () => { value3 }}
```

이러한 형태로 바꿔주어야 올바른 코드가 될 수 있었다.

## 클릭 이벤트에 여러 조건들이 있을 때 각각의 이벤트로 동작시키기

조건들이 여러가지일 때, 각각의 조건들에 맞는 이벤트로 동작하는 그림을 먼저 그리고 시작했다.

```javascript
onClick={
  data === ''
    ? () => {
      setDuplicateMessage('데이터 작성');
      handleEvent();
    }
    : data === 'data'
    ? () => {
      setDuplicateMessage('중복 데이터');
      handleEvent();
    }
    : dataOne === ''
    ? () => {
      setDuplicateMessage('이 항목도 작성해야지');
      handleEvent();
    }
    : dataTwo === ''
    ? () => {
      setDuplicateMessage('전부 작성해야지');
      handleEvent();
    }
    : () => {
      atTheEnd();
     }
   }
```

처음 작성했던 코드인데, 이렇게 작성하니 제일 처음 data === '' 일 때의 조건만 실행이 되었다.

if ... else if ... else의 경우라고 생각을 하고 작성을 했는데, 실행 화면을 보고 다시 생각해보니 else if는 조건 중 하나라도 걸리면 그것만 실행한다. 내가 원하는 그림을 그리기에 맞는 코드 진행이 아니었다.

그래서 삼항연산자를 사용하지 않고, onClick={() => {}} 이벤트 함수 안에 각각의 조건들을 if문으로 전부 따로 작성해줬다.

그렇게 작성한 후 실행했더니, 이번엔 제일 마지막에 작성한 조건문만 실행된다. 즉, 앞서 작성한 조건문들은 실행이 되지 않았다.

22.11.10)위의 코드들을 보면 상태들이 전부 똑같다. 그래서 아마 앞서 작성한 조건문들이 실행이 되지 않는 것 같다.
그래서 useState를 활용하여 전부 다른 상태들로 바꿔주어 해결했다.
