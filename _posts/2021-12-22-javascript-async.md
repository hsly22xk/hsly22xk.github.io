---
layout: single
title: "D+34(35) 비동기(비동기 호출, 비동기 자바스크립트, 콜백, promise, async, await, 타이머API), Node.js 모듈 사용법, fetch API, Event Loop"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

비동기에 관련된 내용 정리 & 이벤트 루프.

## 1. 동기(synchronous)와 비동기(asynchronous)

① blocking: 하나의 작업이 끝날 때까지 이어지는 작업을 막는 것. 요청에 대한 결과가 동시에 일어난다. ⇒ 동기(synchronous)적이다(시작 시점과 완료 시점이 같은 상황).

✷ 클라이언트(client)와 서버(server)

(일단은 간단하게 정리해놓은 것. 자세한 것은 뒤에)

```
‣ 클라이언트: 서버로 접속하는 컴퓨터. 보통 우리가 사용하는 컴퓨터라고 생각할 수 있음.
‣ 서버: 무언가(서비스, 리소스 등)를 제공하는 컴퓨터. 웹 서버나 게임 서버 등.
```

✷ 동기적이다(synchronous)

클라이언트는 어떠한 요청을 서버에 보내고, 서버가 그 요청을 받아 일처리를 위해 데이터베이스에서 데이터를 꺼내오기도 하고, 꺼내온 데이터를 가공하기도 하는 과정을 거치고, 클라이언트에게 응답을 줄 준비를 한다.

클라이언트는 응답이 오는 순간 데이터를 받아 원래 하려던 일들을 처리함.⇒ 서버가 요청을 받아 모든 것을 끝내고 응답을 줄 때까지 클라이언트는 아무것도 하지 않음.

ex) blocking의 예시

```
거스가 운영하는 주점에서 셰인이 먼저 도착하여 피자를 시켰고, 레아는 그 뒤에 도착하여 샐러드를 시키려 한다.
하지만 주점의 사정 상 피자가 나와 셰인이 받을 때까지 레아를 비롯한 나머지 사람들은 주문조차 할 수 없다.
그러므로 레아는 셰인이 주문한 피자가 나와야지만 원하는 메뉴를 주문할 수 있다.
셰인의 피자 주문 완료 시점과 레아의 샐러드 주문 시작 시점이 같다.
```

⇒ 셰인의 피자가 나와 셰인이 피자를 받을 때까지 다른 주문을 받을 수 없는 것이 blocking, 셰인의 피자 주문 완료 시점과 레아의 샐러드 주문 시작 시점이 같은 것을 동기적이다 라고 한다.

동기적으로 작동하는 주문 과정을 수도코드로 작성한다면

```
1. 셰인이 피자를 주문한다.
2. 주문을 받은 거스가 피자를 만든다.
3. 거스가 셰인에게 피자를 전달한다.
4. 레아가 샐러드를 주문한다.
--> 레아는 셰인이 피자를 받을 때까지 주문도 못하고 대기열에 있어야 한다
5. 주문을 받은 거스가 샐러드를 만든다.
6. 거스가 레아에게 샐러드를 전달한다.
```

이것을 동기 함수로 바꾼다면

```js
// 동기적으로 딜레이 시켜주는 함수
// 현재 시각과 시작 시각을 비교하며 ms 범위 내에서 무한 루프를 도는 blocking 함수
function waitSync(ms) {
  var start = Date.now();
  var now = start;
  while (now - start < ms) {
    now = Date.now();
  }
}

function eat(person, menu) {
  console.log(`${person}은 ${menu}를 먹습니다.`);
}

function orderMenuSync(menu) {
  console.log(`${menu}가 접수되었습니다.`);

  // 2초 동안 blocking됨
  waitSync(2000);
  return menu;
}

// 대기열
let customers = [
  {
    name: "Shane",
    request: "피자",
  },
  {
    name: "Leah",
    request: "샐러드",
  },
];

// call synchronously
// 손님이 어떠한 메뉴를 주문하고 그 메뉴가 나오면 그 때 나온 메뉴를 먹음
// 이 함수 한 번 실행에 총 4초가 걸림
customers.forEach(function (customer) {
  let food = orderMenuSync(customer, request);
  eat(customer.name, menu);
});
```

