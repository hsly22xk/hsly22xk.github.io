---
layout: single
title: "D+2 변수와 선언, 할당, 타입, 함수, 조건문"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

자바스크립트 내용 정리.

## 1. 변수(Variable)

① 변수: 상황에 따라 변할 수 있는 값.

⇒ 들어갈 수 있는 값이 다 다르다. 변수는 이름이 붙은 값.

데이터를 보관하기 위한 데이터 보관함(메모리)의 크기는 동일하며, 이 때 보관함의 이름을 '변수'라고 한다.

변수를 통해 보관함에 있는 데이터를 활용할 수 있다.

‣ 프로그래밍은 데이터를 처리하는 것이고, 컴퓨터에게 우리가 원하는 출력 방식을 입력한다.

변수 사용은 데이터를 편리하게 저장하고 꺼내 쓰는 것이다.

ex) 구구단을 출력해낼 때, 숫자를 여러 번 반복해서 쓰는 것이 아닌 변수를 활용하면 쉬움

② 선언(declaration): 데이터를 이용할 때 데이터 보관함의 자리를 확보하는 것.

키워드 let(var, const) 뒤에 변수; 로 쓴다. ⇒ let 변수;

ex) 변수의 이름이 myname일 때,

let myname;

age일 때, let age;

**같은 선언은 한 번만 한다. 두 번 쓰면 에러 난다**

✷ var와 let의 차이점

‣ 호이스팅

: 자바스크립트 코드를 실행시키기 전에 선언된 변수와 함수를 가져가 메모리에 저장시키는데,

함수가 실행되기 전에 안에 있는 변수들을 범위의 최상단으로 끌어올리는 것.

→ var가 let보다 먼저 나왔고,

let은 2015년 경 ES6 버전으로 업그레이드 했을 때 나온 것이다.

ex)

```javascript
console.log(a);
ReferenceError: a is not defined

console.log(a);
var a = 1;
console.log(a);
// 에러가 뜨지 않고 undefined 1로 나옴.
// —> 자바스크립트 엔진이 a라는 변수를 미리 저장해두고
// console.log(a)부터 읽어서 undefined라는 값을 내주고 그 다음에 1이라는 값을 내줌.
```

‣ var는 호이스팅 시 변수의 선언과 초기화(undefined로)를 같이 시킴

‣ var는 지역변수와 전역변수의 개념이 확실하지 않다.

→ var는 함수만 지역변수로 호이스팅이 되고 나머지는 전부 전역변수로 올린다.

‣ let도 호이스팅은 되지만 TDZ(Temporal Death Zone)라는 개념이 있어

변수가 선언이 되어 기억된 것은 알지만, 변수의 초기화문이 나오기 전까지는 접근할 수 없다.

즉, <mark>**변수가 선언된 라인 전까지는 변수를 쓸 수 없다.**</mark>

③ 할당(assignment): 보관함의 자리가 확보되면 데이터를 저장할 수 있다.

변수 = 할당된 값;

= , 부등호 표시는 같다는 표시가 아닌 <mark>**데이터를 저장한다**</mark>는 의미로 사용한다(할당 연산자).

```javascript
myname = "Haley";
age = 12;
```

✷ 선언과 할당을 동시에 할 수 있음

```javascript
let myname = "Haley";
let age = 12;

// 원주율을 일일이 써서 코드를 짤 수 없어서 아예 pi라는 변수의 이름을 붙여 값을 지정함.
let pi = 3.141592;
```

✷ console.log를 통해 결과값을 알 수 있다.

console.log가 없으면 결과값은 이미 나왔지만 눈에는 보이지 않는다.

④ 표현식(expression): 코드의 각 한 줄 한 줄, 변수와 특정 값을 이용하여 연산 등을 하는 경우

⑤ 평가(evaluation): 그것을 구하는 과정

ex)

```javascript
console.log(age * 2);
console.log(age는 age의 값으로 적힌 12로 대체되어 적음 _ 2);
console.log(24);

'hello ' + 'kim'; ⇒'hello kim';
```

