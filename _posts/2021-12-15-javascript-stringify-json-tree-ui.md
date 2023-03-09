---
layout: single
title: "D+30(31) 재귀 함수, stringifyJSON, TreeUI"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

전반적인 내용 정리글.

## Array.prototype.fill

[<font color="blue">Array.prototype.fill</font>](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

배열의 시작 인덱스부터 끝 인덱스의 이전까지 정적인 값 하나로 채운다.

‣ 기본 구문

```js
array.fill(value[, start[, end]])
```

매개변수

① value: 바꿔줄 값

② start: 시작 인덱스(기본값은 0 / optional)

③ end: 끝 인덱스(기본값은 this.length / optional)

반환값: 변형한 배열

ex)

```js
let array = [1, 2, 3, 4];
console.log(array.fill(0, 2, 4));
// [1, 2, 0, 0]

console.log(array.fill(5, 1));
// [1, 5, 5, 5]

console.log(array.fill(6));
// [6, 6, 6, 6]
```

## 1. 재귀 함수

종료 조건이 충족될 때까지 반복적으로 자기 자신을 호출하는 함수. 그러면서 주어진 작업을 수행함.

‣ 재귀(recursion): 어떤 문제를 해결할 때 동일한 구조의 더 작은 문제를 해결함으로써 주어진 문제를 해결하는 방법.

‣ 재귀 호출: 실행과정 중에 자기 자신을 호출하는 호출 방식.

```js
// 자연수로 이루어진 리스트(배열)를 입력받고, 리스트의 합을 리턴하는 함수 `arrSum` 을 작성하라.

// 1. 보조변수 sum을 0으로 초기화한다.
// 2. 순차적으로 배열의 요소에 접근한다.
// 3. 그것을 sum에 더한다.

function arrSum(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}
```

이것을 토대로 자연수로 이루어진 배열 [10, 3, 6, 2]의 합을 구한다고 가정한다.

① 전체 배열인 [10, 3, 6, 2]의 합을 구하는 대신 [3, 6, 2]의 합을 구하는 방법을 생각한다. 기존 문제에서 출발하여 더 작은 경우를 생각한다. arrSum에 적용할 문제를 더 작게 쪼갠다.

```js
arrSum([10, 3, 6, 2]) = 10 + arrSum([3, 6, 2]);
```

② [3, 6, 2] 보다 더 짧은 [6, 2]의 합을 구하는 방법을 생각한다.

```js
arrSum([3, 6, 2]) = 3 + arrSum([6, 2])
```

③ 이보다 더 짧은 [2]의 합을 구하는 방법을 생각해본다. [2]의 합은 2이기 때문에 여기에 6을 더해 [6, 2]의 합을 구할 수 있다.

```js
arrSum([2]) = 6 + arrSum([2])
```

계속 같은 방식으로 문제가 더는 작아지지 않을 때까지 더 작은 경우를 생각한다. arrSum에 적용할 문제를 가장 작은 단위까지 쪼갠다.

④ [6, 2]의 합을 구하는 방법을 알아낸 후, 이 값에 3을 더해 [3, 6, 2]의 합을 구한다.

이 과정을 아래의 간단한 코드로 표현할 수 있다.

```js
arrSum([10, 3, 6, 2]) = 10 + arrSum([3, 6, 2]);
arrSum([3, 6, 2]) = 3 + arrSum([6, 2]);
arrSum([6, 2]) = 6 + arrSum([2]);
arrSum([2]) = 2 + arrSum([]);
arrSum([]) = 0;
```

⑤ 문제가 간단해져서 바로 풀 수 있게 되는 순간부터 앞서 생성한 문제를 해결한다. 가장 작은 단위부터 arrSum을 적용하여 문제를 푼다.

```js
arrSum([]) = 0; // 문제가 더는 작아지지 않는 순간

// 가장 작은 경우의 해결책을 적용한다.
arrSum([2]) = 2 + arrSum([]) = 2;
arrSum([6, 2]) = 6 + arrSum([2]) = 6 + 2 = 8;
arrSum([3, 6, 2]) = 3 + arrSum([6, 2]) = 3 + 8 = 11;
arrSum([10, 3, 6, 2]) = 10 + arrSum([3, 6, 2]) = 10 + 11 = 21;
```