이것의 콘솔 로그 결과는

```
1. 피자가 접수되었습니다.
2. Shane는 피자를 먹습니다.
3. 샐러드가 접수되었습니다.
4. Leah은 샐러드를 먹습니다.
(넘버링은 순서 편의를 위한 임의의 넘버링. 실제 콘솔에선 내용만 나옴.)
```

②. non-blocking: 작업이 끝나지 않아도 이어지는 작업을 할 수 있음. 요청에 대한 결과가 동시에 일어나지 않는다.

⇒ 비동기(asynchronous)적이다(시작 시점과 완료 시점이 같을 필요가 없음). ⇒ 요청에 대한 결과가 이벤트에 의해 이벤트 핸들러가 실행된다.

✅ 특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성을 말한다.

✷ 비동기적이다(asynchronous)

클라이언트에서 앞서 언급한 동일한 요청을 보내고 서버는 동일한 작업을 한다. 그동안 클라이언트는 기다리지 않고 원래 하려던 작업을 하거나 중간에 다른 요청을 받으면 처리한다.

그 와중에 서버에서 작업을 마치고 응답을 보내면 해당 응답을 받고 무언가를 한다.

ex) non-blocking의 예시

```
1. 셰인이 피자를 주문한다.
--> 요청에 blocking이 없음
① 주문을 받은 거스가 피자를 만든다.
② 피자가 완성되면 셰인을 부른다.
③ 피자를 셰인에게 전달한다.
--> 응답은 비동기적으로 이루어진다

2. 레아가 샐러드를 주문한다.
   --> 요청에 blocking이 없음

① 주문을 받은 거스가 샐러드를 만든다.
② 샐러드가 완성되면 레아를 부른다.
③ 레아에게 샐러드를 전달한다.
--> 응답은 비동기적으로 이루어진다

==> 즉, 요청에 blocking 없이 모든 주문을 받아들인다.
==> 여기서 '완성되면' 처럼 무언가 준비가 되었을 때(트리거가 생길 때)를 이벤트라고 한다.
==> 여기서 '부른다' 라는 것은 이벤트에 대한 핸들러, 즉 callback이다.
```

이를 다시 비동기 함수로 바꾸어 쓴다면

```js
function waitSync(callback, ms) {
  // 특정 시간 이후 callback 함수가 실행되게끔 하는 브라우저 내장 기능
  setTimeout(callback, ms);
}

function eat(person, menu) {
  console.log(`${person}은 ${menu}를 먹습니다.`);
}

// 대기열
let customers = [
  {
    name: "Shane",
    request: "피자",
  },
  {
    name: "Leah",
    request: "샐러드",
  },
];

function orderMenuAsync(menu, callback) {
  console.log(`${menu}가 접수되었습니다.`);
  waitSync(function () {
    callback(menu);
  }, 2000); // 2초 딜레이 시킴
}

// call synchronously
customers.forEach(function (customer) {
  orderMenuSync(customer.request, function (menu) {
    eat(customer.name, menu);
  });
});
```

이것의 콘솔 결과는

```
1. 피자가 접수되었습니다.
2. 샐러드가 접수되었습니다.

(4초 딜레이 후 주문에 대한 콜백이 이루어짐)

3. Shane은 피자를 먹습니다.
4. Leah는 샐러드를 먹습니다.
```

## 2. 비동기 함수의 전달 패턴

① callback 패턴

```js
let request = "pizza";
orderMenuAsync(request, function (response) {
  // response --> 주문한 메뉴 결과
  // function(response)가 콜백 함수
  eat(response);
});
```

② 이벤트 등록 패턴

```js
let request = "pizza";
orderMenuAsync(request).onready = function (response) {
  // response --> 주문한 메뉴 결과
  eat(response);
};
```

### 2-1. 비동기의 주요 사례

‣ DOM Element의 이벤트 핸들러