```javascript
let pi = 3.141592;
let radius = 5;
pi * 5 * 5;
// 반지름이 5인 원의 넓이를 구하는 공식이 된다.
해당 표현식을 다시 변수로 집어넣을 수도 있다.

let areaOfCircle = pi * radius * radius;
// areaOfCircle이라는 변수를 만들어 원의 넓이 공식을 집어넣었다.
```

‣ 변수의 이름을 붙일 때는 공백을 사용할 수 없다.

ex)

```javascript
areaOfCircle(O)
area Of Circle(X)
```

‣ 보통 변수로 쓰는 단어의 첫 글자는 대문자로 쓴다.

ex) areaOfCircle(Of와 Circle의 첫 글자가 대문자로 들어간다 / 카멜 케이스)

```javascript
let pie = 3.141592;
let radius = 5;
let areaOfCircle = pi _ radius _ radius
console.log(areaOfCircle)
```

‣ 변수는 동일한 변수를 대입하여 사용할 수 있다.

ex)

```javascript
let sum = 1;
sum = sum + 2;
sum = sum + 3;
sum = sum + 4;
// sum이라는 변수가 1일 때, sum+2, +3, +4 .... 이런 형식으로 대입하여 사용할 수 있다.
// 이미 sum에 할당되어 나오는 sum+2의 값을 대입한 것이라는 의미이다. sum에 sum+2를 집어넣는다는 것.
```

## 2. 타입

① 원시 자료형

```javascript
let pi = 3.141592;
// pi의 타입은 number(숫자)타입
// typeof number

let myname = 'Haley';
// myname의 타입은 string(문자열)타입
// typeof string

let isAdult = true(or false);
// isAdult의 타입은 boolean(불린)타입
// typeof boolean

//undefined는 변수가 정의되지 않은, 할당된 값이 없는 것을 말한다. 이도 타입이라고 본다.
// typeof undefined
```

② 참조 자료형: 원시자료형이 아닌 것은 모두 참조자료형이라고 한다. 배열, 객체, 함수가 이에 포함됨.

‣ 배열(자료형): 문자열 타입이 여러 개 섞여있는(compound) 타입, 순서가 있는 집합

ex)

```javascript
// 문자열 타입 'carrot' 'cucumber' 'onion'
let vegetable = ["carrot", "cucumber", "onion"];
```

‣ 객체: 또 다른 자료형의 타입

ex)

이름: Haley

나이: 24

성인입니까? : ✅

이것을 javascript에서는

```javascript
let person = {
  name: "Haley",
  age: 24,
  isAdult: true,
};
```

즉, 불린, 스트링, 넘버가 모두 섞여 있는 타입이라고 볼 수 있다.

✷ name, age, isAdult 뒤에 = 이 아닌 : 을 쓰는 이유는 객체이기 때문이다. 속성에 값을 할당하기 위해서는 : 을 써야 한다.

부등호를 쓰면 Uncaught SyntaxError: Invalid shorthand property initializer라는 에러가 뜸.

## 3. 함수

① 함수: 코드의 묶음. 즐겨 찾는 코드의 모음을 불러올 수 있다. 기능(function)의 단위.

‣ 함수는 keyword, name, parameter(넣고 싶은 모든, 입력하고 싶은 값. 어떤 값이든 들어갈 수 있음), body로 구분된다.

예를 들어, 변수 부분에서 이야기했던 구구단의 경우를 생각해보자.

변수를 사용하여 숫자를 일일이 타이핑하지 않아도 숫자만 바꾸면 값을 구할 수 있었다.

하지만, console.log();를 9번씩 복붙 해야 했다. 이 9개의 복붙 코드 모음을 불러올 수 있는 기능의 단위가 바로 함수이다.

또한 함수는 구체적인 입력값과 출력 값을 가질 수 있다. 호출 후에는 반드시 돌아온다(return).

함수는 항상 출력값을 반환한다.

✷ 그렇다면 함수는 어떻게 사용할 수 있는가?

‣ 함수의 선언(deaclaration): 변수라는 데이터 보관함 밑에 함수를 보관할 특별 공간을 제작하는 것.

