---
layout: single
title: "D+3 타입스크립트의 타입들(3)"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

- 해당 포스팅은 노마드 코더의 "Typescript로 블록체인 만들기" 강의를 정리한 내용입니다.

## unknown

: 변수의 타입을 미리 알지 못할 때 사용할 때마다 변수타입 지정을 요구한다. unknown타입은 모든 값을 나타낸다.

```typescript
let a: unknown;

if (typeof a === "number") {
  // a의 타입이 number임을 먼저 체크
  let b = a + 1; // 코드 동작
}

if (typeof a === "string") {
  // a의 타입이 string임을 먼저 체크
  let b = a.toUpperCase(); // 코드 동작
}
```

✅ any vs unknown

① any

모든 타입을 할당받을 수 있는 타입.

사용자로부터 받은 데이터 혹은 써드 파티 라이브러리 같은 동적인 컨텐츠로 오는 불특정한 값을 컴파일 검사를 하지 않고 사용하고자 할때 사용하며, 컴파일 중 타입검사를 하지 않아 기존의 Javascript 와 같이 작업하기에 용이하다.

TypeScript에서 타입 검사를 느슨하게 하므로 개발 당시에는 문제가 없으나 애플리케이션 또는 웹 페이지 개발 후 예기치 못한 문제가 발생할 가능성이 매우 높다.

② unknown

모든 타입을 포함하여 어느 값이든 가질 수 있는 타입.

(= unknown은 변수가 어떤 타입이 될 지 모르기 때문에 추론해달라고 컴파일러에게 이야기하는 것과 같다)

any 타입과는 다르게 프로퍼티 또는 연산을 하는 경우 컴파일러가 체크하기 때문에 문제 되는 코드를 미리 예방할 수 있어 안정적인 애플리케이션을 개발할 수 있다.

(= unknown 타입으로 지정된 값은 타입을 먼저 확인한 후에 무언가를 할 수 있기 때문에 unknown 을 사용하는 것이 보다 안전하다)

```typescript
ex)
let a: unknown

let anyType: any = a

let booleanType: boolean = a
// Error: Type 'unknown' is not assignable to type 'boolean'.

let numberType: number = a
// Error: Type 'unknown' is not assignable to type 'number'.

let stringType: string = a
// Error: Type 'unknown' is not assignable to type 'string'.

let objectType: object = a
// Error: Type 'unknown' is not assignable to type 'object'.
```

unknown 타입은 any 타입을 제외한 다른 타입으로 선언한 변수에 할당할 수 없다.

⇒ any 를 사용하는 곳에서 unknown 을 사용하여 보다 안전하게 코딩할 수 있다.

any 는 타입을 좁혀서 사용하지 않아도 되지만, unknown 은 타입을 좁혀서 사용해야만 한다.

## void

: 아무것도 return 하지않는 함수를 대상으로 사용함.

하지만 타입스크립트는 아무것도 return하지 않는 함수를 자동으로 인식하기 때문에 보통은 void를 따로 지정해줄 필요는 없음.

```typescript
// a() 함수의 타입은 void
// function a(): void
function a() {
  console.log("x");
}

const b = a();

// 동작하지 않음
// Property 'toUpperCase' does not exist on type 'void'.
b.toUpperCase();
```

## never

: 함수가 절대 리턴하지 않을 때 발생한다(함수에서 예외(exception)가 발생할 때).

```typescript
ex)
function a() {
  return 'b';
}

function a(): never {
  return 'b'; // 동작하지 않음
}

// 리턴하지않고 오류를 발생시키는 함수
function a(): never {
  throw new Error('b'); // 정상 동작함
}

// 타입이 두 가지일 수도 있는 상황에서 발생할 수 있는 never
function a(name: string|number) { // name의 타입이 string이거나 number일 수 있음을 미리 알려줌
  if(typeof name === 'string') { // name의 타입이 string임을 체크해주는 스코프(범위)
    name // string
  } else if(typeof name === 'number') { // name의 타입이 number임을 체크해주는 스코프
  name // name: number

    // else 스코프에 있는 코드는 절대 실행되지 않아야함을 의미함
    // 앞의 코드들에서 타입이 올바르게 들어온다면 이 코드는 작동하지 않음
  } else {
    name // name: never
  }
}
```