- 마우스, 키보드 입력 등(onclick, onkeydown)

- 페이지 로딩(DOMContentLoaded 등)

⇒ 어떠한 이벤트가 일어났을 때

‣ 타이머

- 타이머 API(setTimeout 등)

- 애니메이션 API(requestAnimationFrame)

‣ 서버에 자원 요청 및 응답

- fetch API: 작성 되어 있는 서버를 이용할 때 특정 서버에 URL로 요청하여 사용할 수 있도록 해주는 것.

- AJAX(XHR)

✷ 비동기적으로 작동되었을 때 효율적인 작업

‣ 백그라운드 실행, 로딩 창 등의 작업

‣ 인터넷에서 서버로 요청을 보내고 응답을 기다리는 작업

‣ 큰 용량의 파일을 로딩하는 작업

⇒ Node.js는 non-blocking하고 비동기적(asynchronous)으로 작동하는 런타임으로 개발했다. JavaScript의 비동기적 실행(Asynchonous execution)이라는 개념은 웹 개발에서 특히 유용하다.

## 3. 비동기 자바스크립트(Async Javascript)

[Javascript 비동기 동작 과정 개념](https://github.com/codestates/agora-states/discussions/2192#discussioncomment-1897656)

### ① 콜백(callback)

비동기를 제어할 수 있는 방법(A way to handle async)

ex)

```js
const printString = (string) => {
  setTimeout(
    () => {
      console.log(string)
    },
    Math.floor(Math.random() * 100) + 1;
  )
}

const printAll = () => {
  printStirng("A")
  printStirng("B")
  printStirng("C")
}
printAll();
// 순차적으로 제어하지 않는 랜덤한 순서로 문자열이 찍혀 나온다.
```

