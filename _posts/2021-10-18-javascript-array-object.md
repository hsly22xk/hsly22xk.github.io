---
layout: single
title: "D+15 배열과 객체"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

자바스크립트의 배열과 객체.

## 1. 배열

고유한 순서번호(인덱스, index)가 있는 값(값 = 요소 = element).

여러 개의 데이터를 하나에 담을 수 있는 통? 같은 거. 다만 순서가 정해져 있고, 담겨있는 데이터들은 연관이 되어있음을 알면 되겠다.

① 순서는 0부터 번호매김(인덱스넘버) 시작(0번째 인덱스의 값, 1번째 인덱스의 값 ~~~ )

배열의 기본 문법: 변수 선언 후 배열은 변수 뒤에 [ ]대괄호를 이용하여 만들고 각각의 요소는 , 쉼표를 써서 구분해준다.

ex)

```javascript
let number [ 1, 2, 3, 4, 5 ]; // 하나의 변수 안에 여러 개의 값을 넣을 수 있다.
```

② 값은 인덱스를 이용해 접근한다.

⇒ 변수라는 배열의 n번째 인덱스(인덱스 넘버 n)를 조회하려면 변수[n]; 이라는 형식으로 할 수 있다.

⇒ 변수라는 배열의 n번째 인덱스의 값을 변경하려면 변수[n] = 변경할 값; 으로 할당해준다.

- 만약 배열에 없는 인덱스 넘버의 값을 조회하면 undefined로 나온다.

- 만약 배열의 길이(arr.length)가 0이라면 undefined로 나온다.

ex)

```javascript
let fruit = ["apple", "banana", "orange"];

// (3)은 배열의 요소가 3개라는 뜻. 인덱스 넘버와는 다르다.
console.log(fruit); // (3) ['apple', 'banana', 'orange']

// 순서번호는 0부터 시작이기 때문에 1번째는 banana.
console.log(fruit[1]); // banana

// 배열에 없는 순서번호를 조회함
console.log(fruit[3]); // undefined
```

- 함수가 갖고 있는 한계를 극복할 수 있는 방법이 배열이다.

\*함수가 갖고 있는 한계?

기존에 배웠을 때는 함수를 호출하고 변수를 하나씩만 담아 리턴했었다. 하나씩 리턴했던 그 값들을 전부 배열로 모을 수 있다.

ex)

```javascript
function drinks() {
  // 함수 이름을 복수 형태인 drinks로 지정하고, 선언한다.
  return ["coffee", "tea", "juice"];
  // 함수의 리턴값으로 배열을 리턴한다.
  // 배열이 담김으로서 함수는 하나지만 값을 여러 개 리턴할 수 있다.
}

// anything이라는 변수 안에 drinks()라는 함수를 할당한다.
let anything = drinks();

// anything안에 drinks()라는 함수의 리턴값인 배열이 담겼다.
anything; // (3) ['coffee', 'tea', 'juice']
```

③이중 배열

만약

```javascript
let number = [
  [13, 5],
  [40, 4],
  [3, 29],
];
```

라는 배열을 선언하고 할당했다고 가정해보자.

console창에 그냥 number 라고만 치면

```
number
(3) [Array(2), Array(2), Array(2)]

0: (2) [13, 5]
1: (2) [40, 4]
2: (2) [3, 29]
```

라는 말이 나온다.

앞에 소괄호로 쓰여진 (3)은 length, 즉 길이가 3 이라는 뜻이고 배열 안에 배열이 또 들어가 있다는 뜻이다.

이 배열의 0번째 인덱스는 길이가 2인 배열 [13, 5]이고 1번째 인덱스는 길이가 2인 배열 [40, 4]이고 2번째 인덱스는 길이가 2인 배열 [3, 29]이다.

즉 number라는 변수의 배열에서의 1번째 인덱스는 [40, 4] 가 되고, 1번째 인덱스의 0번째 인덱스는 40이 된다.

그렇다면 이걸 conosle창에 어떻게 쓸 수 있을까?

number[1]만 치면 [40, 4] 배열만 나온다. 1번째 인덱스의 0번째 인덱스는?

number[1] 뒤에 [0]만 붙여주면 40이라는 값이 나온다.

이것을 2차원 배열이라고 한다.

④ 배열로 할 수 있는 것들

