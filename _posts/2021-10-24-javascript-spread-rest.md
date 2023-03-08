---
layout: single
title: "D+20 spread/rest문법"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

spread/rest 문법

## 1. spread 문법

배열의 요소를 펼쳐 주는 문법으로, 배열을 풀어 인자로 전달하거나, 배열을 풀어 각각의 요소로 전달할 때 사용한다.

ex)

```js
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];
sum(...numbers); // 6
```

...numbers라고 써준 것은 배열의 각각의 요소들을 나눠주고 x, y, z라는 인자에 전달하는 방식이다. 요소들이 x, y, z에 전달되었으므로 sum은 1 + 2 + 3이 된다.

그렇기 때문에 콘솔에 입력하면 답은 6이 나온다.

**✷ ...은 spread문법의 연산자이다(dot 3개 연속으로 붙이는 것이 연산자).**

① 배열에서 사용하기

‣ 배열 합치기

```js
let parts = ["b", "c"];
let entire = ["a", ...parts, "d", "e"];
console.log(entire); // ['a', 'b', 'c', 'd', 'e'];
```

기존의 parts 배열은 건드리지 않으면서, 새로운 entire 배열에 parts 가 가지고 있는 내용을 모두 집어넣어 합친다.

‣ 배열 복사

```js
let arr1 = [1, 2, 3]; // 배열의 요소가 문자열이라도 똑같은 결과가 나온다.
let arr2 = [4, 5, 6];
arr1 = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]
```

→ spread문법은 기존 배열을 변경하지 않는다. 그러므로 arr1의 값을 바꾸려면 새롭게 할당을 해주어야 한다.

→ spread문법은 하나만 쓸 수 있는 것이 아닌 여러 개 쓸 수 있다.

## rest 문법

객체, 배열, 함수의 파라미터에서 사용 가능하며, 파라미터를 배열의 형태로 받아 사용할 수 있다. 파라미터가 가변적일 때 유용하다.

② 객체에서 사용하기

‣ 객체 사용 예시

```js
let obj1 = { foo: "bar", x: 42 };
let obj2 = { foo: "baz", y: 13 };

let clonedObj = { ...obj1 };
let mergedObj = { ...obj1, ...obj2 };

console.log(clonedObj); // { foo: 'bar', x: 42 }
console.log(mergedObj); // { foo: 'baz', x: 42, y: 13 }
```

⇒ 객체에 겹치는 키 이름이 있는 경우에는 원래 obj1의 값은 없어지고 obj2의 값이 앞에 나오며, 나머지 obj1의 키값쌍인 x: 42는 그대로 뒤에 붙는 것을 볼 수 있다.

‣ 함수에서 나머지 파라미터 받아오기

- 함수의 마지막 매개변수 앞에 "..."를 붙이면 사용자가 정한 모든 후속 매개변수를 배열에 넣도록 지정한다.

```js
function myFun(a, b, ...manyMoreArgs) { // 함수에서 ()소괄호 안에 쓰인 것들이 파라미터(매개변수)
  console.log("a", a); // console.log()에서 () 안에 쓰인 것들이 인자, 즉 함수에서 값을 넣어준 것들
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");

a one
b two
manyMoreArgs (4) ['three', 'four', 'five', 'six']
```

함수의 매개변수로 붙은 ...manyMoreArgs는 rest parameter, rest syntax라고 부른다.

<mark>남아있는 모든 인자를 하나의 배열에 담기 때문이다.</mark>

이 예제에서는 따로 매개변수를 지정해주었기 때문에 남은 인자가 배열의 형태로 나온다.

그래서 a one / b two / manyMoreArgs ['three', four', 'five', 'six']라는 형태로 출력이 된다.

따로 매개변수를 지정해주지 않았다면 배열의 형태로 모든 인자를 할당받았을 것이다. 즉, 모든 인자가 배열의 형태로 나왔을 것.

## 3. 구조분해(Destructing)

spread 문법을 이용하여 배열이나 객체의 속성을 해체한 후, 개별 값을 개별 변수에 새로 할당하는 과정으로, 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 표현식.

① 분해 후 새 변수에 할당

‣ 배열

```js
// const를 사용하여 [a, b, ...rest]라는 변수의 이름에 배열 [10, 20, 30, 40, 50]를 할당.
const [a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]
```

‣ 객체

```js
// const를 사용하여 {a, b, ...rest}라는 변수의 이름에 객체 {a: 10, b: 20, c: 30, d: 40}를 할당.
const { a, b, ...rest } = { a: 10, b: 20, c: 30, d: 40 };

console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```

‣ 객체에서 구조 분해 할당을 사용하는 경우

선언 키워드(var, let, const)와 함께 사용하지 않을 시 에러가 발생할 수 있다. 선언 없이 할당하는 경우엔 구조 분해를 통해 변수의 선언과 분리하여 변수에 값을 할당할 수 있다.

```js
var a, b;
({ a, b } = { a: 1, b: 2 });
```

‣ 함수에서의 객체 분해

```js
function whois({ displayName: displayName, fullName: { firstName: name } }) {
  console.log(displayName + " is " + name);
}

let user = {
  id: 42,
  displayName: "jdoe",
  fullName: { firstName: "John", lastName: "Doe" },
};

whois(user); // jdoe is John
```

lastName은 whois함수 내 객체에서 없는 키-값쌍이기 때문에 결과값은 displayName과 fullName객체 안의 키 firstName만 나온다.