![](https://blog.kakaocdn.net/dn/6T1Ri/btroxBwbbmH/64sIk2UFCtNYljok1PB9wk/img.png)

위에서의 코드처럼 A,B,C를 넣었다고 해서 순서대로 A, B, C가 callback queue에 들어가는 것은 아니다.

그래서 A가 끝나면 B, B가 끝나면 C가 들어갈 수 있도록 순서를 제어하고 싶다면

```js
const printString = (string, callback) => {
  setTimeout(
    () => {
      console.log(string);
      callback() // 받은 함수 실행
    },
    Math.floor(Math.random() * 100) + 1;
  )
}

const printAll = () => {
  printString("A", () => { // 콜백을 받아 넘김
    printString("B", () => { // 콜백 함수 안에서 B를 실행하고 콜백 함수를 다시 실행함
      printString("C", () => {}) // 이 콜백 안에서 C를 실행함
    })
  })
}
printAll();
// A
// B
// C
```

✷ 콜백의 에러 핸들링(Callback error handling Design) & Usage ⇒ **callback은 마지막 인자(err, data)를 호출하며, 자동으로 들어간다.**

```js
const somethingGonnaHappen = (callback) => {
  // 무언가 일어나는 걸 기다리는 동안
  waitingUntilSomethingHappens();

  // 만약 모든 것이 잘 되었으면
  // callback 함수의 인자에 앞에는 null, 뒤에는 something을 넣어줌
  // 여기서 something은 기다린 결과값
  // 앞에 쓴 null은 err, something은 data
  if (isSomethingGood) {
    callback(null, something);
  }

  // 만약 잘 되지 않았으면
  // callback 함수의 인자에 앞에 something, 뒤에는 null을 넣어줌
  if (isSomthingBad) {
    callback(something, null);
  }
};

// 여기서 (err, data)가 위에 쓴 callback 함수의 인자
// err와 data로 받아올 수 있음
somethingGonnaHappen((err, data) => {
  // 만약 에러가 발생하면
  if (err) {
    console.log("ERR!!");
    return;
  }

  // 에러가 발생하지 않으면 그대로 데이터를 리턴함
  return data;
});
```

하지만 계속 콜백을 쓰면 많은 코드를 짜야 할 때 코드 가독성이 떨어지고 관리하기가 힘듦(callback HELL).

### ② Promise

콜백 체인을 다룰 수 있는 방법(How to deal with callback chain) → 하나의 클래스 같은 것.

[좀더 자세한 설명은 여기서](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/#%ED%94%84%EB%A1%9C%EB%AF%B8%EC%8A%A4-%EC%97%90%EB%9F%AC-%EC%B2%98%EB%A6%AC%EB%8A%94-%EA%B0%80%EA%B8%89%EC%A0%81-catch%EB%A5%BC-%EC%82%AC%EC%9A%A9)

[promise mdn문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[What is a Promise](https://velog.io/@cadenzah/What-is-a-Promise)

✅ Promise의 3가지 상태(states)

```
⇒ Promise의 상태: Promise의 처리 과정을 의미함.
⇒ new Promise()로 프로미스를 생성하고 종료될 때까지 3가지 상태 중 하나를 갖는다.
⇒ 프로미스가 대기(pending)에서 벗어나 이행 또는 거부된다면 프로미스가 처리(settled)됐다고 말한다.
```

```
‣ 대기(pending): 비동기 처리 로직이 아직 완료되지 않은 상태(이행하지도 거부하지도 않은 상태).
‣ 이행(fulfiled): 비동기 처리가 완료되어 프로미스가 결과값을 반환해준 상태(연산이 성공적으로 완료됨).
‣ 실패(rejected): 비동기 처리가 실패하거나 오류가 발생한 상태(연산이 실패함).
```

```js
// Promise라는 이름의 클래스로 인스턴스가 만들어짐
new Promise();

// 그 안에 resolve()라는 명령어를 통해 다음 액션으로 넘어가거나(Go to next action)
resolve();

// reject()라는 명령어를 통해 에러를 핸들링 할 수 있다(Handle Error)
reject();
```

ex) Promise Chaining의 예시

```js
const printString = (string) => {
  // callback 자체를 넣어주는 것이 아닌
  // Promise라는 새로운 클래스를 만들어 인스턴스를 만든 후
  // 그 안에 resolve와 reject라는 인자를 넣어 콜백 함수의 역할을 하게 한다.
  return new Promise((resolve, reject) => {
    setTimeout(
    () => {
      console.log(string);
      resolve()
      },
    Math.floor(Math.random() * 100) + 1;
    )
  })
}

const printAll = () => {
  printString("A")
  .then(() => { // printString("A")가 끝나면
    return printString("B") // printString("B")를 리턴한다.
  })
  .then(() => { // 이 printString("B")가 끝나면
    return printString("C") // printString("C")를 리턴한다.
  })
}
printAll();
// A
// B
// C
```

→ 첫 테스크(initial task)가 끝나면 .then()으로 다음 테스크(success task)를 이어서 진행할 수 있다.

→ reject()로 에러 처리가 되는 경우 .catch()를 이용해 마지막 체이닝(failure task)에서 에러 핸들링을 할 수 있다.

![](https://blog.kakaocdn.net/dn/cgrDo1/btroecSa839/UcxQJJu0ZXzZ9quEA66xEK/img.png)

⇒ <mark>기본적으로 promise chain은 예외가 발생하면 멈추고 chain의 아래에서 catch를 찾는다.</mark>

ex) 콜백 헬이 일어나는 것처럼 Promise Hell이 일어날 수 있는 예시

```js
function wakeUp() {
  return new Promise(resolve, reject) => {
    setTimeout(() => { resolve('1. I woke up') }, 100)
  })
}

function sitAndStudy() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('2. sit and study') }, 100)
  })
}

function eatLunch() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('3. eat Lunch') }, 100)
  })
}

function goToBed() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('4. go to bed') }, 100)
  })
}

wakeUp()
.then(data => {
  console.log(data);

  sitAndStudy()
  .then(data => {
    console.log(data);

    eatLunch()
    .then(data => {
      console.log(data);

      goToBed()
      .then(data => {
        console.log(data);
      });
    });
  });
});
```

ex) Promise Hell 방지를 위한 Promise Chaining(위의 예시 바꾸기)

```js
function wakeUp() {
  return new Promise(resolve, reject) => {
    setTimeout(() => { resolve('1. I woke up') }, 100)
  })
}

function sitAndStudy() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('2. sit and study') }, 100)
  })
}

function eatLunch() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('3. eat Lunch') }, 100)
  })
}

function goToBed() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('4. go to bed') }, 100)
  })
}

// 위에서의 코드와는 다르게 .then()함수 뒤에 return을 써줌
wakeUp()
.then(data => {
  console.log(data);
  return sitAndStudy();
})
.then(data => {
  console.log(data);
  return eatLunch();
})
.then(data => {
  console.log(data);
  return goToBed();
})
```

⇒ **.then() 함수 뒤에 return 처리**를 잘 해주면 다음에 이어가면서 확인할 수 있음.

### ③ Promise.all(iterable)

모든 프로미스가 이행될 때까지 기다렸다가 그 결과값을 담은 배열을 반환하는 메소드.

‣ 순회 가능한 객체에 주어진 모든 프로미스가 이행한 후, 혹은 프로미스가 주어지지 않았을 때 이행하는 Promise를 반환.

→ 매개변수: iterable, 배열과 같이 순회 가능한 객체.

‣ 이행: 반환한 프로미스의 이행 결과값은(프로미스가 아닌 값 포함) 매개변수로 주어진 순회 가능한 객체에 포함된 모든 값을 담은 배열.

→ 배열 내 모든 값의 이행(또는 첫 번째 거부)을 기다림.

→ 비동기적으로 이행하는 메소드이나, 주어진 순회 가능한 객체가 비어있는 경우 동기적으로 이미 이행한 프로미스를 반환.

→ 전달받은 모든 프로미스가 이미 이행되어 있거나 프로미스가 없는 경우 비동기적으로 이행하는 프로미스를 반환.

‣ 거부: 입력 값으로 들어온 주어진 프로미스 중 하나라도거부당하면(reject값을 반환하면) Promise.all()은 즉시 이행을 거부하며, 거부한 첫 번째 이유를 반환한다(Promise.all()의 실패 우선성) (promise 값들에 문제가 없을 때 promise가 아닌 값도 잘 처리하여 반환하여 준다).

‣ Promise.all()의 특징

→ 여러 개의 비동기 처리(순서 보장 X)를 병렬로 하고 싶을 때 사용

→ 여러 프로미스의 결과를 집계할 때 유용하게 사용.

일반적으로 다음 코드를 계속 실행하기 전에

서로 연관된 비동기 작업 여러 개가 모두 이행되어야 하는 경우에 사용된다.

ex1)

```js
const createRandomNumber1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});
const createRandomNumber2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});
const createRandomNumber3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});

// promise객체를 배열에 담아서 prosmie.all의 인자로 넣어주기
const promises = [
  createRandomNumber1,
  createRandomNumber2,
  createRandomNumber3,
];

Promise.all(promises).then((result) => console.log(result));
// result : [ 9, 1, 1 ]
```

ex2)