배열의 이름.length; 라고 쓰면(변수.length) 배열의 길이를 알아낼 수 있다.

(⇒ 온점(dot)을 이용해서 변수가 가지고 있는 속성에 접근할 수 있다).

ex)

```javascript
let fruit = ["apple", "banana", "orange"];
console.log(fruit.length); // 3
```

⇒ fruit이라고 하는 배열에 담겨 있는 값이 몇 개인가?라는 것을 나타낸다.

⇒ 값의 개수와 순서번호(인덱스)는 다르다

- 요소(값, element)를 추가할 수 있다.

만약 let number [ 1, 2, 3, 4, 5 ] 끝에 6이라는 값을 추가하고 싶다면 number.push(6); 이라고 쓰면 된다(변수.push(추가할 값));

⇒ 온점(dot)을 이용해 관련된 명령(method)을 실행할 수도 있다. 명령을 실행할 때는 소괄호를 열고 닫는 형태로 실행한다.

- 요소를 삭제(제거)할 수 있다.

배열의 마지막 값을 삭제(제거)하고 싶다면 number.pop(); 이라고 쓰면 된다(변수.pop());

✷배열을 문자열로 변환하는 메소드

①arr.join(seperator) // 파라미터로 입력된 구분자

join() 함수는 배열의 모든 값들을 연결한 문자열을 리턴한다. 즉, 배열을 문자열로 리턴하게 만들어준다.

각각의 값들 사이에는 파라미터로 입력된 구분자가 들어감.

```
arr.join('-'); // 구분자로 '-'이 들어감.
arr.join(); // 아무것도 입력되지 않았으므로 구분자로 ','가 들어감.
arr.join('') // 파라미터로 비어있는 문자열이 전달, 배열의 각 값들을 구분자 없이 연결한 문자열이 리턴됨.
arr.join(' ') // 인자값이 공백(" ")으로 배열요소 사이사이에 공백을 더한 문자열로 변환함.
```

ex)

```javascript
let arr = ["abcde"];

arr.join("-") === ["a-b-c-d-e"];
arr.join() === ["a,b,c,d,e"];
arr.join("") === ["abcde"];
arr.join(" ") === ["a b c d e"];
```

② str.split(' '); // split 메소드는 주어진 인자로 문자열을 나눠 배열로 변환한다. 즉, 문자열을 배열로 리턴한다.

ex)

```javascript
str = 'abcde'
str.split(' ') = ['a' , 'b' , 'c' , 'd' , 'e' ]
// 띄어쓰기를 인자로 받아 띄어쓰기를 포함한 채로 문자열을 나눠 배열로 변환되었다.
```

③arr.toString() // 배열을 표현하는 문자열 반환

Array 객체에 대해 toString 메소드는 배열을 합쳐(join) 쉼표로 구분된 각 배열 요소를 포함하는 문자열 하나를 반환한다.

ex)

```javascript
let alphabets = ["a", "b", "c", "d", "e"];
let a = alphabets.toString(); // alphabets 안에 들어가 있는 문자열들을 a 안에 할당.
```

④ Array.from();

특정 길이의 문자열에서 배열을 반환할 수 있다.

```javascript
let num = "1234";
let arr = Array.from(num);
console.log(arr);
// (4) ['1', '2', '3', '4']
```

\*array.concat();

배열을 병합하는 매소드(고차함수 때 자세히 나옴)

```javascript
arr1.concat(arr2);
```

✅ arr.slice();

기존의 배열을 보존해야 하는 경우 배열의 전부 혹은 일부를 복사하여 원하는 작업을 수행할 수 있는 메소드.

```
arr.slice(start, end);
```

배열의 start에 해당하는 요소부터 end 바로 전의 요소까지를 선택하여 복사한 배열이 나온다.

ex)

```javascript
// start와 end에는 숫자가 들어간다.
// end에 값이 없으면 해당 배열의 마지막 요소까지 선택하고, 값이 음수면 마지막 요소를 기준으로 선택한다.

// 중간에 들어간 숫자는 정방향 인덱스 위치를 적어주기 위함. 실제 arr 아님.
arr = ([ 0 'coffee', 1 'tea', 2 'juice', 3 'ice cream' 4]);

arr.slice(1, 3);
// 시작 인덱스가 1번, 종료 인덱스가 3번이기 때문에 'tea'와 'juice'만 포함된다.
// ['tea', 'juice']


arr.slice(2);
// end값이 없을 때
// ['juice', 'ice cream']

arr.slice()
// 시작도 끝도 없는, 아예 인자를 주지 않았을 경우
// [ 'coffee', 'tea', 'juice', 'ice cream']
// 원본 배열이 그대로 복사되어 나온다.
```

