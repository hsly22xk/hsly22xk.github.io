---
layout: single
title: "D+29 클래스를 이용한 모듈화, prototype , 객체 지향 프로그래밍"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

클래스와 oop 관련 내용 정리.

## 1. 클래스를 이용한 모듈화

① 메소드 호출: 객체.메소드() 과 같이 객체 내에 메소드를 호출하는 방법

⇒ 메소드 호출 방식을 사용할 때는 화살표 함수를 사용하지 않는다.

```js
let counter1 = {
  value: 0,
  increase: function () {
    this.value++; // 메소드 호출을 할 경우, this는 counter1을 가리킨다
  },
  decrease: function () {
    this.value--;
  },
  getValue: function () {
    return this.value;
  },
};

counter1.increase();
counter1.increase();
counter1.increase();
counter1.decrease();
counter1.getValue(); // 2
```

② 클로저를 이용해 매번 새로운 객체 생성하기

똑같은 기능을 하는 카운터가 여러 개가 필요할 때 같은 코드를 그대로 복사 / 붙여넣기 해야 하므로 재사용성이 떨어진다.

```js
function makeCounter() {
  return {
    value: 0,
    increase: function () {
      this.value++; // 메소드 호출을 할 경우, this는 makeCounter 함수가 리턴하는 익명의 객체
    },
    decrease: function () {
      this.value--;
    },
    getValue: function () {
      return this.value;
    },
  };
}

let counter1 = makeCounter();
counter1.increase();
counter1.getValue(); // 1

let counter2 = makeCounter();
counter2.decrease();
counter2.decrease();
counter2.getValue(); // -2
```

```js
// OOP(객체 지향 프로그래밍)패턴의 예시
class Counter {
  constructor() {
    this.value = 0; // 생성자 호출을 할 경우 this는 new 키워드로 생성한 Counter의 인스턴스
  }
  increase() {
    this.value++;
  }
  decrease() {
    this.value--;
  }
  getValue() {
    return this.value;
  }
}

let counter1 = new Counter(); // 생성자 호출
counter1.increase();
counter1.getValue(); // 1
```

## 2. 객체 지향 프로그래밍(OOP / Object Oriented Programming)

관련 있는 속성과 메소드를 모두 묶어두는 컴퓨터 프로그래밍 패러다임의 하나.

→ 초기의 언어(C, 포트란 등)는 절차적 언어(순차적인 명령의 조합)였으나 객체 지향 프로그래밍이 등장하면서 데이터의 접근과 처리 과정에 대한 모형을 만들어내는 방식을 고안했다.

즉, 데이터와 기능을 한번에 묶어서 처리 가능. 현대의 언어들(JAVA, C++, C# 등)이 이에 해당함.

⇒ 자바스크립트는 객체 지향 언어는 아니지만, 객체 지향 패턴으로 작성 가능.

✷ 절차 지향 프로그래밍 / 객체 지향 프로그래밍

ex) ATM 코드 이해하기

```
// 절차 지향 언어(ex. C언어)
1. 카드 / 통장 받기
2. 비밀번호 확인
3. 비밀번호가 맞으면 → 출금액 입력
   비밀번호가 틀리면 → 틀렸다고 하고 6번으로 넘어가기
4. 잔액이 출금액수보다 크면 → 5번으로 넘어가기
   잔액이 출금액수보다 부족하면 → 잔액 부족을 알리고 6번으로 넘어가기
5. 출금액수보다 ATM 보유 액수가 크면 → 출금
   출금액수보다 ATM 보유 액수가 적으면 → 보유액수가 부족함을 알리고 6번으로 넘어가기
6. 카드, 통장 돌려주기
```

```java
// 객체 지향 언어(ex. C++, Java ... )
ATM {
  카드 / 통장 받기
  비밀번호 / 잔액 / ATM 보유액 확인
  출금
  카드 / 통장 돌려주기
}

고객 {
  카드 / 통장 넣기, 받기
  비밀번호, 출금액 입력하기
  돈 받기
}
```

