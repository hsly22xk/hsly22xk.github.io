---
layout: single
title: "D+52 Algorithm with math(순열 / 조합, GCD / LCM, 멱집합), 정규표현식"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

수학 알고리즘과 정규식.

## 1. Algorithm with Math

수학적 사고를 통한 컴퓨팅 사고를 할 수 있어야 한다.

### ① 순열 / 조합

‣ 순열: n개 중에서 일부만을 선택하여 나열하는 것. 순서를 지키며 나열하는 것.

‣ 조합: 순서를 고려하지 않고 나열함.

```
카드 뽑기

[A, B, C, D, E]로 이뤄진 5장의 카드가 있습니다. 이 5장의 카드 중 3장을 선택하여 나열하려고 합니다.
이 때, 다음의 조건을 각각 만족하는 경우를 찾아야 합니다.

→ 순서를 생각하며 3장을 선택하는 조건을 만족하는 모든 경우의 수
// 경우의 수를 구하는 방법들
첫번째 나열하는 카드를 선택하는 방법에는 다섯 가지가 있다
첫번째 카드를 나열하고 난 다음, 두번째 카드를 선택하는 방법에는 네 가지가 있다
두번째 카드를 나열하고 난 다음, 세번째 카드를 선택하는 방법에는 세 가지가 있다

// 순열은 일반화 과정을 거쳐, Permutation의 약자 P로 표현한다
5장에서 3장을 선택하는 모든 순열의 수 = 5P3 = (5 X 4 X 3 X 2 X 1) / (2 X 1) = 60
```

```js
//순열
const getPermutations = function (arr, selectNumber) {
  // - 순열을 담을 배열 설정
  const results = [];

  // - base case: 숫자가 한개라면 숫자 그대로 배열로 반환
  if (selectNumber === 1) return arr.map((value) => [value]);

  // - recursive case: arr을 순회하면서 각 숫자들을 fixed하여 첫번째 수로 만든다.
  arr.forEach((fixed, index, origin) => {
    // - fixed를 제외한 나머지 배열을 만든다.
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];

    // - 나머지에 대해서 재귀함수를 통해 순열을 만든다.
    const permutations = getPermutations(rest, selectNumber - 1);

    // - 각각 만들어진 순열 앞에 고정시킨 수(fixed)를 넣는다.
    const attached = permutations.map((permutation) => [fixed, ...permutation]);

    // - 그리고 만들어진 순열들을 스프레드 연산자로 result에 push한다.
    results.push(...attached);
  });

  // - result를 반환
  return results;
};
```

예를 들어 카드를 3장 뽑을 때, [A, B, D]와 [A, D, B] 두 경우 모두 A, B, 그리고 D라는 같은 카드를 3장 선택했지만, 나열하는 순서가 다르므로 서로 다른 경우로 파악해야 한다.