```js
// Promise.all()의 실패 우선성 예시

var p1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("하나"), 1000);
});
var p2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("둘"), 2000);
});
var p3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("셋"), 3000);
});
var p4 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("넷"), 4000);
});
var p5 = new Promise((resolve, reject) => {
  reject(new Error("거부"));
});

// .catch 사용:
Promise.all([p1, p2, p3, p4, p5])
  .then((values) => {
    console.log(values);
  })
  .catch((error) => {
    console.log(error.message);
  });

// 콘솔 출력값:
// "거부"
```

### ④ async await

[참고링크](https://kiwanjung.medium.com/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4)

→ 비동기 함수가 동기 함수처럼 작동하는 방식으로, 실제로는 Promise를 사용하여 결과를 리턴한다.

→ Promise를 동기식으로 코드를 순서대로 작성하는 것처럼 간편하게 작성을 도와주는 API.

⇒ async & await는 새롭게 추가된 것이 아닌 기존에 존재하는 Promise 위에 조금 더 간편한 API를 제공하는 것인데, 이를 syntactic sugar라고 한다. (ex. class)

⇒ Promise chaning을 계속 사용하다 보면 가독성이 떨어져서 async & await를 사용하면 읽기 좋은 코드를 작성할 수 있다.

```js
function wakeUp() {
  return new Promise(resolve, reject) => {
    setTimeout(() => { resolve('1. I woke up') }, 500)
  })
}

function sitAndStudy() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('2. sit and study') }, 400)
  })
}

function eatLunch() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('3. eat Lunch') }, 300)
  })
}

function goToBed() {
  return new Promise((resolve, reject) => {
    setTimeout(() => { resolve('4. go to bed') }, 200)
  })
}

// async await 함수를 사용함
// 함수 앞에 await을 붙여 일반 함수인 것 처럼 받아와 순차적으로 실행됨
// 제일 앞에 async()함수임을 표기해주어야만 가능함
const result = async() => {
  const one = await wakeUp();
  console.log(one);

  const two = await sitAndStudy();
  console.log(two);

  const three = await eatLunch();
  console.log(three);

  const four = await goToBed();
  console.log(four);
}
result();

// 순차적으로 코드가 실행된다
// 일어난다 -> 앉아서 공부한다 -> 점심을 먹는다 -> 잠자리에 든다 순서로 실행됨
```

✷ async()를 붙이지 않고 일반 함수에 바로 await을 붙이면 구문 오류 뜸

<font color="red">SyntaxError: await is only valid in async functions and the top level bodies of modules</font>

ex) Promise.all()메소드를 async await함수를 이용하여 쓴 예시

