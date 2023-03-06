---
layout: single
title: "D+4 OOP(Object Oriented Programming/객체 지향 프로그래밍) in Typescript"
categories: Typescript
tag: [기록, 타입스크립트, TS]
author_profile: false
---

- 해당 포스팅은 노마드 코더의 "Typescript로 블록체인 만들기" 강의를 정리한 내용입니다.

✷ [OOP 관련 링크(1)](https://hsly22xk.tistory.com/305)

✷ [OOP 관련 링크(2)](https://hsly22xk.tistory.com/79)

## How to create Classes in Typescript

```typescript
class Profile {
  constructor(
    private firstName: string,
    private lastName: string, // private 필드
    public age: number // public 필드
  ) {}
}
// private keyword는 오직 TS가 보호해주기 위해 사용하는 것임.

const kimcoding = new Profile("coding", "kim", 15);

// 동작하지 않음
// Property 'firstName' is private and only accessible within class 'Profile'.
// 'firstName' 속성은 private이며 'Profile' 클래스 내에서만 액세스할 수 있습니다.
kimcoding.firstName;

// 동작하는 코드
kimcoding.age;
```

✅ abstract class(추상 클래스)

: 다른 클래스가 상속받을 수 있는 클래스. 오직 다른 곳에서만 상속받을 수 있는 클래스.

→ 추상 클래스는 직접 새로운 인스턴스를 만들 수 없음.

```typescript
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    public age: number
  ) {}
}

class Profile extends User {}

// 동작하지 않는 코드
// Cannot create an instance of an abstract class.
// 추상 클래스의 인스턴스를 만들 수 없습니다.
const kimcoding = new User("coding", "kim", 15);
```

✅ abstract method(추상 메소드)

: 추상 클래스를 상속받는 모든 것들이 구현해야하는 메소드.

✷ method(메소드): 클래스 안에 존재하는 함수.

```typescript
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    public age: number
  ) {}
  private getFullName() {
    // add private keyword
    return `${this.firstName} ${this.lastName}`;
  }
}

class Profile extends User {}

const kimcoding = new Profile("coding", "kim", 15);

// 동작하지 않음
// 'getFullName' 속성은 private이며 'User' 클래스 내에서만 액세스할 수 있습니다.
kimcoding.getFullName();

// private, public은 property 뿐만 아니라 method에서도 작동하는 것을 알 수 있음
```

```typescript
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    public age: number
  ) {}
  // 추상 클래스 안에 들어가있는 메소드
  // 명시하지 않았지만 기본적으로는 public이다.
  getFullName() {
    return `${this.firstName} ${this.lastName}`; // 메소드의 구현(implementation)
  }
}

class Profile extends User {}

const kimcoding = new Profile("coding", "kim", 15);

// coding kim
// 추상 클래스에서 메소드를 구현했을 때 상속받는 클래스에서 호출할 수 있음을 알 수 있음.
kimcoding.getFullName();
```

추상 메소드를 만들려면 메소드를 클래스 안에서 구현하지 않으면 된다.

⇒ 추상 클래스 안에서는 추상 메소드를 만들 수 있지만 메소드를 구현해서는 안되고 메소드의 call signature만 적어두어야 한다.

```typescript
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    private age: number
  ) {}
  abstract getAge(): void; // call signature
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

// Non-abstract class 'Profile' does not implement inherited
// abstract member 'getAge' from class 'User'.
// 비추상 클래스 'Profile'은(는) 'User' 클래스에서 상속된 추상 멤버 'getAge'을(를) 구현하지 않습니다.
// TS에서 Profile이 getAge를 구현해야한다고 알려주고 있음.
class Profile extends User {}

// 추상 클래스를 상속받는 클래스에서 추상 메소드를 구현해주어야 한다.
class Profile extends User {
  getAge() {
    console.log(this.age);
  }
}

const kimcoding = new Profile("coding", "kim", 15);
kimcoding.getFullName(); // coding kim
```

```typescript
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    private age: number
  ) {}
  abstract getAge(): void;
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

class Profile extends User {
  getAge() {
    // 앞에서 age를 private property로 만들었기 때문에 동작하지 않는 코드임
    // property를 private으로 만들면, 그 클래스를 상속했더라도 그 property에 접근할 수 없음.
    // private 필드가 있을 때, properties는 인스턴스 밖에서 접근할 수 없고, 다른 자식 클래스에서도 접근할 수 없음
    console.log(this.age);
  }
}
```

private은 User 클래스의 인스턴스나 메소드에서 접근할 수 있지만, User 클래스는 추상 클래스이기 때문에 인스턴스화 할 수 없다.

✅ protected

```typescript
abstract class User {
  constructor(
    // change private to protected
    protected firstName: string,
    protected lastName: string,
    protected age: number
  ) {}
  abstract getAge(): void;
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

class Profile extends User {
  getAge() {
    console.log(this.age);
  }
}

const kimcoding = new Profile("coding", "kim", 15);

// 동작하지 않음
// firstName은 proteced이기 때문에 클래스 밖에서는 접근할 수 없음
// 'firstName' 속성은 보호된 속성이며 'User' 클래스 및 해당 하위 클래스 내에서만 액세스할 수 있습니다.
kimcoding.firstName;
```

|   구분    | 선언한 클래스 내 | 상속받은 클래스 내 | 인스턴스 |
| :-------: | :--------------: | :----------------: | :------: |
|  private  |        ⭕        |         ❌         |    ❌    |
| protected |        ⭕        |         ⭕         |    ❌    |
|  public   |        ⭕        |         ⭕         |    ⭕    |

```typescript
abstract class User {
  constructor(
    protected firstName: string,
    protected lastName: string,
    protected age: number
  ) {}
  abstract getAge(): void;
  protected getFullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

class Profile extends User {
  getAge() {
    // getFullName() 호출 가능
    this.getFullName();
    console.log(this.age);
  }
}

const kimcoding = new Profile("coding", "kim", 15);

// 여전히 에러 메시지는 나옴
kimcoding.getFullName();
```

![](https://blog.kakaocdn.net/dn/bdcm9F/btr0Hu8Wg8H/cuvOu9sE3GjrMhwgYEwKX0/img.png)

만약 age를 외부 모든 곳에서 사용 가능하게 만들려면 protected를 public으로 변경해주면 된다.

✅ age의 속성을 public으로 명시해주지 않았더니, 'Property 'age' does not exist on type 'Profile.'라는 에러 메시지가 떴다.
![](https://blog.kakaocdn.net/dn/cXq5ey/btr0RILlRj6/zFj8wQa3nuXfqWaNg41NuK/img.png)

JS에서 User 클래스는 일반적인 클래스이기 때문에 원한다면 User의 인스턴스를 만들 수 있지만, TS는 허용하지 않는다.

```typescript
// object의 type을 선언해야할 때 사용할 수 있음
type Tendency = {
  // Tendencies의 타입은 string만을 property로 가지는 object임을 의미함
  // 제한된 양의 property 혹은 key를 가지는 타입을 정의해주는 방법
  // property의 이름은 모르지만 타입만 알고 있을 때 사용함
  // 타입은 number, string, boolean ... 뭐든 될 수 있음
  [key: string]: string;
};

class Mbti {
  private tendency: Tendency;
  constructor() {
    this.tendency = {};
  }
  // 클래스를 타입으로 사용 가능함
  add(t: Personality) {
    // 주어진 tendency가 Mbti에 존재하지 않는다면(=== undefined)
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