- arr.splice();

ex)

```javascript
// 중간에 들어간 숫자는 정방향 인덱스 위치를 적어주기 위함. 실제 arr 아님.
arr = ([ 0 'coffee', 1 'tea', 2 'juice', 3 'ice cream' 4]);

arr.splice(1, 3, 'anything');
// 시작 인덱스 1번, 종료 인덱스 3번까지 없애고 그 사이에 'anything'을 넣어준다.
// ['coffee', 'anything', 'ice cream']
```

\*배열의 최대값 찾기

```javascript
Math.max.apply(null, arr);
Math.max(...arr);
```

[(spread문법에서 더 자세히 말함)](https://golddigger.tistory.com/24)

## 배열의 반복(배열과 반복문을 조합하여 응용하기)

반복문을 사용함으로써 리스트에 담긴 정보를 하나씩 꺼내어 처리할 수 있다.

ex)

```javascript
let number = [ 1, 2, 3, 4 ];

배열의 인덱스를 한 번씩 출력하라. ⇒console.log(num[n]); // 반복할 내용
```

```
조건

- 숫자 (n)은 0부터 시작한다. ⇒let n = 0; (초기화)
- 숫자 (n)은 언제까지 반복할까?

⇒ 배열의 길이에 따라 결정됨. ⇒ n < number.length; <-배열의 길이보다 작을 때까지 반복(조건식)

- 숫자 (n)은 1씩 증가한다. ⇒ n++(n = n + 1); // (증감문)
```

이제 for문으로 작성해 줄 수 있다.

```javascript
for (let n = 0; n < number.length; n++) {
  console.log(num[n]);
}
```

ex) number의 모든 elements를 누적해서 더하기 위한 조건과 반복할 구문은?

```javascript
let number = [10, 20, 40, 10];

let sum = 0;

for (let n = 0; n < number.length; n++) {
  sum = sum + number[n];
}

console.log(sum); // 80
```

- 첫번째 반복에는 0 + 10, 두번째 반복에는 10 + 20, 세번째 반복에는 30 + 40, 네번째 반복에는 70 + 10을 해줄 것이다.

첫번째 반복에서 더한 값이 두번째 반복에 들어가고, 두번째 반복에서 더한 값이 세번째 반복에, 세번째 반복에서 더한 값이 네번째 반복에 들어간다.

즉, 첫번째 반복은 sum + number[0], sum에 number의 0번째 인덱스를 더해준 값이다.

그러니 반복할 구문은 sum = sum + number[n] 이다.

위의 예시가 훨씬 수학적인데 다시 봤을 때 이해하기가 어려웠다.

그래서 나는 다시 봤을 때 내가 개념을 다시 이해할 수 있을 예시를 다시 들었다.

ex)

```javascript
function drinks() {
  return ["coffee", "tea", "juice"];
}

let anything = drinks();
// 배열의 길이에 따라 반복할 횟수가 정해짐.
for (i = 0; i < drinks.length; i++) {
  // document.write은 콘솔창이 아닌 페이지에 화면으로 출력한다는 뜻
  // toUpperCase()함수(기본적으로 제공하는 기능)의 역할은 drinks[i]에 담긴 문자를 전부 대문자로 바꿔준다.
  // 안쓰고 그냥 drinks[0]만 쓰면 0번째 인덱스에 해당하는 값만 나온다.
  // <br /n>은 줄바꿈 태그
  document.write(drinks[0].toUpperCase() + "<br /n>");
  document.write(drinks[1].toUpperCase() + "<br /n>");
  document.write(drinks[2].toUpperCase() + "<br /n>");
}

// 줄바꿈이 된 상태로
// coffee
// tea
// juice
// 라고 나온다.
```

줄바꿈이 된 채로 화면에 출력된다.

여기서 배열에 새로운 요소를 추가시키거나, 기존에 있던 요소를 제거하고 반복문을 실행시키면 추가된 새로운 요소는 아예 나오지 않고, 기존에 있던 요소는 나오지 않으면서 타입에러가 뜬다.