|             |   절차 지향 프로그래밍   |   객체 지향 프로그래밍   |
| :---------: | :----------------------: | :----------------------: |
|    특성     | 컴퓨터의 처리구조와 유사 | 사람의 사고방식에 가까움 |
| 메모리 사용 |           적음           |           많음           |
|  처리 속도  |           빠름           |           느림           |
|  재활용성   |           낮음           |           높음           |
|  코드 이해  |          어려움          |           쉬움           |
|   디버깅    |          어려움          |           쉬움           |

객체 지향 프로그래밍은 단순히 프로그램 방법론의 하나일 뿐, 항상 객체 지향만이 좋다고 할 수 없기 때문에 각 방법론의 장단점을 알고 상황에 맞는 방법론을 택한다.

ex) 메모리 관리가 중요할 땐 메모리를 적게 쓰는 절차 지향, 사람들과의 협업이 중요할 땐 코드 이해가 쉬운 객체 지향

✅ OOP

‣ 프로그램 설계 철학 중 하나.

‣ 객체로 그룹화됨.

‣ 한 번 만들고 나면 메모리상에서 반환되기 전까지 객체 내의 모든 것이 유지됨.

‣ 하나의 모델이 되는 청사진(blueprint)을 만들고, 청사진을 바탕으로 한 객체를 만드는 프로그래밍 패턴

여기서

① 클래스(class): 하나의 모델이 되는 청사진(blueprint)을 만들고(=객체를 생성하기 위한 아이디어 / 청사진),

② 인스턴스(instance): 그 청사진을 바탕으로 한 객체를 만드는(인스턴스 객체, 줄여서 인스턴스)

이라는 의미가 된다.

**✷ 클래스 문법은 (거의) 문법적 설탕에 가깝다.**

⇒ 문법적 설탕(syntactic sugar): 내부적으로는 프로토타입을 쓰지만 겉으로 쉽게 코딩하기 위해 쉬운 문법을 제공하는 방식

⇒ [새로운 인스턴스를 만드는 방법](https://alex-dh.tistory.com/1)

객체는 일반적인 함수를 정의하듯 만드는데 그냥 실행하는 것이 아닌 new 키워드를 써서 만든다.

<mark style='background-color: #dcffe4'>✷ 일반적인 함수에 new 연산자를 붙여 호출하면 해당 함수는 생성자 함수로 동작한다.</mark>

<mark style='background-color: #dcffe4'>✷ new와 함께 생성자 함수를 호출하는 경우, 생성자 함수 내부의 this는 생성자 함수에 의해 생성된 인스턴스를 가리킴.</mark>

⇒ 함수의 맨 앞글자가 대문자인 함수를 생성자 함수라고 암묵적으로 정의한다.(일반 함수에 new 연산자를 붙이는 것이 아님)

⇒ 클래스를 만드는 암묵적인 규칙
<mark>클래스는 대문자, 일반명사</mark>로 만들고 <mark style='background-color: #ffdce0'>일반적인 함수는 적절한 동사 포함 소문자로 시작하도록 만듦.</mark>

ex)

```js
function Drink(color) {
  // 클래스
  let coffee = new Drink("brown");
  let ade = new Drink("orange");
  let tea = new Drink("green");
  // new 키워드가 붙은 모든 것들은 instances
}
```

즉시 객체를 만들기 위한 생성자 함수가 실행되며(클래스는 객체를 만들기 위한 생성자 함수를 포함한다), 변수에 클래스의 설계를 꼭 닮은 새로운 객체, 즉 인스턴스가 할당된다.

각각의 인스턴스는 클래스(Drink)의 고유한 속성과 메소드를 갖게 된다.

(객체 내에는 "데이터와 기능이 함께 있다"는 원칙에 따라 메소드와 속성이 존재한다)

‣ 속성: 객체 내부에 있는 값

‣ 메소드: 객체에 딸린 함수

