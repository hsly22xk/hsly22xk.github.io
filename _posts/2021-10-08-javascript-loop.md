---
layout: single
title: "D+4 반복문(for문, while문)"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

자바스크립트 반복문

## 반복문

같거나 비슷한 코드를 여러 번 실행시켜야 할 때 쓰는 구문

‣ 조건을 따지고 조건을 전부 정확하게 정의해준 다음

ex)

```javascript
let sum = 1;
sum = sum + 2; // 조건
sum = sum + 3; // 조건
sum = sum + 4; // 조건
console.log(sum);

// sum과 숫자 n의 합을 sum에 대입하자.
// 조건에서 숫자 n은 2부터 시작한다.
// 숫자 n은 4가 될 때까지 반복한다.
// 숫자 n은 1씩 증가한다.
```

## 반복문을 작성하는 순서

① 반복할 내용을 코드로 먼저 작성한다.

예시에서 보면 반복되는 코드는 sum = sum + n이다.

② 조건을 코드로 작성한다(조건문).

숫자 n은 2부터 시작한다.

그러면 변수로 먼저 선언을 해준다.

```
let n = 2;
```

숫자 n은 4가 될 때까지 반복한다.

즉, 숫자 n은 4와 같거나 그보다 작다.

```
n <= 4;
```

마지막으로 숫자 n은 1씩 증가한다.

```
n = n + 1;
```

즉,

```
let n = 2;
n <= 4
n = n + 1;
```

로 조건을 작성할 수 있다.

→ for 구문은 어디까지 반복을 해야하는가가 정해져있을 때 주로 사용함

‣ for 구문 쓰는 순서

①반복할 내용(반복되는 코드)을 { } 안에 넣어준다.

앞에 예시를 다시 보자.

```javascript
let sum = 1;
sum = sum + 2;
sum = sum + 3;
sum = sum + 4;
```

sum = sum + n 구문이 반복되고 있다.

이제 이 다음 줄에 for구문을 사용하여 반복문을 써보자.

```javascript
for() {
  sum = sum + n
}
```

② 반복문의 조건을 초기화, 조건식, 증감문 순서로 ( )안에 넣어준다.

예시에서 보면, 우리는 조건을

```javascript
let n = 2;
n <= 4;
n = n + 1;
```

으로 작성했다.

그렇다면 초기 조건, 즉 반복하는 횟수는

```
let n = 2;
```

가 될 것이고

언제까지 반복되는 조건인지?몇 번이나 반복하게 할 것인가?

```
n <= 4;
```

마지막으로 얼만큼 증가하고 감소할 것인지?즉, 반복이 끝났을 때의 상태 변화는?

```
n = n + 1;
```

그렇다면 이것을 다시 정리하여 쓰게 되면,

```
let sum = 1;
for (let n = 2; n <= 4; n = n + 1;) {
  sum = sum + n
}
console.log(sum); // 10
```

그렇다면 예시를 하나 더 들어보자.

```
for( , , ) {

}

console.log('I am a girl')
```

콘솔 출력을 다섯 번 반복하여 찍기 위해 필요한 조건은 무엇일까?

첫번째는 초기화, 두번째는 조건식, 세번째는 증감문이 필요하다.

그렇다면 let n = 0 || let n = 1로 잡을 수 있을 것이다.

조건식은? 우리는 5번 반복해야 되기 때문에 n <= 4 || n < 5로 적을 수 있다.

증감문은? n = n + 1이다.

'I am a girl'을 5번 출력해야 하기 때문에. 5번 출력한다는 것이 조건이다.

```javascript
for (let n = 0; n <= 4; n = n + 1) {
  console.log("I am a girl");
}
// ⑤ I am a girl
// n = 0 이고, n이 4보다 작거나 같다. n = n + 1;이다.
```

즉, 0부터 4까지이다. 0, 1, 2, 3, 4

총 5번 반복이 된다.

```javascript
for(let n = 0; n < 5; n = n + 1){
  console.log('I am a girl');
}
// ⑤ I am a girl
// 위의 예시와 같은 방식으로 진행된다.

n = 0, n = 5보다 작다. 5를 포함하지는 않는다.
즉 0, 1, 2, 3, 4
```

```javascript
for(let n = 1; n <= 5; n = n + 1){
  console.log('I am a girl');
}

⑤ I am a girl

// 이번엔 변수 n을 1로 선언하였다. 이제 n은 5와 같거나 그보다 작다. 즉, 5를 포함한다.

1, 2, 3, 4, 5

// 총 5번 반복이 된다.
```

- while구문

: 특정 조건까지 계속 반복을 해야하는가일 때 주로 사용함

반복할 조건 중 초기화와 증감문을 따로 쓰고, 조건식을 따로 괄호 안에 써준다.

앞의 예시에서 따왔던

```javascript
let sum = 1;
sum = sum + 2;
sum = sum + 3;
sum = sum + 4;
console.log(sum);
```

을 보자.

```javascript
let sum = 1;
let n = 2; // 초기화를 따로 써줬다
while (n <= 4) {
  // 조건식을 따로 소괄호 안에 써주었다
  sum = sum + n; // 반복되는 구문을 { } 안에 써주었다
  n = n + 1; // 증감문도 초기화와 같이 따로 써주었다
}
console.log(sum); // 10
```

즉,

```javascript
let 변수 = 1;
let 초기화변수 = 2;

while (조건식) {
  반복구문;
  증감문;
}
console.log(변수);
```