![](https://blog.kakaocdn.net/dn/k5rC0/btruVLslbPe/KAdvIkKYpP24Bsy18PEdE0/img.png)

일반식 : nPr = n! / (n - r)!

! : 팩토리얼(factorial) → n! 은 n에서부터 1씩 감소하여 1까지의 모든 정수의 곱이다(n 보다 작거나 같은 모든 양의 정수의 곱)

```
5! = 5 X (5 - 1) X (5 - 2) X (5 - 3) X (5 - 4) = 5 X 4 X 3 X 2 X 1 = 120
팩토리얼에서 0!과 1!은 모두 1이다.
```

```
→ 순서를 생각하지 않고 3장을 선택하는 조건을 만족하는 모든 경우의 수
2번 조건에서 모든 경우의 수를 구할 때는 3장을 하나의 그룹으로 선택해야 한다.
2번의 조건을 만족하려면, 다음과 같은 방법으로 경우의 수를 구한다.

1. 순열로 구할 수 있는 경우를 찾는다.
2. 순열로 구할 수 있는 경우에서 중복된 경우의 수를 나눈다.

만약 순열처럼 순서를 생각하여 경우의 수를 센다면, 조합으로써 올바르지 않다.

예를 들어 순열에서 [A, B, C], [A, C, B], [B, A, C], [B, C, A], [C, A, B], [C, B, A]의 여섯 가지는
모두 다른 경우로 취급하지만, 조합에서는 이 여섯 가지를 하나의 경우로 취급한다.
다시 말해 순열에서처럼 순서를 생각하여 선택하면, 중복된 경우가 6배 발생한다.

여기서 나온 여섯 가지 경우의 수는 3장의 카드를 순서를 생각하여 나열한 모든 경우의 수이다.
3장의 카드를 순열 공식에 적용한 결과가 3! / (3-3)! = (3 X 2 X 1) / 1 = 6

순서를 생각하느라 중복된 부분이 발생한 순열의 모든 가짓수를
중복된 6가지로 나누어 주면 조합의 모든 경우의 수를 얻을 수 있다.

따라서 (5 X 4 X 3 X 2 X 1) / ((3 X 2 X 1) X (2 X 1)) = 10
5장에서 3장을 무작위로 선택하는 조합에서 모든 경우의 수 = 5C3 = 5! / (3! * 2!) = 10
조합은 일반화 과정을 거쳐, Combination의 약자 C로 표현한다.
```

![](https://blog.kakaocdn.net/dn/cMiLeb/btruVLFPGcf/1OPFWyaOQrHSgBJXd4xjEK/img.png)

일반식: nCr = n! / (r! \* (n - r)!)

```js
const getCombinations = function (arr, selectNumber) {
  // - 순열을 담을 배열 설정
  const results = [];

  // - base case: 숫자가 한개라면 숫자 그대로 배열로 반환
  if (selectNumber === 1) return arr.map((value) => [value]);

  // - recursive case: arr을 순회하면서 각 숫자들을 fixed하여 첫번째 수로 만든다.
  arr.forEach((fixed, index, origin) => {
    const rest = origin.slice(index + 1);

    // - 나머지에 대해서 재귀함수를 통해 순열을 만든다.
    const combinations = getCombinations(rest, selectNumber - 1);

    // - 각각 만들어진 순열 앞에 고정시킨 수(fixed)를 넣는다.
    const attached = combinations.map((combination) => [fixed, ...combination]);

    // - 그리고 만들어진 순열들을 스프레드 연산자로 result에 push한다.
    results.push(...attached);
  });

  // - result를 반환
  return results;
};
```

```js
//중복순열
const getPermutations = function (arr, selectNumber) {
  // - 순열을 담을 배열 설정
  const results = [];

  // - base case: 숫자가 한개라면 숫자 그대로 배열로 반환
  if (selectNumber === 1) return arr.map((value) => [value]);

  // - recursive case: arr을 순회하면서 각 숫자들을 fixed하여 첫번째 수로 만든다.
  arr.forEach((fixed, index, origin) => {
    // 중복이 허용된다.
    const rest = origin.slice();

    // - 나머지에 대해서 재귀함수를 통해 순열을 만든다.
    const permutations = getPermutations(rest, selectNumber - 1);

    // - 각각 만들어진 순열 앞에 고정시킨 수(fixed)를 넣는다.
    const attached = permutations.map((permutation) => [fixed, ...permutation]);

    // - 그리고 만들어진 순열들을 스프레드 연산자로 result에 push한다.
    results.push(...attached);
  });

  // - result를 반환
  return results;
};
```

```
소수 찾기

한 자리 숫자가 적힌 종잇조각이 흩어져 있습니다. 흩어진 종잇조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.
종이에 기록된 모든 숫자가 배열로 주어진다면, 이 종잇조각으로 만들 수 있는 소수는 몇 개인가요?

// 순열을 사용하여 전략 세우기
n 개의 숫자 중에 1~k 개를 뽑아서 순열을 생성한다.
각 순열을 정수로 변환하고, 해당 정수가 중복되지 않으면서 동시에 소수인지 검사한다.
소수이면 개수를 센다.

숫자는 순서에 의해 전혀 다른 값이 될 수 있다. 예를 들어 123과 321은 전혀 다른 숫자다.
만약 이 문제를 조합으로 접근하게 된다면, 123과 321은 같은 경우로 취급한다.
따라서, 순서를 고려하지 않고 k 개를 뽑아내는 조합으로 이 문제를 해결할 수 없다.
```

```
일곱 난쟁이

왕비를 피해 일곱 난쟁이와 함께 평화롭게 생활하고 있던 백설 공주에게 위기가 찾아왔습니다.
하루일과를 마치고 돌아온 "일곱" 난쟁이가 "아홉" 명이었던 겁니다.
아홉 명의 난쟁이는 모두 자신이 "백설 공주와 일곱 난쟁이"의 주인공이라고 주장했습니다.
(뛰어난 수학적 직관력을 가지고 있던) 백설 공주는 일곱 난쟁이의 키의 합이 100임을 기억해 냈습니다.
아홉 난쟁이 각각의 키가 주어질 때, 원래 백설 공주와 평화롭게 생활하던 일곱 난쟁이를 찾는 방법은 무엇인가요?

// 조합을 이용하여 찾아보기
모든 일곱 난쟁이의 키를 합했을 때 100이 된다고 주어졌기 때문에,
9명의 난쟁이 중 7명의 난쟁이를 순서를 생각하지 않고, 난쟁이 7명의 키를 합했을 때 100이 되는 경우를 찾으면 된다.
```

### ② GCD / LCM(최대공약수, 최대공배수)

```
‣ 약수: 어떤 수를 나누어떨어지게 하는 수
‣ 배수: 어떤 수의 1, 2, 3, ...n 배하여 얻는 수

‣ 공약수: 둘 이상의 수의 공통인 약수
‣ 공배수: 둘 이상의 수의 공통인 배수

‣ 최대공약수(GCD. Greatest Common Divisor): 둘 이상의 공약수 중에서 최대인 수
‣ 최소공배수(LCM. Least Common Multiple): 둘 이상의 공배수 중에서 최소인 수
```

✷ 최대공약수와 최소공배수를 나눗셈으로 구하는 방법(12와 18의 최대공약수와 최소공배수를 구하는 예시)

![](https://blog.kakaocdn.net/dn/csgPKM/btruTDaxA7y/LuWgspn52Q6uRQQMJYhsuk/img.png)

✷ 숫자가 세 개일 때 최소공배수 구하는 방법

![](https://blog.kakaocdn.net/dn/bextVp/btruYT44tFt/O51ScKU10VU2K1c6UAHhRK/img.png)

✷ 소인수분해를 이용하여 최대공약수 / 최소공배수 구하는 방법

![](https://blog.kakaocdn.net/dn/dWjZ5P/btruWRsEH8d/Q2z2zXUkrKFQda0xrWfPM0/img.png)

![](https://blog.kakaocdn.net/dn/c9QCiC/btruThzwFCi/K7e2Apznd25txA6RBwDLLK/img.png)

![](https://blog.kakaocdn.net/dn/movKF/btruYTxcswp/SJ313kxGS5KUZ0zKv23EA0/img.png)

```
Mask States

방역용 마스크를 제작/판매하는 Mask States 사는 이례적인 전염성 독감 예방을 위해 기존 가격을 유지하며
약속된 물량의 방역용 마스크를 제공하고 있습니다.
이 회사는 사장을 포함하여 A, B, C 세 명뿐이고, 이들 모두 마스크를 제작합니다.

각각의 제작 속도는 다음과 같습니다.
A는 55분마다 9개를, B는 70분마다 15개를, C는 85분마다 25개의 방역용 마스크를 만들 수 있습니다.
이 회사의 사람들은 05:00 시부터 동시에 마스크를 만들기 시작하여
각 55분, 70분, 85분 동안 연속으로 마스크를 제작한 후, 5분씩 휴식을 취합니다.
이들 세 명이 처음으로 동시에 쉬는 시점이 퇴근 시간이라면, 이날 하루에 제작한 마스크는 모두 몇 개인가요?
(휴식시간과 퇴근시간이 겹치는 경우, 휴식을 취한 뒤 퇴근합니다.)

// 최소 공배수 개념을 사용하여 문제 풀이
A, B, C의 작업 시간과 쉬는 시간 5분을 더하면 A, B, C는 각각 60분, 75분, 90분마다 마스크를 만든다.
세 명이 동시에 휴식을 취하는 시점은 세 명이 쉬고 난 직후가 같을 시점이 된다.
쉬고 난 직후가 처음으로 같을 시점을 구해야 하므로 공배수와 최소 공배수의 개념을 알아야 한다.

LCM(60, 75, 90)은 900
(LCM; Least Common Multiple, 최소 공배수)

A는 B, C와 휴식을 취한 직후가 처음으로 같을 시점까지 900/60 = 15 번 작업하고,
15번 X 9개 = 135개의 마스크를 만들어 낸다.
B는 900/75 = 12번의 작업을 반복하고 12턴 X 15개 = 180개,
C는 900/90 = 10번의 작업을 반복하고 10턴 X 25개 = 250개의 마스크를 만들어 낸다.

A, B, C가 하루에 제작한 마스크의 총 개수는 135개 + 180개 + 250개 = 565개가 된다.
```

![](https://blog.kakaocdn.net/dn/c6TKUN/btruWP8ODNk/tpaNhjb331xhlzNXkfIi60/img.png)

```
조명 설치

코드스테이츠 라운지에 있는 가로 24cm, 세로 12cm인 직사각형 모양 조형물의 가장자리에 조명을 설치하려고 합니다.
네 모퉁이에는 조명을 반드시 설치해야하고, 나머지 조명은 일정한 간격으로 설치하려고 할 때,
필요한 최소한의 조명 개수는 몇 개일까요?
이 때, 꼭지점을 제외한 직사각형의 모든 변에는 최소 하나 이상의 조명이 반드시 설치되어야 합니다.
(단, 설치한 조명의 간격은 정수로 이루어진 cm 단위입니다.)

모든 조명을 일정한 간격으로 설치해야 하므로, 가로변과 세로변의 공약수를 구해야 한다.
가로와 세로 각각 나누어서 나머지가 없이 떨어지는 수들을 나열한 뒤, 공통된 수만 모으면 공약수를 구할 수 있다.

그리고 공약수를 기준으로 조명을 설치하면, 길이가 다른 가로와 세로여도 일정한 간격으로 나누어 조명을 설치할 수 있다.
최소로 필요한 조명의 개수를 파악해야 하기 때문에 최대 공약수가 필요하다.

GCD(12, 24)는 12 (GCD; Greatest Common Divisor, 최대 공약수)
네 모퉁이는 반드시 설치해야 하므로 각 변의 길이를 최대 공약수 12로 나누어 최소로 필요한 조명의 개수를 구할 수 있다.
(12/12 + 24/12) X 2 = 3 X 2 = 6개

이 문제에서는 꼭지점을 제외한 직사각형의 모든 변에, 최소 하나 이상의 조명이 설치되어야 하므로
12를 제외한 최대 공약수로 문제를 해결해야 한다.
(12/6 + 24/6) X 2 = 6 X 2 = 12개
```

### ③ 멱집합

한 집합의 모든 부분 집합. → 부분집합을 나열하는 방법에서 가장 앞 원소(혹은 임의의 집합 원소)가 있는지, 없는지에 따라 단계를 나누는 기준을 결정한다.

![](https://blog.kakaocdn.net/dn/en2sfs/btruXUilqeK/KaysthYk0JItU7SlE1QXzk/img.png)

```
Step A: 1을 제외한 {2, 3}의 부분집합을 나열한다.
Step B: 2를 제외한 {3}의 부분집합을 나열한다.
Step C: 3을 제외한 {}의 부분집합을 나열한다. → {}
Step C: {}의 모든 부분집합에 {3}을 추가한 집합들을 나열한다. → {3}

Step B: {3}의 모든 부분집합에 {2}를 추가한 집합들을 나열한다.
Step C: {3}의 모든 부분집합에 {2}를 추가한 집합들을 나열하려면,
{}의 모든 부분집합에 {2}를 추가한 집합들을 나열한 다음 {}의 모든 부분집합에 {2, 3}을 추가한 집합들을 나열한다.
→ {2}, {2, 3}

Step A: {2, 3}의 모든 부분집합에 {1}을 추가한 집합들을 나열한다.

Step B: {2, 3}의 모든 부분집합에 {1}을 추가한 집합들을 나열하려면,
{3}의 모든 부분집합에 {1}을 추가한 집합들을 나열한 다음 {3}의 모든 부분집합에 {1, 2}를 추가한 집합들을 나열한다.

Step C: {3}의 모든 부분집합에 {1}을 추가한 집합을 나열하려면,
{}의 모든 부분집합에 {1}을 추가한 집합들을 나열한 다음 {}의 모든 부분집합에 {1, 3}을 추가한 집합들을 나열한다.
→ {1}, {1, 3}

Step C: {3}의 모든 부분집합에 {1, 2}를 추가한 집합을 나열하려면,
{}의 모든 부분집합에 {1, 2}를 추가한 집합들을 나열한 다음 {}의 모든 부분집합에 {1, 2, 3}을 추가한 집합들을 나열한다.
→ {1, 2}, {1, 2, 3}

→ 원소가 있는지, 없는지 2가지 경우를 고려하기 때문에 집합의 요소가 n 개일 때 모든 부분집합의 개수는 2ⁿ개 이다.
```

→ 멱집합에 대한 설명이 트리구조와 비슷함을 알 수 있지만, 정확하게 멱집합이 트리 문제라고 말할 수는 없음.

→ 멱집합을 구하는 방법에서 각 단계에서 순환구조를 보이며, 이는 문제를 작은 단위로 줄여나가는 재귀를 응용할 수 있음을 알 수 있다.(문제가 가장 작은 단위로 줄어들고, 함수가 리턴될 때 카운트를 올리는 방식으로 멱집합의 개수 구하기).

✷ 순환구조: 임의의 원소를 제외하면서 집합을 작은 단위로 줄여나가는 방법

## 2. 정규식

**문자열에서 특정한 문자를 찾아내는 도구** → 특정한 규칙을 갖는 문자열로 이루어진 표현식

### ① 이메일 유효성 검사

```js
let regExp =
  /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
```

### ② 휴대폰 번호 유효성 검사

```js
let regExp = /^01([0|1|6|7|8|9]?)-?([0-9]{3,4})-?([0-9]{4})$/;
```

### ③ 알고리즘 문제에 정규표현식 적용하기

```js
// 문자열 str 이 주어질 때, str의 길이가 5 또는 7이면서 숫자로만 구성되어 있는지를 확인해 주는 함수를 작성하세요.
// 결과는 Boolean으로 리턴됩니다. 예를 들어 str가 c2021이면 false, 20212이면 true를 리턴합니다.

function solution(str) {
  return /^\d{5}$|^\d{7}$/.test(str);
}
```

## 2-1. 정규표현식 사용하기

### ① 리터럴 패턴

```js
let pattern = /c/;
// 슬래시(/)로 감싸 사용한다.
// 슬래시 안에 들어온 문자열이 찾고자 하는 문자열이다.
// 'c 를 찾을 거야!' 라고 컴퓨터에게 명령을 내리는 것.
// 찾고 싶은 c를 pattern 이라는 변수에 담아놨기 때문에 이 변수를 이용하여 c 를 찾을 수 있다.
```

### ② 생성자 함수 호출 패턴

```js
let pattern = new RegExp("c");
// RegExp 객체의 생성자 함수를 호출하여 사용한다.
// new 를 이용해서 정규 표현식 객체를 생성하고,
// 리터럴 패턴과 동일하게 'c 를 찾을 거야!' 라는 명령.
```

## 2-2. 정규표현식 내장 메소드

내장 메소드를 사용하여 어떤 문자열 안에 원하는 정보를 찾거나 특정 패턴에 대응하는 문자열을 검색, 추출, 다른 문자열로 치환 가능.

### ① exec()

execution, 원하는 정보를 뽑아내고자 할 때 사용한다.

→ 검색의 대상이 찾고자 하는 문자열에 대한 정보를 갖고 있다면 이를 배열로 치환, 찾는 문자열이 없으면 null 반환.

```js
let pattern = /a/; // 찾고자 하는 문자열
pattern.exec("apple"); // 검색하려는 대상을 exec 메소드의 첫 번째 인자로 전달.

// 즉, 'apple'이 'a' 를 포함하고 있는지 확인.
// 이 경우 'a' 가 포함되어 있으므로, ['a'] 를 반환.
```

### ② test()

찾고자 하는 문자열이 대상 안에 있는 지에 대한 여부를 boolean으로 리턴.

```js
let pattern = /a/;
pattern.test("apple");
// 이 경우는 'apple'이 'a'를 포함하고 있으므로 true.
```

### ③ match()

RegExp.exec()과 비슷한 기능을 함. 정규 표현식을 인자로 받아 주어진 문자열과 일치된 결과를 배열로 반환, 없으면 null.

```js
let pattern = /a/;
let str = "apple";
str.match(pattern);
// str 안에 pattern 이 포함되어 있으므로, ['a'] 를 반환.
```

### ④ replace()

```js
let pattern = /a/;
let str = "apple";
str.replace(pattern, "A");
// str 안에서 pattern 을 검색한 후 'A' 로 변경하여 결과 리턴.
// 여기서는 'Apple' 반환.
```

### ⑤ split()

주어진 인자를 구분자로 삼아 문자열을 부분 문자열로 나누어 그 결과를 배열로 반환.

```js
"123,456,789".split(","); // ["123", "456", "789"]
"12304560789".split("0"); // ["123", "456", "789"]
```

### ⑥ search()

정규 표현식을 인자로 받아 가장 처음 매칭되는 부분의 문자열 위치 반환. 매칭되는 문자열이 없을 경우 -1 반환.

```js
"JavaScript".search(/script/); // -1 대소문자를 구분합니다
"JavaScript".search(/Script/); // 4
"codestates".search(/ode/); // 1
```

## 2-3. flag

정규 표현식에서 추가적인 검색 옵션의 역할을 함. 각자 혹은 함께 사용하는 것이 모두 가능, 순서 구분이 없음

### ① i

대소문자 구분 X

```js
let withi = /c/i;
let withouti = /c/;
"Codestates".match(withi); // ['C']
"Codestates".match(withouti); // null
```

### ② g

global, 검색된 모든 결과 리턴.

```js
let withg = /c/g;
let withoutg = /c/;
"coolcodestates".match(withg); // ['c', 'c']
"coolcodestates".match(withoutg); // ['c'] g 가 없으면 첫 번째 검색 결과만 반환
```

### ③ m

다중행 검색.

```js
let str = `1st : cool
2nd : code
3rd : states`;
str.match(/c/gm);
// 3개의 행을 검색하여 모든 c 를 반환
// ['c', 'c']
str.match(/c/m);
// m은 다중행을 검색하게 해 주지만,
// g 를 빼고 검색하면 검색 대상을 찾는 순간 검색을 멈추기 때문에
// 첫 행의 ['c'] 만 리턴
```

## 2-4. 정규식 패턴

### ① Anchors - ^ and $

```js
^

문자열의 처음. 문자열에서 ^뒤에 붙은 단어로 시작하는 부분을 찾는다.
일치하는 부분이 있더라도, 그 부분이 문자열의 시작 부분이 아니면 null 을 리턴한다.

"coding is fun".match(/^co/); // ['co']
"coding is fun".match(/^fun/); // null
```

```js
$

문자열의 끝. 문자열에서 $앞의 표현식으로 끝나는 부분을 찾는다.

^와 비슷하지만 ^는 문자열의 시작을 찾는 반면, $는 문자열의 마지막 부분을 찾는다.
마찬가지로 일치하는 부분이 있더라도, 그 부분이 문자열의 끝부분이 아니면 null 을 리턴한다.

"coding is fun".match(/un$/); // ['un']
"coding is fun".match(/is$/); // null
"coding is fun".match(/^coding is fun$/);
// 문자열을 ^ 와 $ 로 감싸주면 그 사이에 들어간 문자열과 정확하게 일치하는 부분을 찾는다
// ["coding is fun"]
```

### ② Quantifiers — \*, +, ? and {}

```js
*

* 바로 앞의 문자가 0번 이상 나타나는 경우를 검색한다.

아래와 같은 문자열이 있을 때에 /ode*/g 을 사용하게 되면 "od" 가 들어가면서 그 뒤에 "e"가 0번 이상 포함된 모든 문자열을 리턴한다.

"co cod code codee coding codeeeeee codingding".match(/ode*/g);
// ["od", "ode", "odee", "od", "odeeeeee", "od"]
```

```js
+

+ 도 * 와 같은 방식으로 작동, 다만 + 바로 앞의 문자가 1번 이상 나타나는 경우를 검색한다는 점이 다르다.

// ["ode", "odee", "odeeeeee"]
"co cod code codee coding codeeeeee codingding".match(/ode*/g);
```

```js
?

? 앞의 문자가 0번 혹은 1번 나타나는 경우만 검색한다.
*? 또는 +? 와 같이 ?는 * 혹은 + 와 함께 쓰는 것도 가능하다.

"co cod code codee coding codeeeeee codingding".match(/ode?/g);
// ["od", "ode", "ode", "od", "ode", "od"]

"co cod code codee coding codeeeeee codingding".match(/ode*?/g);
// ["od", "od", "od", "od", "od", "od"]

"co cod code codee coding codeeeeee codingding".match(/ode+?/g);
// ["ode", "ode", "ode"]
```

```js
{}

*, *?, +, +? 의 확장판으로 생각할 수 있다.

*, *?, +, +? 가 '0개 이상' 또는 '1개 이상' 검색이 전부였던 반면, {}는 직접 숫자를 넣어서 연속되는 개수를 설정할 수 있다.

// 2개의 "e"를 포함한 문자열을 검색
// ["odee", "odee"]
"co cod code codee coding codeeeeee codingding".match(/ode{2}/g);

// 2개 이상의 "e"를 포함한 문자열을 검색한다.
// ["odee", "odeeeeee"]
"co cod code codee coding codeeeeee codingding".match(/ode{2,}/g);

// 2개 이상 5개 이하의 "e"를 포함한 문자열을 검색한다.
// ["odee", "odeeeee"]
"co cod code codee coding codeeeeee codingding".match(/ode{2,5}/g);
```

```js
OR operator

| 는 or 조건으로 검색하여 | 의 왼쪽 또는 오른쪽의 검색 결과를 반환한다.

"Cc Oo Dd Ee".match(/O|D/g); // ["O", "D"]
"Cc Oo Dd Ee".match(/c|e/g); // ["c", "e"]
"Cc Oo Dd Ee".match(/D|e/g); // ["D", "e"]
"Ccc Ooo DDd EEeee".match(/D+|e+/g);
// + 는 1번 이상 반복을 의미하기 때문에
// ["DD", "eee"] 를 반환한다.
```

```js
Bracket Operator - []

대괄호 [] 안에 명시된 값을 검색한다.

// a or b or c 를 검색합니다. or(|) Operator 로 작성한 a|b|c 와 동일하게 작동한다.
[abc]

// [abc] 와 동일하다. - 로 검색 구간을 설정할 수 있다.
[a-c]


// [] 에 + 등의 기호를 함께 사용할 수도 있다.
// C or D 가 한 번 이상 반복된 문자열을 반복 검색하기 때문에
// ["C", "DD"] 가 반환된다.
// [] 에 + 등의 기호를 함께 사용할 수도 있다.
"Ccc Ooo DDd EEeee".match(/[CD]+/g);


// ["cc", "oo"]
"Ccc Ooo DDd EEeee".match(/[co]+/g);

// - 때문에 c ~ o 구간을 검색하여
// ["cc", "oo", "d", "eee"] 가 반환된다.
"Ccc Ooo DDd EEeee".match(/[c-o]+/g);


// a~z 또는 A~Z 에서 한 번 이상 반복되는 문자열을 반복 검색하기 때문에
// ["AA", "ZZ", "Ad", "Az", "dd", "zz"] 를 반환한다.
"AA 12 ZZ Ad %% Az !# dd 54 zz".match(/[A-Za-z]+/g);


// flag i 는 대소문자를 구분하지 않기 때문에 위와 동일한 결과를 반환한다.
// ["AA", "ZZ", "Ad", "Az", "dd", "zz"]
"AA 12 ZZ Ad %% Az !# dd 54 zz".match(/[A-Z]+/gi);


// 숫자도 검색 가능.
// ["12", "54"]
"AA 12 ZZ Ad %% Az !# dd 54 zz".match(/[0-9]+/g);


// [] 안에 ^ 를 사용하면 anchor 로서의 문자열의 처음을 찾는것이 아닌
// 부정을 나타내기 때문에 [] 안에 없는 값을 검색한다.
// ["$#67", "@9"]
"aAbB$#67Xz@9".match(/[^a-zA-Z]+/g);
```

### ③ Character classes

#### \d & \D

‣ \d 의 d 는 digit. 0 ~ 9 사이의 숫자 하나를 검색한다. [0-9] 와 동일함.

‣ \D 는 not Digit. 숫자가 아닌 문자 하나를 검색한다. [^0-9] 와 동일함.

```js
"abc34".match(/\d/); // ["3"]
"abc34".match(/[0-9]/); // ["3"]
"abc34".match(/\d/g); // ["3", "4"]
"abc34".match(/[0-9]/g); // ["3", "4"]
"abc34".match(/\D/); // ["a"]
"abc34".match(/[^0-9]/); // ["a"]
"abc34".match(/\D/g); // ["a", "b", "c"]
"abc34".match(/[^0-9]/g); // ["a", "b", "c"]
```

#### \w & \W

‣ \w 는 알파벳 대소문자, 숫자, _(underbar) 중 하나를 검색한다. [a-zA-Z0-9_]와 동일함.

‣ \W 는 알파벳 대소문자, 숫자, _ (underbar)가 아닌 문자 하나를 검색한다. [^a-zA-Z0-9_]와 동일함.

```js
"ab3_@A.Kr".match(/\w/); //["a"]
"ab3_@A.Kr".match(/[a-zA-Z0-9_]/); // ["a"]
"ab3_@A.Kr".match(/\w/g); //["a", "b", "3", "_", "A", "K", "r"]
"ab3_@A.Kr".match(/[a-zA-Z0-9_]/g); // ["a", "b", "3", "_", "A", "K", "r"]

"ab3_@A.Kr".match(/\W/); // ["@"]
"ab3_@A.Kr".match(/[^a-zA-Z0-9_]/); // ["@"]
"ab3_@A.Kr".match(/\W/g); // ["@", "."]
"ab3_@A.Kr".match(/[^a-zA-Z0-9_]/g); // ["@", "."]
```

### ④ Grouping and capturing

#### grouping

```js
()

그룹으로 묶는다는 의미 이외에도 다른 몇 가지 의미가 더 있다.
그룹화 표현식의 일부를 ()로 묶어주면 그 안의 내용을 하나로 그룹화할 수 있다.

let co = 'coco';
let cooo = 'cooocooo';

co.match(/co+/); // ["co", index: 0, input: "coco", groups: undefined]
cooo.match(/co+/); // ["cooo", index: 0, input: "cooocooo", groups: undefined]

co.match(/(co)+/); // ["coco", "co", index: 0, input: "coco", groups: undefined]
cooo.match(/(co)+/); // ["co", "co", index: 0, input: "cooocooo", groups: undefined]
```

co+ 는 "c"를 검색하고 + 가 "o"를 1회 이상 연속으로 반복되는 문자를 검색해 주기 때문에 "cooo"가 반환되었다.

하지만 (co)+ 는 "c" 와 "o" 를 그룹화하여 "co"를 단위로 1회 이상 반복을 검색하기 때문에 "coco"가 반환되었다.

여기서 특이한 점은 일치하는 문자열로 반환된 결과가 2개다. 캡처 () 로 그룹화한다고 하였고, 이를 캡처한다 라고 한다.

#### capturing

```js
// 캡쳐했을 경우 작동방식
co.match(/(co)+/); // ["coco", "co", index: 0, input: "coco", groups: undefined]

() 로 "co"를 캡처
캡처한 "co" 는 일단 당장 사용하지 않고, + 가 "co"의 1회 이상 연속 반복을 검색
이렇게 캡처 이외 표현식이 모두 작동하고 나면, 캡처해 두었던 "co"를 검색
```

따라서 2번 과정에 의해 "coco" 가 반환되고, 3번에 의해 "co"가 반환된다.

ex)

```js
"2021code".match(/(\d+)(\w)/);
// ["2021c", "2021", "c", index: 0, input: "2021code", groups: undefined]

() 안의 표현식을 순서대로 캡처 ⇒ \d+ 와 \w
캡처 후 남은 표현식으로 검색 ⇒ 이번 예시에는 남은 표현식은 없습니다.
\d 로 숫자를 검색하되 + 로 1개 이상 연속되는 숫자를 검색 ⇒ 2021
\w 로 문자를 검색 ⇒ c
3번과 4번이 조합되어 "2020c" 가 반환
첫 번째 캡처한 (\d+) 로 인해 2021 이 반환
두 번째 캡처한 (\w) 로 인해 "c" 가 반환
```

**문자열 대체 시 캡처된 값 참조**. 캡처된 값은 replace() 메소드를 사용하여 문자 치환 시 참조 패턴으로 사용될 수 있다.

ex)

```js
"code.states".replace(/(\w+)\.(\w+)/, "$2.$1"); //states.code
```

우선 첫 번째 (\w+) 가 code 를 캡처하고, 두 번째 (\w+) 가 states 를 캡처한다.

(/(\w+)\ 와 (\w+)/\사이의 . 은 . 앞에 역슬래시가 사용되었기 때문에 '임의의 한 문자'가 아닌 기호로서의 온점 . 을 의미한다.)

각 캡처된 값은 첫 번째는 $1 이 참조, 두 번째는 $2 이 참조하기 때문에 이 참조된 값을 "$2.$1" 이 대체하게 되어 code 와 states 가 뒤바뀐 "states.code" 가 반환된다.

#### non-capturing

()를 사용하면 그룹화와 캡처를 한다고 하였지만 (?:)로 사용하면 그룹은 만들지만 캡처는 하지 않는다.

```js
let co = "coco";

co.match(/(co)+/); // ["coco", "co", index: 0, input: "coco", groups: undefined]

co.match(/(?:co)+/);
// ["coco", index: 0, input: "coco", groups: undefined]
// 위 "캡처" 예시의 결괏값과 비교해보기
```

#### lookahead

(?=) 는 검색하려는 문자열에 (?=여기) 에 일치하는 문자가 있어야 (?=여기) 앞의 문자열을 반환한다.

```js
// ab 가 c 앞에 있기 때문에 ["ab"] 를 반환한다.
"abcde".match(/ab(?=c)/);

// d 의 앞은 "abc" 이기 때문에 null 을 반환한다.
"abcde".match(/ab(?=d)/);
```

#### negated lookahead

(?!) 는 (?=) 의 부정.

```js
"abcde".match(/ab(?!c)/); // null
"abcde".match(/ab(?!d)/); // ["ab"]
```

### ✷ 정규식 패턴(표현식)

| 정규식 패턴 |                                     설명                                      |
| :---------: | :---------------------------------------------------------------------------: |
|      ^      |                        줄(Line)의 시작에서 일치 /^abc/                        |
|      $      |                         줄(Line)의 끝에서 일치 /xyz$/                         |
|      .      |                 (특수기호, 띄어쓰기를 포함한) 임의의 한 문자                  |
|   a or b    |                         인덱스가 작은 것을 우선 반환                          |
|     \*      |       0회 이상 연속으로 반복되는 문자와 가능한 많이 일치. {0,} 와 동일        |
|     \*?     |        0회 이상 연속으로 반복되는 문자와 가능한 적게 일치. {0} 와 동일        |
|      +      |       1회 이상 연속으로 반복되는 문자와 가능한 많이 일치. {1,} 와 동일        |
|     +?      |        1회 이상 연속으로 반복되는 문자와 가능한 적게 일치. {1} 와 동일        |
|     {3}     |                              숫자 3개 연속 일치                               |
|    {3,}     |                              3개 이상 연속 일치                               |
|   {3, 5}    |                          3개 이상 5개 이하 연속 일치                          |
|     ()      |                             캡쳐(capture)할 그룹                              |
|    [a-z]    |                 a부터 z 사이의 문자 구간에 일치(영어 소문자)                  |
|    [A-Z]    |                 A부터 Z 사이의 문자 구간에 일치(영어 대문자)                  |
|    [0-9]    |                     0부터 9 사이의 문자 구간에 일치(숫자)                     |
| \(역슬래쉬) |  escape 문자. 특수 기호 앞에 \를 붙이면 정규식 패턴이 아닌, 기호 자체로 인식  |
|     \d      |                         숫자를 검색함. /[0-9]/와 동일                         |
|     \D      |                  숫자가 아닌 문자를 검색함. /[^0-9]/와 동일                   |
|     \w      |       영어대소문자, 숫자, (underscore)를 검색함. /[A-Za-z0-9]/ 와 동일        |
|     \W      | 영어대소문자, 숫자, (underscore)가 아닌 문자를 검색함. /[^a-za-z0-9]/ 와 동일 |
|     [^]     |           []안의 문자열 앞에 ^이 쓰이면, []안에 없는 문자를 검색함            |