undefined된 요소를 toUpperCase함수로 불러올 수 없다는 것이다.

```javascript
function drinks() {
  return ["coffee", "tea", "juice"];
}

let anything = drinks();

// i를 0부터 시작해서 1씩 증가시킬 건데, i가 3보다 작을 때까지 반복문을 실행시킨다.
// 0,1,2가 나올 텐데, 여기서 0,1,2는 배열의 각각의 요소들의 순서번호(인덱스)로 사용될 수 있다.
for (i = 0; i < 3; i++) {
  // 위에서 일일이 순서번호를 써준 것과 다르게 i만 썼다.
  document.write(drinks[i].toUpperCase() + "<br /n>");
}

// coffee
// tea
// juice
```

이렇게 쓰고 결과를 보면 아까와 똑같은 결과를 볼 수 있다.

그렇다면 배열에 요소를 추가할 건데, 그 요소도 화면에 출력하고 싶다면 어떻게 해야 할까?

```javascript
function drinks() {
  return ["coffee", "tea", "juice", "wine"];
}

let anything = drinks();
for (i = 0; i < drinks.length; i++) {
  document.write(drinks[i].toUpperCase() + "<br /n>");
}
```

요소가 추가된 것과 상관없이, 반복되는 횟수를 배열의 길이로 지정했기 때문에 요소가 추가되어도, 기존에 있던 요소가 제거되어도 화면에 그대로 출력된다.

배열의 길이로 지정함으로써 요소들의 개수에 따라 결과는 탄력적으로 바뀐다.

## 3. 배열 기초 메소드

① Array.isArray();

자바스크립트의 특정 값이 배열인지 아닌지 판별할 수 있다.

ex)

```javascript
let number = [1, 2, 3, 4];

Array.isArray("문자열"); // false
Array.isArray(123); // false
Array.isArray({}); // false →{}는 object(객체)
Array.isArray(number); // true
Array.isArray([1, 2, 3, 4]); // true
Array.isArray([]); // true
```

직접 배열을 넣거나 배열의 이름을 넣으면 true, 배열이 아닌 타입을 넣으면 false로 나온다. 배열 안이 비었더라도 true로 나온다.

② 배열의 요소 추가, 삭제(제거)

- console.log 대신 console.table

```javascript
let arr = ["coffee", "tea"];
console.table(arr);
```

