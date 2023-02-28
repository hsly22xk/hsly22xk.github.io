---
layout: single
title: "D+2 타입스크립트의 타입들(1)"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

기존 티스토리 블로그에 올렸던 타입스크립트 관련 내용을 옮겨보고자 한다.

## TS의 타입들

[앞의 글](https://hsly22xk.tistory.com/406)에 작성한 대로, number, string, boolean 등 기본적인 타입들도 있지만 TS에서 쓰는 타입들에 대해 정리한다.

```typescript
// 기본 타입들
let a: number = 1;
let b: string = "1";
let c: boolean = true;

// number, string, boolean으로 된 array
let a: number[] = [1];
let b: string[] = ["1"];
let c: boolean[] = [true];
```

## 변수에 타입을 할당하는 방법

① 선택적 변수(optional parameter) 지정하기

```typescript
const profile = {
  name: "kimcoding",
};
```

상기 예시에서, profile 안에 name은 모두 가지고 있지만, 몇몇 profile에서 age만 가지고 있다는 가정하에 TS에서는 어떻게 쓸 수 있을까?

profile의 타입이 obejct라고 적어준다면, 에러가 난다.
![](https://blog.kakaocdn.net/dn/byVLQD/btr0aPYZbe9/RyP31GjFC5V39xRxObGIf1/img.png)
profile 자체를 object 타입이라고 적어주는 것은 TS에서 아무 의미가 없다.

그렇기 때문에 일단 이렇게 작성해 준다.

```typescript
const profile: {
  name: string;
  age: number;
} = {
  name: "kimcoding",
};
```

하지만 이렇게 작성한다면 age 속성이 들어가 있지 않기 때문에 다시 에러 메시지를 보내주고, 처음 원하던 대로의 형태로 나오지 않는다.

```typescript
const profile: {
  name: string;
  age?: number;
} = {
  name: "kimcoding",
};
```

![](https://blog.kakaocdn.net/dn/E6NiM/btr0fsBKh1S/lcdNcx5icgsNC4eBkWL8O1/img.png)
age뒤에 ?를 붙여주면 해결이 된다.

?를 붙여주면 age의 타입은 number or undefined가 된다.

이때,

```typescript
const profile : {
name: string,
age?: number
} = {
name: 'kimcoding'
}


if(profile.age < 10) {
...
}
```

![](https://blog.kakaocdn.net/dn/boln9d/btr0aVybnMh/jLF6kRAndjoLzTzaroShP1/img.png)

앞에서 age의 타입을 number일수도 있고 undefined일 수도 있다고 지정을 해 두었기 때문에, 단순히 profile.age가 number 타입인 것처럼 생각하고 코드를 작성한다면 에러 메시지를 띄운다.

```typescript
if(profile.age && profile.age < 10) {
...
}
```

이렇게 작성해 주면 해결된다.

✷ undefined & null

undefined와 null은 TS, JS 모두 쓰인다. 선택적 타입은 undefined가 될 수 있다.

let a : undefined = undefined;
let b : null = null;

② Alias 타입

만약 수많은 profile들을 만들게 된다면, 이를 더 효율적으로 작성할 수 있는 코드가 있지 않을까?

```typescript
const profileOne : {
  name: string,
  age?: number
} = {
  name: 'kimcoding'
}

const profileTwo : {
  name: string,
  age?: number
} = {
  name: 'parkhacker',
  age: 20
}

const profileThree : {
  name: string,
  age?: number
} = {
  name: 'leejava',
}

...
```

이런 경우에는 별칭(alias)을 사용할 수 있다.

```typescript
type Profile = {
  // 꼭 대문자로 시작하기!
  name: string;
  age?: number;
};

// Profile 타입으로 지정해주었기 때문에 변수명에 들어가있던 profile을 지워주어도 작동한다.
const one: Profile = {
  name: "kimcoding",
};

const two: Profile = {
  name: "parkhacker",
  age: 20,
};

const three: Profile = {
  name: "leejava",
};
```

이러한 alias 타입은 object 타입에서만 유효한 것이 아니라, 어떤 타입에서든 적용할 수 있다.

```typescript
type Age = number;
type Profile = {
  name: string;
  age?: Age; // 꼭 이렇게 할 필요는 없지만, 이렇게도 할 수 있다.
};

const one: Profile = {
  name: "kimcoding",
};

const two: Profile = {
  name: "parkhacker",
  age: 20,
};

const three: Profile = {
  name: "leejava",
};
```

## 함수의 리턴값의 타입 지정 방법

```typescript
type Profile = {
  name: string;
  age?: number;
};

// profile의 object를 만들고 그 결과로 Profile을 반환하는 함수
function profileList(name: string) {
  return {
    name,
  };
}

const kimcoding = profileList("kimcoding");
kimcoding.age = 15; // 작동하지 않음
```

TS에서는 제대로 동작하지 않는다.

왜냐하면 profileList() 안에는 name이라는 요소만 있는 object만 리턴하고 있기 때문이다.

그렇다면 어떻게 함수가 리턴하는 것에 대한 타입을 이야기해 줄 수 있을까?

```typescript
type Profile = {
  name: string;
  age?: number;
};

function profileList(name: string): Profile {
  return {
    name,
  };
}

const kimcoding = profileList("kimcoding");
kimcoding.age = 15;
```

함수에 Profile이라는 타입을 붙여주면, string 타입으로 name을 받고 Profile 타입을 리턴하는 함수로 받아들여진다.

## TS에서 화살표 함수 사용하기

```typescript
type Profile = {
name: string,
age?: number
}

// name을 인자로 받고 name이 있는 object를 리턴하는 함수
const profileList = (name: String) => ({name});

const kimcoding = profileList('kimcoding');
kimcoding.age = 15; // 작동하지 않음
이렇게 했을 때, profileList()가 Profile을 리턴하는 함수라는 것을 명시해주지 않았기때문에 에러 메시지가 뜬다.

type Profile = {
name: string,
age?: number
}

const profileList = (name: String) : Profile => ({name});

const kimcoding = profileList('kimcoding');
kimcoding.age = 15;
```