⇒ 이처럼 함수 arrSum 은 (인자가 빈 배열이 아닌 경우) 실행과정 중에 자기 자신을 호출한다. 이러한 호출 과정을 앞서 언급한 재귀 호출이라고 한다.

✷ 다음과 같이, arrSum 을 보다 엄밀하게(formally) 정의할 수 있다.

```js
// 함수 arrSum의 엄밀한 정의

/*
 * 1. arr이 빈 배열인 경우 = 0
 * 2. 그 외의 경우 = arr[0] + arrSum(arr2)
 *   (arr2는 arr의 첫 요소를 제외한 나머지 배열)
 */
arrSum(arr);
```

## 2. 재귀를 사용할 수 있는 경우

① 주어진 문제를 비슷한 구조의 더 작은 문제로 나눌 수 있는 경우

② 중첩된 반복문이 많거나 반복문의 중첩 횟수(number of loops)를 예측하기 어려운 경우

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    for (let k = 0; k < n; k++) {
      for (let l = 0; l < n; l++) {
        for (let m = 0; m < n; m++) {
          for (let n = 0; n < n; n++) {
            for (let o = 0; o < n; o++) {
              for (let p = 0; p < n; p++) {
                // do something
                someFunc(i, j, k, l, m, n, o, p);
              }
            }
          }
        }
      }
    }
  }
}
```

모든 재귀 함수는 반복문(while 문 또는 for 문)으로 표현할 수 있지만 재귀를 적용할 수 있는 대부분의 경우에는 재귀를 적용한 코드가 훨씬 간결하고 이해하기 쉽다.

## 3. 재귀적 사고

① 재귀 함수의 입력값과 출력값 정의하기

→ 문제를 가장 추상적으로 / 단순하게 정의하기.

‣ 함수 arrSum의 경우 number 타입을 요소로 갖는 배열을 입력으로 받고 number 타입을 리턴한다.

이를 조금 더 간단하게 표기해보자.

```js
arrSum: [number] => number
```

② 문제를 쪼개고 경우의 수를 나누기

→ 문제를 쪼갤 기준을 정한다.

→ 정한 기준에 따라 문제를 더 큰 경우와 작은 경우로 구분할 수 있는지 확인한다.(일반적인 경우에는 입력값으로 기준을 정한다)

⇒ 입력값이나 문제의 순서와 크기가 제일 중요한 관점이다. 주어진 입력값 / 문제 상황을 크기로 구분할 수 있거나, 순서를 명확하게 정할 수 있으면 문제 구분에 도움이 된다.

ex)

‣ 함수 arrSum의 경우 입력값인 배열의 크기에 따라 더 작은 문제로 나눌 수 있었다. arrSum([1, 2, 3, 4])과 arrSum([2, 3, 4])을 구하는 방법은 동일하기 때문에 이 구분은 적절하다.

‣ 문제에서 주어진 입력값에 따라 경우의 수를 나눈다. 일반적으로 더 이상 문제를 쪼갤 수 없는 경우와 그렇지 않은 경우로 나눈다.

‣ 함수 arrSum은 입력값이 빈 배열인 경우와 그렇지 않은 경우로 나눈다. 각각의 경우는 다른 방식으로 처리한다.

```js
arrSum: [number] => number
arrSum([ ])
arrSum([e1, e2, ... , en])​
```

③ 단순한 문제 해결하기

재귀의 기초(base case): 문제를 여러 경우로 구분한 후, 가장 해결하기 쉬운 문제부터 해결한다.

→ 재귀 함수를 구현할 때 재귀의 탈출 조건(재귀 호출이 멈추는 조건)을 구성한다.

‣ 함수 arrSum을 더이상 쪼갤 수 없는 경우는 입력값이 빈 배열인 경우이고, 이 때 arrSum([])의 리턴값은 0이다.

```js
arrSum: [number] => number
arrSum([ ]) = 0
arrSum([e1, e2, ... , en])
```

④ 남아있는 복잡한 경우 해결하기

‣ 길이가 1 이상인 배열이 함수 arrSum에 입력된 경우, 맨 앞의 요소에 대한 결과(head)를 따로 구하고 나머지 요소를 새로운 입력값으로 갖는 문제로 구분하고, 이를 해결하여 얻은 결과를 head에 더한다.

```js
arrSum: [number] => number
arrSum([ ]) = 0
arrSum([e1, e2, ... , en]) = e1 + arrSum([e2, ..., en])
```

‣ 배열을 head와 나머지 부분(tail)으로 구분하는 방법을 알면 arrSum을 재귀적으로 구현 가능하다.

⑤ 코드 구현하기

```js
function arrSum(arr) {
  //Base Case : 문제를 더 이상 쪼갤 수 없는 경우 (재귀의 기초)
  if (arr의 길이가 0인 경우) {
    return 0;
  }
  /*
  * Recursive Case : 그렇지 않은 경우
  * 문제를 더 이상 쪼갤 수 없는 경우
  * head: 배열의 첫 요소
  * tail: 배열의 첫 요소만 제거된 배열
  */
  let head = arr[0];
  let tail = arr.slice(1);
  return head + arrSum(tail);
}
```

✷ Factorial로 알아보는 재귀 함수

ex)

![](https://blog.kakaocdn.net/dn/cduKIY/btrnJASO6TW/r060PJ9ibRIqoAz5FiGTLk/img.png)

```js
4! = 4 * 3 * 2 * 1
   = 4 * (3 * 2 * 1) // ()친 부분은 3!
   = 4 * 3 * (2 * 1) // ()친 부분은 2!
   = 4 * 3 * 2 * (1) // ()친 부분은 1