```js
const createRandomNumber1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});
const createRandomNumber2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});
const createRandomNumber3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve(Math.floor(Math.random() * 10)), 1000);
});

const promises = [
  createRandomNumber1,
  createRandomNumber2,
  createRandomNumber3,
];

async function handlePromises() {
  const result = [];
  for (let i = 0; i < promises.length; i++) {
    // async 함수 내에서 promise객체 앞에 await을 붙이면 동기적 처리 가능
    result.push(await promises[i]);
  }
  console.log(result); // [ 2, 8, 1 ]
}

// async 함수 실행
handlePromises();
```

### ⑤ 타이머 API

[**<mark>✷ API(Application Programming Interface)</mark>**](http://blog.wishket.com/api%EB%9E%80-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85-%EA%B7%B8%EB%A6%B0%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8/)

프로그램들이 서로 상호작용하는 것을 도와주는 매개체. 응용 프로그램에서 사용할 수 있도록 운영체제/프로그래밍언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스.

‣ setTimeout(callback, millisecond): 일정 시간 후에 함수를 실행함.

→ arg: 실행할 콜백 함수, 콜백 함수 실행 전 기다려야 할 시간(밀리초)

→ return value: 임의의 타이머 ID

```js
setTimeout(function () {
  console.log("1초 후 실행");
}, 1000);

// 123
```

‣ setInterval(callback, millisecond): 일정 시간의 간격을 가지고 함수를 반복적으로 실행함.

→ arg: 실행할 콜백 함수, 콜백 반복적으로 함수를 실행시키기 위한 시간 간격(밀리초)

→ return value: 임의의 타이머 ID

```js
setInterval(function () {
  console.log("1초마다 실행");
}, 1000);

// 345
```

‣ clearInterval(timerId): 반복 실행 중인 타이머 종료.

→ arg: 타이머 ID

→ return value: 없음.

```js
const timer = setInterval(function () {
  console.log("1초마다 실행");
}, 1000);

clearInterval(timer);
// 더 이상 반복 실행되지 않음
```

‣ clearTimeout(timeoutID): 이전에 설정된 시간 초과를 취소함(setTimeout()을 취소하는 역할)

→ arg: 취소하려는 시간 초과의 식별자.

```js
// 6초마다 updateClock()이 호출된다.
const timerId = setInterval(updateClock(), 6000);

// 60초 후에 clearTimeout()를 호출한다.
setTimeout(function () {
  // timerId의 반복 호출을 종료시킨다.
  clearTimeout(timerId);
}, 60000);
```

## 4. Node.js 모듈 사용법

### ① Node.js

비동기 이벤트 자바스크립트 런타임. 로컬 환경에서 자바스크립트를 실행할 수 있는 자바스크립트 런타임.

✷ 모듈: 어떤 기능을 조립할 수 있는 형태로 만든 부분.

fs(File System) 모듈: PC의 파일을 읽거나 저장하는 등의 일을 할 수 있게 도와줌.

### ② Node.js 내장 모듈 사용 방법

[‣ Node.js v14.17.0 Documentation](https://nodejs.org/dist/latest-v14.x/docs/api/)

개발자는 자신이 이해하는 범위만큼 모듈을 사용할 수 있다. 예를 들어, DNS에 대한 지식을 알고 있다면, DNS 모듈 사용법 문서에서 관련 메소드를 사용할 수 있다.

당장 DNS가 무엇인지 모를 수는 있지만, 파일 시스템 모듈은 파일을 읽거나 저장하는 기능을 구현할 수 있도록 돕는다.

메소드 목록을 살펴보면, 파일을 읽을 때에 쓸법한 메소드 이름을 찾을 수 있다.(물론, 처음부터 필요한 메소드를 정확하게 찾는 일은 쉽지 않다.)

→ 파일을 읽을 때: [readFile](https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_fs_readfile_path_options_callback)

→ 파일을 저장할 때: [writeFile](https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_fs_writefile_file_data_options_callback)

‣ 모든 모듈은 '모듈을 사용하기 위해 불러오는 과정'이 필요하다. 브라우저에서 다른 파일을 불러올 때에는 다음과 같이 script 태그를 이용했다.

```js
<script src="불러오고싶은_스크립트.js"></script>
```

Node.js 에서는 자바스크립트 코드 가장 상단에 require 구문을 이용하여 다른 파일을 불러온다.

```js
const fs = require("fs"); // 파일 시스템 모듈 불러오기
const dns = require("dns"); // DNS 모듈 불러오기

// 이제 fs.readFile 메소드 등 사용 가능
```

### ③ 3rd-party 모듈 사용 방법

‣ 써드 파티 모듈(3rd-party-module): 해당 프로그래밍 언어에서 공식적으로 제공하는 빌트인 모듈(built-in module)이 아닌 모든 외부 모듈을 일컬음.

```js
// 써드 파티 모듈 중 하나인 underscore 모듈을 다운로드 받기 위한 터미널 커맨드
npm install underscore

// require 구문을 통한 모듈 사용방법
const _ = require('underscore');
```

### ④ fs.readfile(path[, options], callback)

로컬에 존재하는 파일을 읽어오는 메소드로, 비동기적으로 파일 내용의 전체를 읽는다. 메소드 실행 시 인자 세 개를 넘길 수 있음.

→ path: 파일 이름을 인자로 넘길 수 있다.

네 가지 종류의 타입을 넘길 수 있지만 일반적으로 문자열(string)의 타입으로 넘긴다.

```js
/* /etc/passwd 라는 파일을 불러오는 예제  */
fs.readFile('/etc/passwd', ..., ...)
```

→ [,options]: 넣을 수도 있고 넣지 않을 수도 있는 선택적 인자(=대괄호).

객체 형태 또는 문자열로 넘길 수 있으며 문자열로 전달할 때는 인코딩을 전달함.

ex)

```js
let options = {
  encoding: 'utf8', // UTF-8이라는 인코딩 방식으로 연다
  flag: 'r' // 읽기 위해 연다
}

// /etc/passed 파일을 옵션을 사용하여 읽는다
fs.readFile('/etc/passwd', options, ...)
```

data에는 문자열이나 Buffer가 전달된다.

어떤 경우(=If no encoding is specified, then the raw buffer is returned.)에 문자열로 전달되는 것.

```js
import { readFile } from "fs";
readFile("/etc/passwd", "utf8", callback);
```

→ callback: 콜백 함수를 전달함. 파일을 읽고 난 후 비동기적으로 실행되는 함수.

```
err \<Error>
data \<string> | \<Buffer>
```

<mark>콜백 함수에는 두 가지 파라미터가 존재하는데, 에러가 발생하지 않으면 err는 null 이 되며, data(파일의 내용)에 문자열이나 Buffer라는 객체가 전달된다.</mark>

```js
// 메소드 fs.readFile로 파일의 데이터를 읽어 들이기

fs.readFile("test.txt", "utf8", (err, data) => {
  if (err) {
    throw err; // 에러를 던진다
  }
  console.log(data);
});
```

## 5. fetch를 이용한 네트워크 요청

### ① fetch API

[✷ using Fetch](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch)

URL로 요청하는 것을 가능하게 해주는 API. 특정 URL로부터 정보를 받아오는 역할을 함. ⇒ 과정이 비동기로 이루어지기 때문에, 경우에 따라 다소 시간이 걸릴 수 있다.

시간이 소요되는 작업을 요구할 경우에는 blocking이 발생하면 안 되므로, 특정 DOM에 정보가 표시될 때까지 로딩 창을 대신 띄우는 경우도 있다.

ex)