‣ 함수의 호출(call, invocation): 함수가 만들어지면 언제든 사용하여 부를 수 있음.

이제 함수를 포함한 표현식이 어떤 식으로 평가되는지 알아보자.

ex)

```javascript
function cal (param1, param2) {
  console.log(param1 + param2);
  return param1 * 10;
}

let result = cal(10, 20); ←함수 호출 코드
console.log(cal(10, 20));
```

여기서 parameter들은 함수 호출 시에 사용된 인자의 값(즉, 10과 20)으로 바뀐다.

parameter의 평가가 끝나면 함수 코드가 순차적으로 실행된다.

첫 번째 console.log(10 + 20)

두 번째 return (10 \* 10)

함수가 리턴하면 호출된 장소로 돌아간다. 이때 함수 호출 코드는 리턴 값으로 바뀌게 된다.

즉, 결과값은 각각 30, 100으로 나오게 된다.

삼각형의 넓이를 구하는 공식은 밑변 \* 높이다.

```javascript
let base = 3;
let height = 4;
console.log(base * height) / 2;
```

이렇게 간단하게 할 수 있겠지만, 계속 숫자만 달라진 채로 반복된다면 일일이 바꿔줘야 할 것이다.

그것을 더욱 편리하게 하기 위해 함수를 쓴다.

② 함수를 표현하는 세 가지 방식

‣ 함수선언식

```javascript
function getTriangleArea(base, height) {
  let triangleArea = (base * height) / 2,
  return triangleArea;
}

console.log(getTriangleArea(3, 4)) / 2; // 6
```

여기서 입력값(매개변수)은 base와 height. 즉 변수로 적어주는 값.

삼각형의 넓이를 구하기 위한 공식을 변수로 써주었다.

이 값이 출력되기 위해서는 출력 값이 리턴되어야 한다. 그래서 return TriangleArea를 써준다.

여기서 getTriangle(3, 4) 에서 (3, 4)는 전달 인자로 볼 수 있다. 즉, 함수를 호출할 때 전달해주는 값.

만약 써주지 않았다면 출력 값은 undefined.

‣ 함수표현식

const getTriangleArea = function(base, height) {
let triangleArea = (base \* height) / 2;
return triangleArea;
}
함수 표현식은 제일 먼저 함수를 선언해주는 것이다. 이것이 const getTriangleArea이다.

그다음에 익명 함수를 할당하는 방식이다.

함수 선언 바로 다음에 써주는 것들이 전부 익명 함수로 출력 값을 낸 것이다.

‣ 화살표함수

```javascript
const getTriangleArea = (base, height) => {
  let triangleArea = (base * height) / 2;
  return triangleArea;
};
```

화살표 함수도 제일 먼저 변수를 선언해주고, 그 변수의 function keyword를 => 화살표 표시로 익명 함수를 축약해서 표시한 익명 함수를 할당해준다.

③ 함수는 지시사항들의 묶음이다.

사실 앞서 언급했던 함수는 즐겨 찾는 코드의 모음이라는 말이 나는 이해가 가지 않았다.

근데 모르는 거 여러 번 듣고 들여다 보고 소리 내어 읽어보아도 이해가 안 되니 소용없었다.

그래서 다음 챕터로 넘어왔다. 차라리 수도코드로 활용하여 예시를 들어보자.

영상에서는 다른 예시를 들었지만, 내게 가장 익숙한 잼 샌드위치 만들기를 적었다.

```javascript
function getSomeJamSandwich() {
  // 1. 식빵 봉지를 뜯어 식빵 두 장을 꺼낸다.
  // 2. 식빵 두 장을 넓은 면이 위로 가도록 도마 위에 둔다.
  // 3. 잼 뚜껑을 열어 잼 나이프를 그 안에 넣고 잼을 듬뿍 뜬다.
  // 4. 잼이 듬뿍 발린 잼 나이프를 한쪽 식빵의 넓은 면에 발라준다.
  // 5. 잼을 바르지 않은 나머지 식빵의 넓은 면으로 다른 식빵의 잼 바른 부분의 넓은 면을 덮어준다.
  // 6. 잼 샌드위치를 제공한다(return)
}
```