function fact(n) {
  if(n === 1) {
  return 1;
  }
  return n * fact(n - 1);
}
```

## 4. StringifyJSON

① JSON(JavaScript Object Notation)

데이터 교환을 위해 만들어진 객체 형태의 포맷. 브라우저와 서버 사이에서 오고가는 데이터의 형식.

⇒ 서로 다른 프로그램 사이에서 데이터를 교환하기 위한 포맷으로 JSON 포맷은 자바스크립트을 포함한 많은 언어에서 범용적으로 사용하는 유명한 포맷이다.

ex)

네트워크를 통해, 어떤 객체 내용을 다른 프로그램에게 전송한다고 가정한다.

이 객체 내용을 일종의 메신저 혹은 채팅 프로그램에서 쓰는 하나의 메시지라고 한다면, 다음 객체를 어떻게 전송할 수 있을까?

```js
// 메시지를 담고 있는 객체 메시지

const message = {
  sender: "Alex",
  receiver: "Haley",
  message: "Shall we dance at Flower Dance?",
  createdAt: "2021-03-23 21:10:33",
};
```

메시지 객체가 전송 가능하려면(transferable condition) 메시지를 보내는 발신자와 메시지를 받는 수신자가 같은 프로그램을 사용하거나, 문자열처럼 범용적으로 읽을 수 있는 형태여야 한다.

**<mark>객체는 타입 변환을 이용해 String으로 변환할 경우 객체 내용을 포함하지 않는다.</mark>**

JavaScript에서 객체에 메소드(message.toString())나 형변환(String(message))을 시도하면 [object Object] 라는 결과를 리턴한다.

이 문제를 해결하는 방법은 객체를 JSON의 형태로 변환하거나 JSON을 객체의 형태로 변환하는 방법이다.

‣ [JSON.stringify](https://steemit.com/kr-dev/@cheonmr/json-stringify): Object type을 JSON으로 변환한다.

‣ JSON.parse: JSON을 Object type으로 변환한다.

```js
// message 객체를 JSON으로 변환하는 메소드 JSON.stringify

let transferableMessage = JSON.stringify(message);
console.log(transferableMessage);
// `{"sender":"Alex", "receiver":"Haley", "message":"Shall we dance at Flower Dance?", "createdAt":"2021-03-23 21:10:33"}`
console.log(typeof transferableMessage); // `string`

