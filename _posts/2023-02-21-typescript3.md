---
layout: single
title: "D+2 타입스크립트의 타입들(2)"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

기존 티스토리 블로그에 올렸던 타입스크립트 관련 내용을 옮겨보고자 한다.

## readonly 속성 타입에 추가하기

✷ readonly : 말 그대로 요소들을 읽기 전용으로 만들 수 있는 속성.

```typescript
type Profile = {
  readonly name: string;
  age?: number;
};

const profileList = (name: string): Profile => ({ name });
const kimcoding = profileList("kimcoding");

kimcoding.name = "kim"; // 작동하지 않음
```

상기 코드처럼 name이라는 요소에 readonly 속성이 붙게 되면, name을 수정할 때 TS가 막아준다.

```typescript
const numbers: readonly numbers[] = [1, 2, 3, 4];
numbers.push(5); // 작동하지 않음
```

이처럼 number 타입의 요소들로 이루어진 배열 안에 5를 push 하는 것은 되지 않는다.

왜냐하면 push라는 것은 readonly number[] 타입에 존재하지 않기 때문이다.

```typescript
const names: readonly string[] = ["kimcoding", "parkhacker"];
names.push("leejava"); // 작동하지 않음

// filter 혹은 map은 불변성을 가지기 때문에 array를 바꾸지 않아 readonly 속성이 있더라도 사용 가능하다
names.filter();
names.map();
```

## Tuple

: 정해진 개수와 순서에 따라 배열을 선언할 수 있다.

항상 정해진 개수의 요소를 가져야 하는 array를 지정할 수 있고, 순서의 맞는 타입의 값을 요구할 때 유용하다.

```typescript
const profile: [string, number, boolean] = []; // 작동하지 않음
```

작동하지 않는 이유는, profile에는 3가지의 요소가 들어가야 하고 그 타입은 순서대로 string, number, boolean이어야 하는데 막상 배열 안에는 아무 요소도 들어가 있지 않기 때문이다.

```typescript
const profile: [string, number, boolean] = ["kimcoding", 15, true];
profile[0] = 1; // 작동하지 않음
```

이미 0번째 요소는 string 타입으로 지정해 주었기 때문에 number 타입으로 바꾸려 하면 작동하지 않는다.

```typescript
const profile : readonly[string, number, boolean] = ['kimcoding', 15, true];]
profile[0] = 'hello'; // 작동하지 않음
```

readonly 속성을 붙여준다면 아무것도 바꿀 수 없다.

## any타입

```typescript
// let a: any[]
// 빈 배열을 쓰게 되면 TS는 기본적으로 이것을 any의 array라고 생각한다.
let a = [];
```

: TS의 보호장치들을 비활성화 시킬 때 쓰는 타입으로, 비어있는 값을 쓰게 되면 기본값은 any라는 타입이 된다.

any는 그 어떤 타입이라도 될 수 있는 타입이다.

```typescript
const array: any[] = [1, 2, 3, 4];
const b: any = true;

a + b; // 작동하는 코드
```

any를 마구잡이로 남발하는 것은 당연히 좋은 방식이 아니지만, 가끔은 any를 사용해야 할 때가 생긴다.

✷ undefined, null, any
any: 아무 타입
undefined: 선언X 할당X
null: 선언O 할당X