![](https://blog.kakaocdn.net/dn/bjFucb/btrorP3CMw1/e2rXzTwvKlYcTT3TZM0aB0/img.png)

시시각각 변하는 정보와, 늘 고정적인 정보가 따로 분리되어 있는 구성을 확인할 수 있다.

이 중에서 오늘의 날씨 / 뉴스가 동적으로 데이터를 받아와야 하는 정보이다.

이럴 때 많은 웹사이트에서는 해당 정보만 업데이트하기 위해 요청 API를 이용하는데, 여기서는 그중 대표적인 fetch API를 이용해 해당 정보를 원격 URL로부터 불러오는 경우이다.

### ② fetch API를 사용하는 방법

ex)

```js
// fetch API를 사용하여 데이터를 요청

let url =
  // "원격으로 요청하고 데이터를 받아올 수 있는 URL"
  fetch(url)
    // 자체적으로 json() 메소드가 있어, 응답을 JSON 형태로 변환시켜서 다음 Promise로 전달한다
    // fetch()가 완료되길 기다린 뒤에 실행
    .then((response) => response.json())

    // 콘솔에 json을 출력
    // response()가 완료되길 기다린 뒤에 실행
    .then((json) => console.log(json))

    // 에러가 발생한 경우, 에러를 띄운다
    // 이전 Promise 중에서 Rejected인 경우가 있을 때에만 실행
    .catch((error) => console.log(error));
```