⇒ stringify하는 과정을 직렬화(serialize)라고 한다.
```

<mark>JSON으로 변환된 객체의 타입은 문자열이고, 발신자는 객체를 직렬화한 문자열을 객체의 내용으로 보낼 수 있다.</mark>

수신자가 이 문자열 메시지를 다시 객체의 형태로 만들려면 메소드 JSON.parse 를 사용할 수 있다.

```js
// 직렬화된 JSON에 메소드 JSON.parse를 적용하면 다시 객체의 형태로 변환할 수 있다.

let packet = `{"sender":"Alex", "receiver":"Haley", "message":"Shall we dance at Flower Dance?", "createdAt":"2021-03-23 21:10:33"}`

let obj = JSON.parse(packet)
console.log(obj)

/*
 * {
 * sender: "Alex",
 * receiver: "Haley",
 * message: "Shall we dance at Flower Dance?",
 * createdAt: "2021-03-23 21:10:33"
 * }
 */
 console.log(typeof(obj))
 // `object`

⇒ JSON.parse를 적용하는 이 과정을 역직렬화(deserialize)한다고 한다.
```

![](https://blog.kakaocdn.net/dn/rEFZh/btrnN2PcW1z/ucJpCn1HtrkOahEUJUrHM1/img.png)

(직렬화와 역직렬화 모식도)

## 4-1. JSON의 기본 규칙

⇒ JSON은 키와 값 사이, 그리고 키-값 쌍 사이에는 공백이 있어서는 안된다.

|           |              자바스크립트 객체               |            JSON             |
| :-------: | :------------------------------------------: | :-------------------------: |
| 문자열 값 | 문자열 값은 어떠한 형태의 따옴표도 사용 가능 | 반드시 큰따옴표로 감싸야 함 |
|    키     |         키는 따옴표 없이 쓸 수 있음          | 반드시 큰따옴표를 붙여야 함 |

## 5. Tree UI

```
‣ 트리 구조에 재귀 함수를 활용할 수 있다.
‣ JSON 구조에 재귀 함수를 활용할 수 있다.
‣ DOM 구조에 재귀 함수를 활용할 수 있다.
```

```js
// tree-UI를 만들어야 할 메뉴판
// menu는 수정하지 않고, createTreeView 함수만 수정한다.

