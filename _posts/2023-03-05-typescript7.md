---
layout: single
title: "D+5 Interface in Typescript(1)"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

- 해당 포스팅은 노마드 코더의 "Typescript로 블록체인 만들기" 강의를 정리한 내용입니다.

## 데이터를 보호하기 위한 방법

```typescript
type Tendency = {
  [key: string]: string;
};

class Mbti {
  private tendency: Tendency;
  constructor() {
    this.tendency = {};
  }
  add(t: Personality) {
    if (this.tendency[t.term] === undefined) {
      this.tendency[t.term] = t.def;
    }
  }
  def(term: string) {
    return this.tendency[term];
  }
}

class Personality {
  constructor(public term: string, public def: string) {}
}

const I = new Personality("Introversion", "내향형");

const mbti = new Mbti();

mbti.add(I);
mbti.def("Introversion");
```

만약, 타입스크립트에서 내용을 수정하는 것으로부터 데이터를 보호하려면 어떻게 할 수 있을까?

현재 코드에서는 term과 def가 public이기 때문에, 데이터를 마음대로 수정할 수 있지만, 그렇게 하지 않기 위해서?

```typescript
class Personality {
  constructor(public readonly term: string, public readonly def: string) {}
}

const I = new Personality("Introversion", "내향형");

I.def("외향형"); // 작동하지 않는 코드
```

답은 간단하다. readonly 속성을 붙여주기만 하면 된다. readonly 속성을 붙이면 public이더라도 데이터를 덮어쓰는 것을 방지할 수 있다.

대부분의 경우에는 private이나 protected 속성을 사용하는데, 이 예제에서는 property들을 public으로 둔 상태에서 readonly, 즉 읽기 전용으로 만들어 데이터를 수정하는 것을 보호할 수 있다.

## static

```typescript
type Tendency = {
  [key: string]: string;
};

class Mbti {
  private tendency: Tendency;
  constructor() {
    this.tendency = {};
  }
  def(term: string) {
    return this.tendency[term];
  }
  static test() {
    return "test clear";
  }
}

console.log(Mbti.test()); // test clear
```

이러한 static 메소드는 클래스를 생성하지 않아도 사용할 수 있다.

## 타입을 쓰는 여러가지 방법

```typescript
type Profile = {
  name: string;
  age: number;
};
```

interface에 대해 설명하기 전, type에 대한 정의를 다시 한 번 짚고 넘어가보고자 한다.

상기 코드는 TS에게 property의 이름과 타입이 무엇인지에 대해(객체의 모양에 대해) 알려주는 의미다.

```typescript
type Profile = {
  name: string;
  age: number;
};

// kimcoding이라는 이름의 객체
const kimcoding: Profile = {
  // 자동완성기능을 위한 kimcoding의 타입은 Profile임을 명시해줌
  name: "kimcoding",
  age: 15,
};
```

이런 방식으로 타입을 쓸 수 있다.

또 다른 방법으로는 아래와 같이 작성할 수 있고,

```typescript
type Mbti = string; // Mbti의 타입이 string임을 알려줌

const I: Mbti = "Introversion"; // Mbti의 타입이 string이기 때문에 작동하는 코드
```

alias를 쓸 수도 있다.

```typescript
type Name = string;
type Age = number;
type Address = Array<string>;

type Profile = {
  name: Name;
  age: Age;
};

// kimcoding이라는 이름의 객체
const kimcoding: Profile = {
  // 자동완성기능을 위한 kimcoding의 타입은 Profile임을 명시해줌
  name: "kimcoding",
  age: 15,
};
```

타입을 지정된 옵션으로만 제한할 수도 있다.

```typescript
type Address = "Pellican" | "Desert" | "Ridgeside";
// 특정한 하나의 값이 아닌 여러 개의 값이 있고, 그 타입을 지정해주고 싶을 때 타입을 만들어 지정해줄 수 있다
// === Type에 특정 값을 가지도록 하는 부분

type Age = 10 | 20 | 30;

type Profile = {
  name: string,
  village: Address,
  age: Age
}

const kimcoding: Profile {
  name: "kimcoding",
  village: "Pellican", // 미리 허용된 값만 작성 가능.
  age: 10 // 미리 허용된 값만 작성 가능.
}
```

Address 타입처럼 concrete 타입의 특정 값을 쓸 수 있다.

만약 특정 값 이외의 다른 값을 쓰게 된다면 그 값은 허용되지 않는다.

```typescript
type Address = "Pellican" | "Desert" | "Ridgeside";

type Age = 10 | 20 | 30;

type Profile = {
  name: string,
  village: Address,
  age: Age
}

const kimcoding: Profile {
  name: "kimcoding",
  village: "Zuzu", // Type '"Zuzu"' is not assignable to type 'Address'.
  age: 10
}
```

Type은 객체의 모양을 묘사하는 데 사용하며, 타입 alias를 만들고, 타입이 특정 값을 가지도록 제한할 수도 있다.

## Interface

Type과 마찬가지로 객체의 모양을 설명하는 다른 방법이다.

```typescript
type Address = "Pellican" | "Desert" | "Ridgeside";
// 특정한 하나의 값이 아닌 여러 개의 값이 있고, 그 타입을 지정해주고 싶을 때 타입을 만들어 지정해줄 수 있다
// === Type에 특정 값을 가지도록 하는 부분

type Age = 10 | 20 | 30;

interface Profile {
  name: string,
  village: Address,
  age: Age
}

const kimcoding: Profile {
  name: "kimcoding",
  village: "Zuzu", // Type '"Zuzu"' is not assignable to type 'Address'.
  age: 10
}
```

interface는 객체의 모양을 특정해 주기 위해 사용하며, React.js를 활용하여 작업할 때 많이 사용한다.

이러한 interface는 property들을 축적시킬 수 있다는 특징을 가지고 있다.

ex)

```typescript
interface Person {
  name: string;
}

interface Person {
  lastName: string;
}

interface Person {
  age: number;
}

const kimcoding: Person = {
  name: "kimcoding",
  lastName: "k",
  age: 15,
};
```

이렇게 같은 interface에 다른 이름을 가진 property들을 쌓을 수 있다.

## Type vs Interface

둘 다 객체의 모양을 잡아주는 데 사용하지만, type 키워드가 interface 키워드에 비해 활용할 수 있는 것이 많다.

```typescript
interface Hello = string; // 작동하지 않는 코드
```

interface는 객체의 모양을 TS에게 설명해 주기 위해서'만' 사용되는 키워드인 반면, type 키워드는 다양한 목적을 가지며 사용할 수 있다.

ex)

```typescript
interface Person {
  name: string;
  // readonly name: string;
  // ① readonly 속성을 붙이면
}

// 상속 개념 적용 가능
interface Profile extends Person {}

const kimcoding: Profile = {
  name: "kimcoding",
};

kimcoding.name = "coding"; // ② 해당 코드는 작동하지 않음
```

```typescript
type Person = {
  name: string;
};

type Profile = Person & {};

const kimcoding: Profile = {
  name: "kimcoding",
};
```