✷ [constructor(생성자)가 하는 일](https://joonyon.tistory.com/24)

‣ 클래스의 인스턴스 객체를 생성하는 역할

‣ 역할 객체를 생성할 때 항상 실행되는 것으로, 객체를 초기화해주기 위해 맨 처음 실행되는 메소드.

```js
class Drink {
  constructor(name, color) {
    <-- 생략 -->
  }
  setHot() {
  }
  setCold() {
  }
}
```

✷ 클래스를 만드는 새로운 문법, ES6(ECMAScript 6)

```js
// 1. ES5
function Drink(name, color) {
  <-- 인스턴스가 만들어질 때 실행되는 코드(=생성자(constructor) 함수) -->
}

// 2. ES6
class Drink {
  <-- 인스턴스가 만들어질 때 실행되는 코드(=생성자(constructor) 함수) -->
  constructor(name, color) {
    this.name = name;
    this.color = color;
  }
}
// 생성자(constructor) 함수는 리턴값을 만들지 않는다
// ES6를 더 자주 쓰기 때문에 이 패턴에 익숙해질 것
```

✷ constructor 매개변수를 써주지 않으면 자동으로 생성됨.

③ constructor: 인스턴스가 초기화될 때 실행하는 생성자 함수

④ this: 인스턴스 객체. 객체 내의 메소드에서 객체가 가진 속성을 사용하고 싶을 때 사용하는 키워드.

함수가 실행될 때 해당 스코프마다 생기는 고유한 실행 context.

<mark>new 키워드로 생성했을 때는 해당 인스턴스가 바로 this의 값이 됨.</mark>

parameter로 넘어온 브랜드, 이름, 색상 등은 인스턴스 생성 시 지정하는 값이며,

<mark style='background-color: #dcffe4'>this에 할당한다는 것</mark>은 <mark style='background-color: #dcffe4'>만들어진 인스턴스에 해당 매개 변수(브랜드, 이름, 색상)를 부여하겠다</mark> 라는 의미.

✷ 인스턴스에서의 사용

```js
let coffee = new Drink("latte", "brown");
latte.color; // 'brown'
latte.setHot(); // 라떼를 뜨겁게 한다

let ade = new Drink("orangeade", "orange");
ade.name; // 'orangeade'
ade.setCold(); // 에이드를 차갑게 한다
```

✷ 이렇게 외우기

![](https://blog.kakaocdn.net/dn/bgAQdq/btrnCQIen22/kU3AM2BaSO6HAK0K7FyPUk/img.png)

(ES5)

![](https://blog.kakaocdn.net/dn/4U8Ma/btrnHRmdl22/eD4u359rEG11ptn6kn5avk/img.png)

(ES6 형태의 예시 사진)

‣ 실전 예제(배열)

```js
let arr = new Array("coffee", "tea", "ade");
arr.length; // 3
arr.push("cocktail"); // 새 엘리먼트 추가
```

**<mark>arr(배열)을 정의하는 것은 Array의 인스턴스를 만들어내는 것과 동일하다.</mark>**

따라서 new Array("coffee", "tea", "ade")의 방식으로도 배열을 만들 수 있다.

✷ 배열 메소드를 배웠을 때 메소드들이 대부분 Array.prototype.메소드명으로 표기되어 있는 이유는 모든 메소드들이 클래스의 원형 객체(prototype)에 정의되어 있기 때문이다.

## 2-1. 객체 지향 프로그래밍의 네 가지 특성

① 캡슐화(Encapsulation)

‣ 속성(데이터)과 메소드(기능)들을 하나에 객체 안에 넣어 느슨하게 결합하여 묶는 것.

‣ 코드가 복잡하지 않게 만들고, 재사용성을 높인다.

⇒ 쉽게 얘기하면 캡슐 약은 안의 약 성분이 어떤 것인지는 모르지만 그게 캡슐인 것은 안다는 것.

✷ 느슨한 결합: 절차적 코드 작성이 아닌 코드가 상징하는 실제 모습과 닮게 코드를 모아 결합하는 것.

ex) 마우스 구동을 위한 전 과정을 곳곳에 적어두는 것이 아닌 마우스의 상태를 속성(property)으로 정하고 클릭, 이동을 메소드(method)로 정해서 코드만 보고도 인스턴스 객체의 기능을 상상할 수 있게 작성하는 것.

✷ 은닉화(hiding): 내부 데이터 / 내부 구현이 외부로 노출되지 않도록 만드는 것.

즉, 디테일한 구현 / 데이터는 숨기고 객체 외부에서 필요한 메소드(동작)만 노출시켜야 한다.

은닉화의 특징을 살려서 코드를 작성하면 객체 내 메소드의 구현만 수정하고, 노출된 메소드를 사용하는 코드 흐름은 바뀌지 않도록 만들 수 있다.

(반면 절차적 코드의 경우 데이터의 형태가 바뀔 때 코드의 흐름에 큰 영향을 미쳐 유지보수가 어렵다. 더 엄격한 클래스는 속성의 직접적인 접근을 막고 설정하는 함수(setter), 불러오는 함수(getter)를 철저하게 나누기도 한다)

② 추상화(Abstraction)

‣ 내부 구현은 복잡한데 실제로 노출되는 부분은 단순하게 만듦.

‣ 코드가 복잡하지 않게 만들고, 단순화된 사용으로 인해 변화에 대한 영향을 최소화한다.

ex)

스마트폰이라는 객체 안에 스피커와 마이크 등등의 내부 구현 ⇒ 실사용 시 내부 구현에 대한 존재를 생각하지 않고 스마트폰을 들어 그에 해당하는 아이콘을 터치하는 것만으로도 충분히 사용 가능함.

‣ 추상화를 통한 인터페이스 단순화 가능.

→ 인터페이스: 클래스 정의 시 메소드와 속성만 정의한 것.

→ 너무 많은 기능 노출이 되지 않아 예기치 못한 사용상의 변화가 일어나지 않도록 만들 수 있음.

✷ 캡슐화와 추상화의 차이

‣ 캡슐화: 코드나 데이터의 은닉에 포커스가 맞춰져 있음

‣ 추상화: 클래스를 사용하는 사람이 필요하지 않은 메소드 등을 노출시키지 않고, 단순한 이름으로 정의하는 것에 포커스가 맞춰져 있음.

③ 상속(Inheritance) :불필요한 코드를 줄여 재사용성을 높인다. 부모 클래스의 특징을 자식 클래스가 물려받는 것.

→ 더 정확하게는 '기본 클래스(base class)의 특징을 파생 클래스(derive class)가 상속받는다' 이다.

ex)