## 6. Event Loop

{% include video id="8aGhZQkoFbQ" provider="youtube" %}

### ① 이벤트 루프의 역할

![](https://blog.kakaocdn.net/dn/cjpjnN/btrorOQ7ual/R6VZ3755RagzXy3w8tKzK1/img.png)

main() 함수가 콜 스택에 먼저 쌓이고, console.log('Hi');가 그 뒤에 쌓이면 web API인 cb(콜백) 함수가 web APIs에서 돌아간다.

돌아가는 동안 main() 함수와 console.log('Hi');가 끝나고 cb 함수는 task queue로 옮겨진다.

이벤트 루프는 콜 스택과 테스크 스택을 주시하면서 스택이 비워질 때까지 기다린다. 스택에 비어 있으면 큐에 있는 첫 번째 콜백을 스택에 쌓아 효과적으로 실행할 수 있게 해 준다.

console.log('Codestates');를 실행하고 스택이 정리가 된다. 이제 이벤트 루프가 개입하여 콜백을 호출한다.

이제 다시 console.log('there')가 스택에 쌓이면서 실행이 된다.

→ setTimeout()을 쓰는 이유는 스택이 비워질 때까지 지연시키기 위함이다. 그 시간 이후에 실행될 것이라는 의미로 사용하는 것은 아님.

[✷ console.timeLog()](https://developer.mozilla.org/en-US/docs/Web/API/console/timeLog)

[✷ console.error()](https://developer.mozilla.org/ko/docs/Web/API/Console/error)