![](https://blog.kakaocdn.net/dn/zjQju/btribAprKiI/RhaCuVtF1SWrW6J67fH5lK/img.png)

‣ arr. push();

뒤쪽에 배열의 요소 추가

![](https://blog.kakaocdn.net/dn/cOwJJC/btrh4Nj1FkM/BCKRgvZUrpKqjH1jySKvV0/img.png)

‣ arr.pop();

뒤쪽에 배열의 요소 삭제(제거)

![](https://blog.kakaocdn.net/dn/smd1z/btribzRDFec/PILzUCjsS9wldFGjRlZfYK/img.png)

‣ arr.shift();배열의 앞쪽에 있는 요소 삭제(제거)하기

배열의 앞쪽에 있는 요소 삭제(제거)하기

![](https://blog.kakaocdn.net/dn/rCCAj/btriaVHolZg/bwEBT2DD4vRLx5z14OHpx0/img.png)

앞쪽에 있던 'coffee' 라는 요소가 사라지고 'tea'만 남았다.

‣ arr. unshift();배열의 앞쪽에 요소 추가하기

배열의 앞쪽에 요소 추가하기

![](https://blog.kakaocdn.net/dn/lSp4G/btrh7xA0cfE/4R06HWCGU6Ja94ArpGpGf0/img.png)

- arr.unshift('juice');를 쳤을 때 나오는 숫자 2는 앞으로 나올 배열의 length(길이).

③ 배열의 요소 포함 여부 확인하기

ex)

```javascript
let str = ["i", "love", "coffee"];

str.indexOf("love");
// ()안에는 내가 찾고자 하는 element의 값을 넣어준다.
// 1
// 1은 배열의 찾고자 하는 element가 들어있는 곳의 index.
```

그런데 만약 저 배열에 없는 단어를 indexOf에 넣어본다면 어떻게 될까?

```javascript
str.indexOf("tea");
// -1
```

그렇다면 이게 있는지 없는지 여부(존재)를 알아보고 싶다면 어떻게 쓸 수 있을까?

```javascript
str.indexOf("love") !== -1;
// true
```

즉, 이 단어가 -1과 같지 않다 라고 써주면 같지 않기 때문에 true를 출력한다.

\*indexOf는 대소문자를 구분하기 때문에 만약 정확하게 써주지 않는다면 -1을 출력한다.

⇒ 함수식으로 써보자.

```javascript
let str = ["i", "love", "coffee"];

function hasElement(arr, element) {
  let isPresenet = arr.indexOf(element) !== -1;
  return isPresent;
}

hasElement(str, "love");
// hasElement(배열, 찾으려는 요소)
// true or false를 출력한다.
// true
```

함수를 선언하고 isPresent라는 변수를 안에 선언하여 arr.indexOf(element)가 -1과 같지 않다면 isPresent를 리턴한다.

그렇게 hasElement(str, 'love'); 를 입력하면 str 배열 안에 'love'라는 요소가 있기 때문에 true로 출력된다.

이를 내장된 메소드로 쓰면

```javascript
str.includes("love");
// true

str.includes("tea");
// fales
```

있는 요소를 넣으면 true, 없는 요소를 넣으면 false가 나오는 것을 확인할 수 있다.

## 4. 객체(object)

배열이 순서번호(인덱스)를 숫자로 가져왔다면, 객체는 (숫자도 쓸 수 있지만)직접 원하는 데이터(문자 등)로 가져온다.

여러 속성을 하나의 변수에 저장할 수 있도록 해주는 데이터 타입으로 Key - Value Pair를 저장할 수 있는 구조

한 묶음의 데이터에 이름을 붙여줄 수 있다. 즉, 의미를 부여한다.

관련된 데이터와 함수의 집합

(일반적으로 여러 데이터와 함수로 이루어지는데, 객체 안에 있을 때는 property와 method라고 부른다)

- 프로퍼티: 객체의 속성을 나타내는 접근 가능한 이름과 활용 가능한 값을 가지는 특별한 형태이다.

특정 객체가 가지고 있는 정보를 품고 있어 그 객체가 가진 정보에 직접적으로 접근할 수 있게 해 준다.

\*메소드: 객체가 가지고 있는 동작이며 객체 내의 함수를 메소드라 칭한다.

✷ 메소드와 함수의 차이

메소드는 객체가 갖고 있는 동작이기 때문에 메소드를 수행하기 위해서는 객체를 통해서 해당 메소드를 수행해야 하며 그 동작을 수행하는 주체는 객체이다.

① 객체의 구조

⇒ 하나의 변수 안에 여러 가지 정보를 담을 때 적합한 자료 구조.

ex)

```javascript
// {}중괄호를 이용하여 객체를 만든다.
let user = {
  firstname: 이름, // key-value pair(키-값쌍)은 ,(쉼표)로 구분해준다.
  lastname: 성,
  email: 이메일주소,
  city: 도시이름,
  // 콜론을 기준으로 앞에는 키(key), 뒤는 값(value)
  // key와 value 사이는 :(콜론)으로 구분한다.
  //키와 값을 모두 합쳐 property(프로퍼티)라고 부른다.
  // 값에는 문자열이나 숫자열, 객체가 중첩되어 들어갈 수도 있음(모든 유형이 될 수 있다).
};
```

- 키는 문자열이거나 기호여야 한다. ⇒ 즉, user라는 이름을 사용하여 객체를 만들었다.

그 객체 안에는 'firstname', 'lastname', 'email', 'city'라는 인덱스가 들어가 있으며 그 인덱스의 값은 각각 '이름', '성', '이메일주소', '도시이름' 이 되겠다.

- 객체를 만드는 다른 방법

ex)

```javascript
let user = {};
// 빈 객체를 하나 할당해준다.
// let user = new Object;
// 이것은 {}중괄호와 같은 의미

user["firstname"] = "이름";
user["lastname"] = "성";
user["email"] = "이메일주소";
user["city"] = "도시이름";

console.log(user);
// {firstname: '이름', lastname: '성', email: '이메일주소', city: '도시이름'}
```

으로 나온다.

② 객체의 값을 사용하는 방법

‣ Dot notation

ex)

```javascript
let user = {
  firstname: 'Haley',
  lastname: 'Jeong',
  email: 'emailaddress@email.com'
  city: 'City'
  };

user.firstname;
// 'Haley'

user.city;
// 'City'

// 변수.찾고싶은속성; 로 써준다
// 중간에 dot(.) 중요함!!
```

‣ Bracket notation

ex)