```js
class Human {
  constructor(name, gender, age) {
    // 속성
    this.name = name;
    this.gender = gender;
    this.age = age;
  }
  sleep() {
    // 메소드
  }
  eat() {
    // 메소드
  }
}
```

추가로 학생이라는 클래스를 작성할 때, 사람 클래스의 속성과 메소드를 재구현하는 것은 비효율적이다.

학생의 본질은 결국 사람이기 때문에 상속을 이용하여 학생 클래스는 사람 클래스를 상속받을 수 있다.

학생은 추가적으로 학습 내용, 공부하다와 같은 속성 / 메소드를 추가한다.

```js
class Student {
  constructor(name, gender, age, learning subject) { // learning subject라는 속성 추가
    // 생략 //
  }
  sleep() {
  }
  eat() {
  }
  learn() { // learn이라는 메소드 추가
  }
}
```

④ 다형성(Polymorphism)

→ 다양한 형태를 가질 수 있다.

→ 동일한 메소드에 대해 조건문(if, else if) 대신 객체의 특성에 맞게 달리 작성하는 것이 가능해진다.

인스턴스는 클래스로부터 파생된 것. 엄밀하게는 중복 클래스로부터 남은 자식 클래스들이 부모 클래스로부터 상속받아 다양한 형태로 쓸 수 있다(=오버라이딩)