## 4. 조건문(Conditional)

: 어떠한 조건을 판별하는 기준을 만드는 것

ex)

학생이냐 아니냐의 판단 기준은 학교를 다니냐 안 다니냐

성인이냐 아니냐의 판단 기준은 만 19세 이상인가 아닌가

⇒조건문에는 반드시 비교 연산자가 필요함. 비교의 결과는 언제나 true or false(boolean).

ex)

```javascript
3 > 6; // false;
1 < 8; // true;
"You" === "Me"; // false;
```

✅ 비교 시 엄밀(엄격)한 비교(===과 !==)의 필요성

= : 할당하는 것

== / != : 서로 같은 지 다른 지 확인(느슨한 비교)

=== / !== : 서로 같은 지 다른 지 확인 + 타입까지 같은지 확인

ex)

```javascript
2 == "2"; // true --> 느슨한 비교를 하므로 숫자 타입이나 문자 타입이나 같다는 뜻인 true가 리턴됨
2 === "2"; // false --> 엄격한 비교를 하기 때문에 숫자 타입과 문자 타입은 다르다는 뜻인 false가 리턴됨
```

① 조건문 쓰는 방법

```javascript
if (조건1) {
  // 조건1이 통과할 경우 {} 사이에 있는 공식이 실행됨
  // 즉, 조건에 따른 실행 내역이 {} 사이에 들어가게 됨
} else if (조건2) {
  // 조건1이 통과하지 않고
  // 조건2가 통과할 경우 else if에 있는 공식이 실행됨
} else {
  // 조건1과 2가 모두 통과하지 않는 경우 else에 있는 공식이 실행됨
}

// if와 else if 뒤에 나오는 조건1, 조건2 같은 경우에는 boolean으로 결과값이 나오는 조건문(표현식)이 들어감
```

② 두 가지 경우가 중첩되는 경우 ⇒ 논리 연산자 이용

ex)

```javascript
// 1. 학생이면서 여성일 때 통과
// and연산자(두 가지 조건 다 만족시켜야만 함)
if(isStudent && isFemale) {
return true;
};

// 2. 학생이거나 여성일 때 통과
// or연산자(둘 중 하나만 만족시켜도 됨)
if(isStudent || isFemale) {
retrun true;
};

// 3. 학생이 아니면서 여성일 때 통과
//not연산자(=truthy, falsy여부를 반전시킴)
if(!isStudent && isFemale) {
return true;
};
```

not 연산자의 예시

```javascript
!true; // false
!false; // true
!(3 < 1); // true
!undefined; // true ⇒undefined는 falsy한 값으로 말한다
!"Hello"; // false ⇒문자열은 truthy한 값으로 말한다
```

✅ 기억해야 하는 6가지 falsy값: if문에서 false가 변환되므로 if문이 실행되지 않음

```
①if (false)
②if (null)
③if (undefined)
④if (0)
⑤if (NaN)
⑥if (' ') →아무 값도 없는 문자열
```

✷ 코드 학습법

‣ 모르는 것을 검색할 때

1. 구글링 한다(mdn ~ , how to ~ 문법으로 검색하는 것이 빠르다)

2. stackoverflow를 적극 활용한다. 최대의 q&a사이트.

3. 아고라 스테이츠를 활용한다.

‣ 크롬 개발자 도구를 활용하여 자바스크립트 문법을 직접 작성해볼 수 있다.

(역시 글로 백번 읽는 것보다 한 번 직접 해보는 게 더 빠르다.

그렇다 해도 맨땅에 헤딩하는 사람은 오류 나오면 왜 오류 나왔는지 모른다...그냥 계속해보고 모르는 건 질문해보자)

⇒ 구글링해서 내가 알 수 있을 정도로 계속 찾아보고 이해하는 것이 제일 정도다. 그것도 아니면 공부할 때는 유튜브 강의 영상만큼 좋은 게 없다...