const menu = [
  {
    type: "group",
    name: "음료",
    children: [
      {
        type: "group",
        name: "콜드 브루",
        children: [
          { type: "item", name: "나이트로 콜드 브루" },
          { type: "item", name: "돌체 콜드 브루" },
          { type: "item", name: "제주 비자림 콜드 브루" },
          { type: "item", name: "콜드 브루" },
        ],
      },
      {
        type: "group",
        name: "프라푸치노",
        children: [
          { type: "item", name: "애플 쿠키 크림 프라푸치노" },
          { type: "item", name: "더블 에스프레소 칩 프라푸치노" },
          { type: "item", name: "모카 프라푸치노" },
          { type: "item", name: "피스타치오 크림 프라푸치노" },
        ],
      },
      {
        type: "group",
        name: "블렌디드",
        children: [
          { type: "item", name: "망고 바나나 블렌디드" },
          { type: "item", name: "딸기 요거트 블렌디드" },
          { type: "item", name: "자몽 셔벗 블렌디드" },
          { type: "item", name: "피치 & 레몬 블렌디드" },
        ],
      },
      {
        type: "group",
        name: "티",
        children: [
          { type: "item", name: "라임 패션 티" },
          { type: "item", name: "민트 블렌드 티" },
          { type: "item", name: "아이스 유스베리 티" },
          { type: "item", name: "아이스 캐모마일 블렌드 티" },
        ],
      },
      {
        type: "group",
        name: "주스",
        children: [
          { type: "item", name: "한방에 쭉 감당" },
          { type: "item", name: "파이팅 청귤" },
          { type: "item", name: "딸기주스" },
          { type: "item", name: "도와주 흑흑" },
        ],
      },
    ],
  },
  {
    type: "group",
    name: "음식",
    children: [
      {
        type: "group",
        name: "빵",
        children: [
          { type: "item", name: "트러플 미니 스콘" },
          { type: "item", name: "보늬밤 몽블랑 데니쉬" },
          { type: "item", name: "고소한 치즈 베이글" },
          { type: "item", name: "미니 클래식 스콘" },
        ],
      },
      {
        type: "group",
        name: "케이크",
        children: [
          { type: "item", name: "밀당 에그 타르트" },
          { type: "item", name: "마스카포네 티라미수 케이크" },
          { type: "item", name: "블루베리 쿠키 치즈 케이크" },
          { type: "item", name: "부드러운 생크림 카스텔라" },
        ],
      },
      {
        type: "group",
        name: "샌드위치",
        children: [
          { type: "item", name: "애플 까망베르 샌드위치" },
          { type: "item", name: "트리플 머쉬룸 치즈 샌드위치" },
          { type: "item", name: "로스트 치킨 샐러드 밀 박스" },
          { type: "item", name: "B.E.L.T 샌드위치" },
        ],
      },
      {
        type: "group",
        name: "과일",
        children: [
          { type: "item", name: "하루 한 컵 RED" },
          { type: "item", name: "한라봉 가득 핸디 젤리" },
        ],
      },
      {
        type: "group",
        name: "스낵",
        children: [
          { type: "item", name: "리저브 초콜릿 세트" },
          { type: "item", name: "로스티드 아몬드 앤 초콜릿" },
          { type: "item", name: "마카롱" },
          { type: "item", name: "자일리톨 캔디 크리스탈 민트" },
        ],
      },
      {
        type: "group",
        name: "아이스크림",
        children: [
          { type: "item", name: "자바 칩 유기농 바닐라 아이스크림" },
          { type: "item", name: "넛츠 초콜릿 아포가토" },
          { type: "item", name: "바닐라 아포가토" },
        ],
      },
    ],
  },
  {
    type: "group",
    name: "굿즈",
    children: [
      {
        type: "group",
        name: "머그",
        children: [
          { type: "item", name: "우리 한글 블랙 머그 473ml" },
          { type: "item", name: "서울 투어 머그 355ml" },
          { type: "item", name: "스타벅스 1호점 머그 400ml" },
          { type: "item", name: "서울 제주 데이머그 세트" },
        ],
      },
      {
        type: "group",
        name: "텀블러",
        children: [
          { type: "item", name: "SS 부산 투어 텀블러 355ml" },
          { type: "item", name: "SS 블랙 헤리티지 오드리 텀블러 355ml" },
          { type: "item", name: "SS 에치드 실버 텀블러 473ml" },
        ],
      },
      {
        type: "group",
        name: "악세사리",
        children: [
          { type: "item", name: "리저브 오렌지 카드 홀더" },
          { type: "item", name: "스타벅스 1호점 에코백" },
          { type: "item", name: "스타벅스 1호점 랩탑 파우치" },
        ],
      },
    ],
  },
  {
    type: "group",
    name: "카드",
    children: [
      { type: "item", name: "10000원권" },
      { type: "item", name: "30000원권" },
      { type: "item", name: "50000원권" },
      { type: "item", name: "100000원권" },
    ],
  },
];
```

```js
const root = document.getElementById("root");
function createTreeView(menu, currentNode) {
  // 적용해야 할 코드 작성 //
}

createTreeView(menu, root);
```

```
① ul#root 안에 li 엘리먼트를 4개 넣기
② 체크박스 만들기
③ span태그로 감싸기 ⇒ DOM에서 새로운 엘리먼트를 만들고 넣을 때 어떻게 했는지 생각해보기 ⇒ 반복되는 것이 어떤 것이 있는지 생각해보고 반복문 사용하기 ⇒ root에 대한 재귀함수 호출에 대해 생각해보기

④ 자식 노드가 있느냐 없느냐의 조건을 따지기 ⇒ currentNode에 대해 생각해보기.
⇒ html 구조가 헷갈리면 html파일을 브라우저로 연 후 우클릭+검사로 콘솔창을 열어 html구조 확인해보기.
```

[DOM에서 새로운 엘리먼트를 만들고 넣을 때 참고링크](https://hsly22xk.github.io/javascript/javascript-dom/)