```js
// 다형성의 예시 코드

class Cafe {
  constructor() {
    this.menu = "Vanilla Latte";
    this.price = 5800;
  }
  taste() {
    return "Mmmmm yummy!";
  }
}

const cafe = new Cafe();
console.log(cafe);
// ▾ Cafe {menu: 'Vanilla Latte', price: 5800}
// ‣ menu: "Vanilla Latte"
// ‣ price: 5800
// [[Prototype]]: Object

class Casher extends Cafe {
  constructor() {
    super();
    this.menu = "Americano";
    this.price = 3000;
    this.color = "brown";
  }
}

const casher = new Casher();
casher.taste();
// "Mmmmm yummy!"
```

```js
class Cafe {
  constructor() {
    this.menu = "Vanilla Latte";
    this.price = 5800;
  }
  taste() {
    return "Mmmmm yummy!";
  }
}

const cafe = new Cafe();
console.log(cafe);
// ▾ Cafe {menu: 'Vanilla Latte', price: 5800}
// ‣ menu: "Vanilla Latte"
// ‣ price: 5800
// [[Prototype]]: Object

class Casher extends Cafe() {
  constructor() {
    super();
    this.menu = "Americano";
    this.price = 3000;
    this.color = "brown";
  }
  taste() {
    return "This is bitter sweet";
  }
}

const casher = new Casher();
casher.taste();
// "This is bitter sweet"
```

```js
class Cafe {
  constructor() {
    this.menu = "Vanilla Latte";
    this.price = 5800;
  }
  taste() {
    return "Mmmmm " + "this.menu" + "tastes good";
  }
}

class Casher extends Cafe() {
  constructor() {
    super();
    this.menu = "Americano";
    this.price = 3000;
    this.color = "brown";
  }
  taste() {
    return super.eat() + "and nice!";
  }
}

const casher = new Casher();
casher.taste();
// "Mmmmm Vanilla Latte tastes good and nice!"
```

부모에게서 상속받아 다양한 형태를 만들 수 있다.

또다른 예시)

HTML 엘리먼트에서 Textarea, Select, Checkbox 등에 render라는 이름을 가진 메소드가 있다고 할 때, 이들의 공통 부모인 HTML Element라는 클래스에 render라는 메소드를 만들고 상속을 받게 할 수 있다.

이 때, 다형성의 핵심은 같은 이름을 가졌더라도 메소드가 조금씩 다르게 작동한다는 것이다.

Textarea는 가로로 긴 네모 박스와 커서가 있는 형태, Select는 박스를 누를 때 선택지가 나오도록 하는 형태.

✷ 언어 자체에서 다형성을 제공하지 않는다면 기본(부모) 클래스에 종류별로 분기를 시켜서 하나하나 다르게 만들거나 각각의 자식 클래스에 별도의 각기 다른 render 함수를 만들 수도 있지만 엘리먼트라는 클래스의 본질상 "화면에 뿌린다(render)" 는 개념은 부모가 갖고 있는 것이 합리적이다.

## 3. 클래스와 프로토타입

자바스크립트는 프로토타입(=원형 객체) 기반 언어(prototype-based language)이다.

✷ prototype(프로토타입): 모델의 청사진을 만들 때 쓰는 원형 객체(original form).

프로토타입에는 constructor와 메소드가 함께 포함되어 있으나, 메소드를 정의하지 않으면 프로토타입에는 constructor만 들어간다.

```
__proto__ === prototype, __proto__때문에 프로토타입 체이닝이 가능함.
⇒ 메소드들은 각각의 섬이고 프로토타입은 그 섬을 연결해주는 다리 역할이다.
```

```
✷ __proto__ (= 프로토타입 링크, Prototype Link): 모든 객체에 존재하는 레퍼런스 속성이자 객체의 원형을 참조한다.

객체가 생성될 때 프로토타입이 결정되며 사용자가 임의로 변경할 수 있다. 사용자가 임의로 동적으로 변경하는 특징을 사용해 상속을 구현할 수 있다.

__proto__를 이용하면 부모 클래스의 프로토타입, 혹은 '부모의 부모 클래스'의 프로토타입을 탐색할 수 있다.
```

