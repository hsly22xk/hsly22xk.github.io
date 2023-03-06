---
layout: single
title: "D+1 타입스크립트의 개념과 타입 시스템"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

- 해당 포스팅은 노마드 코더의 "Typescript로 블록체인 만들기" 강의를 정리한 내용입니다.

## Typescript(TS)

: 작성한 코드를 Javascript(JS)로 변환해 주는 strongly typed(강타입) programming language.

→ Node.js는 TS와 JS 모두 이해하지만, 브라우저는 TS가 아닌 JS를 이해한다.

## TS를 사용하는 이유

: JS는 어떠한 코드를 실행할 때 런타임 에러 현상 해결을 도와주지 않지만, TS는 코드를 실행하기 전에 이러한 런타임 에러를 잡아줄 수 있음.

✷ 런타임 에러: 코드를 실행할 때 발생하는 에러

→ 컴파일은 작성한 TS 코드를 JS로 바꿔준다. 하지만 TS 코드에 에러가 있으면 그 코드는 JS로 컴파일되지 않는다.

⇒ (이 과정은 유저가 코드를 실행하는 런타임에 발생하는 것이 아니며, 일반 유저들은 JS 코드만 사용한다)

JS 코드 자체는 어떠한 보호장치가 없지만, TS가 유효하지 않은 JS 코드 실행을 방지해준다.

ex)

```typescript
function plus(a, b) {
  return a + b;
}
plus("1", false);
// '1false'
```

브라우저의 개발자 도구에서 plus라는 함수는 인자를 각각 a, b로 넣고 a + b의 값을 리턴하는 함수다.

하지만 각각 인자에 넣은 값의 타입은 string과 boolean이다. 이 두 개를 더할 수 없다는 것을 사람은 알지만 JS에서는 그대로 값이 나오는 것을 확인할 수 있었다.

이때, TS는 인자의 타입을 지정해야 한다는 것을 알려주고, 만약 인자를 하나 쓰지 않은 상태라면 에러 메시지를 띄워준다.

```typescript
function plus(a, b) { // 인자의 타입을 지정해주지 않음
return a + b;
}
plus(1); // plus 함수의 인자는 2개지만 여기서는 1개만 넣음

Parameter 'a' implicitly has an 'any' type.
Parameter 'b' implicitly has an 'any' type.
Expected 2 arguments, but got 1. 3. TS의 타입 시스템
```

## TS의 타입 시스템

JS에서는 변수의 타입을 지정해주지않고도 변수를 선언할 수 있지만, TS는 모든 것의 타입을 지정해주어야 한다. → TS는 먼저 코드를 확인한 다음 데이터 타입을 먼저 비교해 주기 때문에 사용자의 오류를 방지해 준다.

ex) 만약 변수에 1이라는 값을 할당한다면, 컴파일러에게 변수의 타입은 number이고, 항상 number라는 것을 알려주어야 한다(= 변수의 타입이 number임을 지정해주어야 한다).

① Implicit Types(암시적 타입)

타입을 추론하게 하는 방법의 예시
![](https://blog.kakaocdn.net/dn/cNsSGa/btrZV7NgEvr/CJzZ10XDOCUyV3wHsAk8wk/img.png)
![](https://blog.kakaocdn.net/dn/OhSPu/btrZ7cmmJLC/koDytuiJh9c3DzOmPVzQ3K/img.png)
a라는 변수에 'hello'라는 string 타입의 값을 지정해 주었다. 이제 a에 1이라는 number 타입을 재할당해 주었을 때, 에러 메시지가 뜨는 것을 볼 수 있다. 하지만 같은 string 타입으로 재할당해 준다면, 에러 메시지는 뜨지 않는다.

```typescript
let a = "hello";
a = "world";
```

(JS 코드를 작성하면서 재할당되는 값의 타입을 생각해 본 적이 없었는데, 처음 학습하면서 너무 신기했던 부분 중 하나였다).

② Explicit Types(명시적 타입)

구체적으로, 명시적으로 타입을 지정해주는 방법
![](https://blog.kakaocdn.net/dn/bisbMF/btrZV86vmlx/YwKjKl19I6rgoh3BU0kxFk/img.png)
①번에서의 예시처럼 따로 명시를 해주지 않아도 상관없지만, 명시적으로 타입을 작성해 줄 수도 있다.

하지만 변수 b의 타입을 boolean으로 해주었지만 number 타입인 1을 할당했다면, 역시 에러 메시지가 뜬다.

저 코드를 맞는 코드로 수정하려면 다음과 같이 작성할 수 있다.

```typescript
let b: boolean = true;
```

저렇게 에러 메시지가 뜨는 이유는 a는 string 이어야 하고, b는 boolean이어야 하기 때문이다. 왜냐하면 코드를 작성할 때 타입을 지정해주었고, 값을 해당 타입으로 할당해주었기 때문이다.

둘 다 사용할 수 있지만, ②번에서의 예시가 TS의 문법이다.

ex)
![](https://blog.kakaocdn.net/dn/IzJKj/btrZ7b14Pth/KXymREWgYyH8JZ8ZR9ftv1/img.png)

```typescript
let d = [1, 2, 3];
d.push("4");
```

배열에서도 마찬가지다.

number 타입으로만 이루어진 요소들의 배열 안에 string 타입의 요소를 넣으려고 한다면, 작동하지 않는다.
![](https://blog.kakaocdn.net/dn/cXNlce/btrZ9GfJ5Ga/ohqH1K69R7SjJmSekAPLA1/img.png)

```typescript
let c = ["1", 2, 3];
c.push(false);
```

string과 number 타입이 섞여있어도 마찬가지다. boolean타입의 요소를 넣으려고 할 때 작동하지 않는 것을 알 수 있다.

배열의 타입을 명시해주려면,

```typescript
let d = number[] = [];
d.push('4') // 작동하지 않음
```

이러한 명시적 표현은 TS가 타입을 추론하지 못할 때 유용하지만, 보통 명시적 표현은 최소한으로 사용하는 것이 좋다.
![](https://blog.kakaocdn.net/dn/tYLp8/btrZ7a3eqXR/uv5iqSj8coJK9Z7WDNjoJK/img.png)

```typescript
const profile = {
  name: "kimcoding",
};

profile.name = 1; // 작동하지 않음
profile.name(); // 작동하지 않음
```

이러한 에러들은 추론이 동작하기 때문에 발생하는 것이다.

profile이라는 객체 안의 key인 name의 value 타입은 string인데, number 타입 혹은 아예 있지 않은 function은 작동하거나 호출할 수 없다고 나온다.