```javascript
let user = {
  firstname: 'Haley',
  lastname: 'Jeong',
  email: 'emailaddress@email.com'
  city: 'City'
  };

user['firstname'];
// 'Haley'

user['city'];
// City

// 변수['찾고싶은속성']; 으로 써준다
// 변수 다음에 속성에는 꼭 [] 대괄호 표시해주기
// 속성에는 '' 표시해주기
```

✷ 주의점

braket notation을 쓸 때 변수['찾고싶은속성']과 변수[찾고싶은속성] 으로 쓰는 것은 매우 많이 다르다!

즉, 원래 써주었던 '문자열' 형태로 쓰는 것과 그냥 변수 이름 쓰듯이 쓰는 것은 다르다는 것이다.

ex)

user['firstname']과 user[firstname]은 다르다는 것.

user[firstname]으로 썼다면 console창에 Uncaught ReferenceError: firstname is not defined.

라고 나올 것이다. 참조되지 않았다, firstname은 정의되지 않았다.

여기서 쓰는 firstname은 firstname이라는 정의되지 않은 변수를 참조한다고 말하기 때문에, firstname이 정의되지 않았다고 나온다.

그렇다면 여기서 ''를 쓰지 않고도 원하는 값을 나오게 싶다면 어떻게 할 수 있을까?

```javascript
// user[name] === user['firstname']이 되는 방법

// 변수를 선언하고 문자열로 할당한다.
let name = "firstname";
user[name]; // 'Haley'
```

✷ Bracket notation과 Dot notation의 차이점

- Bracket notation은 key값이 동적으로 변할 때, 즉 변수일 때 써준다.

- Dot notation은 정해진 key값이 있을 때만 사용할 수 있다.

✅변수는 값을 할당하지 않고 선언만 할 경우 자동적으로 undefined를 할당한다.

하지만 객체의 정보를 담고 있어야 할 요소가 그 어떤 정보도 할당받지 않았다면 객체로서는 필요가 없기 때문에 프로퍼티를 추가하면서 값을 할당하지 않으면 syntax error가 뜬다.

③delete키워드를 사용하여 삭제하는 방법

\*프로퍼티는 undefined나 null을 할당한다고 삭제되지 않기 때문에 반드시 delete라는 keyword를 사용하여 프로퍼티를 삭제해주어야 한다.

ex)

```javascript
let user = {
  firstname: 'Haley',
  lastname: 'Jeong',
  email: 'emailaddress@email.com'
  city: 'City'
  };

// user라는 변수 안에 있는 city키-값 쌍을 지운다(delete 변수.지우고싶은 키-값 쌍)
delete user.city;

let user = {
  firstname: 'Haley',
  lastname: 'Jeong',
  email: 'emailaddress@email.com'
  };
```

✅ 객체는 배열처럼 길이를 잴 수 있을까?

정확하게 말하자면 객체는 배열처럼 .length만 사용해서 길이를 잴 수 없지만, 객체의 속성을 이용한 길이는 잴 수 있다.

Object.keys().length를 사용하면 객체의 길이를 잴 수 있다.(정확하게는 객체 자체의 길이는 아니지만)

()안에다가 객체를 넣어주면 Object.keys()를 했을 때 해당 객체의 key값이 배열에 담겨서 리턴된다.