ex)

```js
class Cafe {
  constructor() {
    this.menu = "Vanilla Latte";
    this.price = 5800;
    }
    taste() {
      return "Mmmmm " + "this.menu" + "tastes good";
      }
}

class Casher extends Cafe() {
  constructor() {
    super();
    this.menu = "Americano";
    this.price = 3000;
    this.color = "brown";
    }
    taste() {
      return super.eat() + "and nice!";
    }
}

const casher = new Casher();
bee.eat();
// Mmmmm Vanilla Latte tastes good and nice!

cahser.**proto**
// ‣ Cafe {constructor: ⨍, taste: ⨍}

Casher.prototype === casher.**proto**
// true

const cafe = new Cafe();

Cafe.prototype
// ▾ {constructor: ⨍, taste: ⨍}
// ‣ constructor: class Cafe
// ‣ taste: ⨍ taste()
// [[Prototype]]: Object

Cafe.prototype === cafe.**proto**
// true

Cafe.prototype === Cafe
// false
```

✷ 새로운 인스턴스를 만드는 메소드: Object.create() ⇒ 주어진 객체를 프로토타입 객체로 삼아 새로운 객체를 생성하는 메소드.

ex)

```js
var person2 = Object.create(person1);
```

person2는 person1을 프로토타입 객체로 삼는다.

```
person2.__proto__
```

① Human이라는 클래스와 인스턴스, 프로토타입의 관계

