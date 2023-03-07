---
layout: single
title: "D+5 Interface in Typescript(2)"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
published: false
---

- 해당 포스팅은 노마드 코더의 "Typescript로 블록체인 만들기" 강의를 정리한 내용입니다.

## 추상화를 원할 때 Class vs Interface

ex - abstract class)

```typescript
abstract class Person {
  constructor(protected firstName: string, protected lastName: string) {}

  // 추상 클래스는 무엇을 구현해야할 지에 대해 알려줄 수 있다
  abstract yourName(name: string): string;
  abstract myName(): string;
}

new Person(); // Cannot create an instance of an abstract class.

class Profile extends Person {
  myName() {
    return `${this.firstName} ${this.lastName}`;
  }
  yourName(name: string) {
    return `Hello ${name}. My name is ${this.myName()}`;
  }
}
```

만약 많은 Profile들을 만들고, Person을 직접적으로 만들지 않고도 코드에 남으려면?

Interface는 매우 가볍다. Interface는 컴파일하면 JS로 바뀌지 않고 바로 사라진다.

그렇다면 Interface를 사용할 때, 클래스가 특정 형태를 따르도록 강제할 수 있는 방법이 있을까?

ex - interface)

```typescript
interface Person {
  firstName: string;
  lastName: string;
  yourName(name: string): string;
  myName(): string;
}

class Profile implements Person {
  constructor(
    // interface를 상속할 때 property를 private이나 protected로 만들 수 없다
    // 무조건 public이어야 함
    public firstName: string,
    public lastName: string
  ) {}
  myName() {
    return `${this.firstName} ${this.lastName}`;
  }
  yourName(name: string) {
    return `Hello ${name}. My name is ${this.myName()}`;
  }
}
```

클래스는 아니지만 클래스의 모양을 특정할 수 있게 해주는 간단한 방법이다. 또한 implement를 사용하면 코드가 더 가벼워진다.

interface Person을 추적할 수 없는데, interface는 TS에서만 존재하는 개념이다.

interface는 클래스의 모양을 알려주면서도 JS 코드로 컴파일되지는 않는다. 그리고 만약 원한다면 하나 이상의 interface를 동시 상속하는 것도 가능하다.

```typescript
interface Person {
  firstName: string;
  lastName: string;
  yourName(name: string): string;
  myName(): string;
}

// ① interface Human 추가
interface Human {
  age: number;
}

class Profile implements Person, Human {
  // ② interface Human 추가 상속
  constructor(
    public firstName: string,
    public lastName: string,
    public age: number // ③ age 속성 추가
  ) {}
  myName() {
    return `${this.firstName} ${this.lastName}`;
  }
  yourName(name: string) {
    return `Hello ${name}. My name is ${this.myName()}`;
  }
}
```

```typescript
interface Person {
  firstName: string;
  lastName: string;
  yourName(name: string): string;
  myName(): string;
}

class Profile implements Person {
  constructor(public firstName: string, public lastName: string) {}
  myName() {
    return `${this.firstName} ${this.lastName}`;
  }
  yourName(name: string) {
    return `Hello ${name}. My name is ${this.myName()}`;
  }
}

// interface Person을 타입으로도 사용할 수 있다.
function allUsers(user: Person) {
  return "Hello Users";
}

// Person은 interface이기 때문에 굳이 new Person을 넣어주지 않더라도 interface의 내용 형식만 제대로 지켜주면 된다
allUsers({
  firstName: "coding",
  lastName: "kim",
  myName: () => "kimcoding",
  yourName: (name) => "string",
});
```

## Types vs Interface