✷ [Object.keys()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

전달된 객체에서 직접 찾은 열거할 수 있는 속성 이름에 해당하는 문자열 배열을 반환한다.

✷ [Object.assign()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

[객체를 병합하는 메소드.](https://pro-self-studier.tistory.com/21)

## 5. in 연산자

해당하는 키 값이 있는지 없는지 확인할 수 있다.

ex)

```javascript
let user = {
  firstname: 'Haley',
  lastname: 'Jeong',
  email: 'emailaddress@email.com'
  city: 'City'
  };

// true(value가 변수 안에 있는가가 true, 즉 있다라고 나온다)
'city' in user;

// false(value가 변수 안에 있는가가 false, 즉 없다라고 나온다)
'content' in user;
```

✷ 배열과 객체의 가장 큰 차이점은 순서의 유무이다.

배열은 요소에 0부터 순차적으로 접근할 수 있지만 객체는 속성에 순서대로 접근하지 않고, key를 통해서 value에 접근한다.

⇒ key에 문자열이나 기호(symbol) 이외의 값을 지정하면 암묵적으로 타입이 변환되어 문자열이 되며 이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.

배열과는 달리 객체는 프로퍼티를 열거할 때 순서를 보장하지 않는다.

## 6. for in과 for of

통상적으로 for in은 객체에서, for of는 배열에서 쓰인다.

① for in 구문을 통해서 객체의 모든 key에 순차적으로 접근하고 출력할 수 있다.

객체를 반복시킬 수 있는 반복문. 인덱스 값 혹은 키값을 출력한다.

```javascript
let object = { a: 1, b: 2, c: 3 };

for (let key in object) {
  console.log(key);
}
// for in문을 작성
// object 안에 key가 있을 때 반복한다
// 콘솔 결과 출력은 key

// a
// b
// c
```

```javascript
let object = { a: 1, b: 2, c: 3 };

for (let key in object) {
  console.log(object[key]);
}
// for in문 작성
// object 안에 key가 있을 때 반복한다
// 콘솔 결과 출력은 object안의 key의 value

// 1
// 2
// 3
```

객체 {a: 1, b: 2, c: 3} 안에서 key는 a, b, c. 그 key의 value는 1, 2, 3.

둘 다 똑같이 반복조건은 object안의 key만큼이었지만, 콘솔 출력 결과를 key로 뒀느냐 key의 value로 두느냐에 따라 리턴값이 달라졌다.

② for of는 string과 array, 유사배열 등에서 사용이 가능한 반복문이고, 객체에서는 사용되지 않는다.

배열 안에 있는 요소를 출력한다.

for (let arr[i] of arr)가 for (let i = 0; i < arr.length; i += 1) 과 같다고 생각하면 쉽다.

즉, arr안의 arri[i](요소)를 output한다고 생각하면 된다.

```javascript
let array = [1, 3, 4];

// for(i = 0; i < array.length; i++)과 같은 의미
for (let el of array) {
  // 배열의 요소인 el을 순서대로 꺼내온다
  console.log(el);
}

// 1
// 3
// 4
```

```javascript
let array = [1, 3, 4];

// array안에 있는 el이라는 키의 값을 반복한다
for (let el in array) {
  // array안에 있는 el라는 키의 값을 꺼내온다
  console.log(array[el]);
}

// 1
// 3
// 4
```

array라는 변수를 선언하고 똑같은 값을 할당했을 때, 배열의 요소, 객체의 요소의 값을 출력하는 방법을 달리하여 코드를 작성해보았다.

어쨌든 두 개의 코드는 결론적으로 같은 의미로 사용된 것이지만, for of문과 for in문을 사용했을 때 다르게 쓰는 것을 직접 작성했다.

✷ 명시적 return문이 없을 경우 undefined를 반환한다. 따라서 모든 함수는 값을 반환한다. return문을 사용하지 않더라도 리턴값을 전달하게 되어있다.

✷o bject.entries(obj): 문자열의 키를 가진 속성을 반환한다.

⇒ object.entries() 는 object 에서 직접 찾은 열거 가능한 문자열 키 속성 [key, value] 쌍에 해당하는 배열 요소가있는 배열을 반환한다. 속성의 순서는 객체의 속성 값을 수동으로 반복하여 지정하는 것과 동일하다.

✷ 속성 개수 구하기

```javascript
const count = object.keys(obj).length;
```

예시를 하나 들어보자.

```javascript
const obj = {
  firstName: "Emily",
  lastName: "Johnson",
  sequencenumber: 12,
};
```

라는 객체를 하나 선언했을 때

객체(object)가 가지고 있는 속성의 개수를 구하고 싶을 때 사용하는 함수가 바로 <mark>object.keys();</mark>함수다.
object.keys() 함수는 <mark>파라미터로 입력받은 객체의 key 목록을 배열로 리턴</mark>한다.

object.keys(obj)는 "['firstName', 'lastName', 'sequencenumber']"를 리턴하게 된다.
그 다음 배열의 길이를 length 속성을 사용하면 그 값이 객체의 속성 개수가 된다.