✷ [instantiation](https://velog.io/@yhe228/instantiation-pattern-%EC%9E%A5%EB%8B%A8%EC%A0%90) = 인스턴스 만들기

![](https://blog.kakaocdn.net/dn/dGkh6G/btrnDHraNuA/zZfbKkRfJEs4Tsxm42aHHK/img.png)

```js
class Human {
  constructor(name, age) {
    this.name = name;
    this.age;
  }
  sleep() {
    return `${this.name}이(가) 잠을 잡니다.`
  }
}

const steve = new Human('Steve', 20) // instantiation // 인스턴스 만들기

console.dir(steve)
// ▾ Human
// age: 20
// name: "Steve"

// ▾ [[Prototype]]: Object(=== double under proto, dunder proto)
// constructor: class Human
// sleep: 𝑓 sleep()
// [[Prototype]]: Object

steve.sleep();
// 'steve이(가) 잠을 잡니다.'
steve.__proto__.sleep;
𝑓 sleep() { return `${this.name}이(가) 잠을 잡니다.` }
```

② Array(배열) 클래스와 인스턴스, 프로토타입의 관계

![](https://blog.kakaocdn.net/dn/oSzn9/btrnC2bdWKF/Y9WvUYhd05Kt47nouor750/img.png)

✷ 모든 array에 toString()을 쓸 수 있는 이유: array 자체가 new Array로 만들어지는 것이기 때문에 prototype이 상속되어 toString()을 쓸 수 있다.

## 4. 프로토타입 체인(prototype chain)

```
특정 객체의 속성 / 메소드에 접근 시 현재 객체에 해당 속성이 존재하지 않는다면 __proto__가 가리키는 링크를 따라 부모 역할을 하는 프로토타입 객체의 속성 / 메소드를 차례대로 검색하는 것.
```

```js
class Human {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sleep() {
    console.log(`${this.name}은 잠에 들었습니다`);
  }
}

let kimcoding = new Human("김코딩", 30);

Human.prototype.constructor === Human; // true
Human.prototype === kimcoding.__proto__; // true
Human.prototype.sleep === kimcoding.sleep; // true
```

→ 모든 객체들이 메소드와 속성들을 상속받기 위한 템플릿으로써 프로토타입 객체(prototype object)를 가진다.

프로토타입 객체도 또다시 상위 프로토타입 객체로부터 메소드와 속성을 상속 받을 수도 있고 그 상위 프로토타입 객체도 마찬가지이다. 이를 프로토타입 체인이라 부른다.

⇒ 다른 객체에 정의된 메소드와 속성을 한 객체에서 사용할 수 있도록 하는 근간이다.

⇒ 상속되는 속성과 메소드들은 각 객체가 아니라 객체의 생성자의 prototype이라는 속성에 정의되어 있다.

JavaScript에서는 객체 인스턴스와 프로토타입 간에 연결이 구성되며

이 연결을 따라 프로토타입 체인을 타고 올라가며 속성과 메소드를 탐색한다.

```
(많은 브라우저들이 생성자의 prototype 속성에서 파생된 __proto__ 속성으로 객체 인스턴스에 구현하고 있다.)
```

```
‣ 자바스크립트는 특정 객체의 속성 / 메소드에 접근할 때 객체 자신의 것뿐만 아니라
__proto__가 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 속성 / 메소드를 접근할 수 있다.

⇒ JavaScript에서는 객체 인스턴스와 프로토타입 간에 연결이 구성되며,
(많은 브라우저들이 생성자의 prototype 속성에서 파생된 __proto__ 속성으로 객체 인스턴스에 구현하고 있다.)

이 연결을 따라 프로토타입 체인을 타고 올라가며 속성과 메소드를 탐색한다.
```

‣ 모든 프로토타입 체이닝의 종점은 Object.prototype이다.

‣ 하위 객체는 상위 객체의 속성 / 메소드를 상속받는 것이 아닌 공유한다.

‣ **해당 객체에 없는 속성 / 메소드를 접근할 때 프로토타입 체이닝이 일어난다.**

✷ ECMAScript 2015부터는 Object.getPrototypeOf(obj) 함수를 통해 **객체의 프로토타입 객체에 바로 접근할 수 있게 되었다.**

‣ <mark>상속을 자바스크립트에서 구현할 때는 프로토타입 체인을 사용한다.</mark>

학생(Student)과 사람(Human)이라는 클래스가 각각 존재한다고 가정할 때, 클래스 Human의 메소드와 속성을 객체로 구현한 예시이다.

```js
// 클래스 Human의 속성과 메소드

let harvey = new Human("하비", "29");

// 속성
harvey.age;
harvey.gender;

// 메소드
harvey.eat();
harvey.sleep();
```

학생은 학생이기 이전에 사람이기 때문에 클래스 Student는 Human의 기본적인 메소드를 상속받을 수 있다. 하지만 학생은 일반적인 사람의 특징에 추가적인 특징이 필요하다.

```js
// 클래스 Student의 속성과 메소드

let haley = new Student("헤일리", 21);

// 속성
haley.grade;

// 메소드
haley.learn();
```

위 예시에서 나타나는 헤일리는 Student이다. 헤일리가 학생이라 age, gender와 같은 속성이 존재하지 않거나 sleep(), eat() 메소드를 사용할 수 없는 것은 아니다.

**Student는 Human의 특징을 그대로 물려받는다.**

이렇게 속성과 메소드를 물려주는 클래스를 부모 클래스(여기서는 Human), 속성과 메소드를 물려받는 클래스를 자식 클래스(여기서는 Student), 그리고 이 과정을 상속이라고 한다.

✷ 프로토타입 체인에서 한 객체의 메소드와 속성들이 다른 객체로 복사되는 것이 아님. 체인을 타고 올라가며 접근하는 것.

## 4-1. super와 extends를 이용한 상속

[<font color="blue">참고링크</font>](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Inheritance#ecmascript_2015_%ED%81%B4%EB%9E%98%EC%8A%A4)

① Human 클래스에 일반적인 사람이 가질 만한 특성들을 나열한다.

```js
// 클래스 Human의 속성과 메소드

class Human {
  constructor(first, last, age, gender, interests) {
    this.name = {
      first,
      last,
    };
    this.age = age;
    this.gender = gender;
    this.interests = interests;
  }
  greeting() {
    console.log(`Hi! I'm ${this.name.first}`);
  }
  farewell() {
    console.log(`${this.name.first} has left the building.`);
  }
}
// greeting()과 farewell()은 멤버 메소드
// 클래스의 메소드는 생성자 다음에 아무 메소드나 추가할 수 있다

// new 연산자로 객체 인스턴스 생성 가능
let harvey = new Human("Harvey", "Nichols", 29, "male", ["Smuggling"]);
harvey.greeting();
// Hi! I'm Harvey

let haley = new Human("Haley", "Johnson", 21, "female"["Government"]);
haley.farewell();
// Haley has left the building.
```

② Person을 class 문법으로 상속받아 Student 클래스를 만들었다. 이 작업을 하위 클래스 생성이라 부른다.

하위 클래스를 만들려면 자바스크립트에서 extends 키워드를 통해 상속받을 클래스를 명시한다.

```js
// extends를 이용한 Student를 Human 안에 상속하기

class Student extends Human {
  constructor(first, last, age, gender, interests, subject, grade) {
    this.name = {
      first,
      last,
    };

    this.age = age;
    this.gender = gender;
    this.interests = interests;

    // subject와 grade는 Student에 특정된 속성
    this.subject = subject;
    this.grade = grade;
  }
}
```

③ constructor()에서 첫 번째로super() 연산자를 정의하면 코드를 조금 더 읽기 쉬워진다.

이는 상위 클래스의 생성자를 호출하며 super()의 매개변수를 통해 상위 클래스의 멤버를 상속받을 수 있는 코드이다.

✷ [super(); 를 호출해야 하는 이유](https://ko.javascript.info/class-inheritance)

만약 super를 호출하지 않으면

<font color="red">ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor</font>

(상속 클래스의 생성자에선 반드시 super(...)를 호출해야 하는데, super(...)를 호출하지 않아 에러가 발생했습니다. super(...)는 this를 사용하기 전에 반드시 호출해야 합니다.)

라는 에러가 나온다.

먼저, 상속 클래스의 생성자가 호출될 때 어떤 일이 일어나는지 알아본다.

자바스크립트는 '상속 클래스의 생성자 함수(derived constructor)'와 그렇지 않은 생성자 함수를 구분한다.

상속 클래스의 생성자 함수엔 특수 내부 프로퍼티인 [[ConstructorKind]]:"derived"가 이름표처럼 붙는다.

일반 클래스의 생성자 함수와 상속 클래스의 생성자 함수 간 차이는 new와 함께 드러난다.

‣ 일반 클래스가 new와 함께 실행되면, 빈 객체가 만들어지고 this에 이 객체를 할당한다.

반면, 상속 클래스의 생성자 함수가 실행되면, 일반 클래스에서 일어난 일이 일어나지 않는다.

‣ 상속 클래스의 생성자 함수는 빈 객체를 만들고, this에 이 객체를 할당하는 일을 부모 클래스의 생성자가 처리해주길 기대한다.

이런 차이 때문에 상속 클래스의 생성자에선 super를 호출해 부모 생성자를 실행해 주어야 하며, 그렇지 않으면 this가 될 객체가 만들어지지 않아 에러가 발생한다.

```js
// super와 extends를 이용한 상속

class Student extends Human {
  constructor(first, last, age, gender, interests, subject, grade) {
    super(first, last, age, gender, interests);

    // subject와 grade는 Student에 특정된 속성
    this.subject = subject;
    this.grade = grade;
  }
}
```

④ Student의 인스턴스를 생성하면 의도한 대로 이제 Student와 Person 양 쪽의 메소드와 속성을 사용할 수 있다.

```js
let emily = new Student(
  "Emily",
  "Johnson",
  25,
  "female",
  ["religion"],
  "theology",
  3
);

emily.greeting(); // Hi! I'm Emily
emily.farewell(); // Emily has left the building.
emily.age; // 25
emily.subject; // theology
```
