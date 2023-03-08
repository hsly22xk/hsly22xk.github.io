---
layout: single
title: "D+23 고차함수"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

고차함수에 관련한 전반적인 내용 정리.

## 1. 일급 객체(first-class citizen)

‣ 대표적인 예시: 함수

✷ 변수에 할당을 할 수 있기 때문에 함수를 배열의 요소나 객체의 속성값으로 저장할 수 있다.

⇒ 함수를 데이터(string, number, boolean, array, object)를 다루듯이 다룰 수 있다.

✷ 다른 함수의 인자로 전달될 수 있다

✷ 다른 함수의 결과로 리턴될 수 있다

## 2. 고차함수(higher✷order function)

함수를 인자로 전달받거나 함수를 결과로 반환하는 함수로, 변수에 할당하지 않고 함수를 바로 이용할 수 있다.

어떤 고차 함수에 함수를 인자로 전달하고, 고차 함수는 함수 자체를 리턴한다.

원래 알던 개념에서 변수가 빠졌을 뿐, 동작은 동일하게 함.

고차함수는 인자로 받은 함수를 필요한 시점에 호출하거나 클로저를 생성하여 반환한다.

ex)

```js
// 함수를 인자로 전달받고 함수를 반환하는 고차 함수
function makeCounter(predicate) {

// 자유 변수. num의 상태는 유지되어야 한다.
let num = 0;

// 클로저. num의 상태를 유지한다.
return function () {

// predicate는 자유 변수 num의 상태를 변화시킨다.
num = predicate(num);
return num;
};
}

// 보조 함수
function increase(n) {
return ++n;
}

// 보조 함수
function decrease(n) {
return ✷✷n;
}

// makeCounter는 함수를 인수로 전달받고 클로저를 반환한다.
const increaser = makeCounter(increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// makeCounter는 함수를 인수로 전달받고 클로저를 반환한다.
const decreaser = makeCounter(decrease);
console.log(decreaser()); // ✷1
console.log(decreaser()); // ✷2
```

① 콜백 함수(callback function)

다른 함수(caller)의 인자(argument)로 전달되는 함수로, 함수에 파라미터로 들어가는 함수를 콜백 함수라고 부른다.

‣ 용도: js에서 뭔가 순차적으로 코드를 실행하고 싶을 때 사용함.

콜백 함수를 전달받은 고차함수는 특정한 타이밍(이벤트)에서 함수 내부에서 콜백 함수를 호출할 수 있다.

caller는 조건에 따라 콜백 함수의 실행 여부를 결정할 수 있다. 아예 호출하지 않을 수도, 여러 번 실행할 수도 있다.

// 이벤트가 정의되어 있지 않을 때 콜백은 현재 실행 흐름이 완료된 후에 호출되어 후처리를 담당한다.

```html
<script>
    document.querySelector('.button').addEventListener('click', function() {
    <✷✷ 함수 안에 실행할 코드 입력 ✷✷>
  })
</script>
```

⇒ addEventListener는 함수

⇒ 그 함수의 파라미터 자리에 'click' 다음에 써놓은 function()함수가 콜백 함수

⇒ 이제 버튼을 클릭했을 때 함수 안에 적어둔 코드가 실행됨

✷ 다른 데서 만든 함수도 콜백 함수로 집어넣을 수 있고, 콜백 함수의 함수 이름을 작명할 수도 있다.

다만 콜백 함수는 아무데서나 다 쓰는 게 아닌 콜백 함수가 필요한 곳에서만 사용 가능하다.

② 커링 함수(curring function)

단일 호출로 처리하는 함수를 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합되도록 변환하는 것(고차 함수 안에 커링 함수가 있는 것)

## 3. 내장 고차 함수

✅ 배열 조작 메소드

① array.forEach()

원래는 변수를 선언하여 반복문의 형태를 써주었지만 이제는 forEach()메소드를 사용한다.

가장 기본적인 형태의 반복문으로, 단순 반복을 하고 return값을 따로 가지지 않는다. 그냥 반복하면서 요소(값)을 리턴한다. 반복문의 기능 외에는 아무것도 없다.

```js
// 문자열을 사용하여 forEach()를 사용하는 예시

let drink = ["coffee", "tea", "juice", "wine", "cocktail"];
let all = function (drink) {
  console.log(drink);
};
drink.forEach(all);
// coffee
// tea
// juice
// wine
// cocktail
// 배열의 요소가 숫자일 때 숫자만 전부 반복하여 요소를 리턴한 예시

let arr = [1, 2, 3, 4, 5];
arr.forEach((el) => console.log(el));
// 1
// 2
// 3
// 4
// 5
// 배열의 요소의 인덱스 넘버(순서번호)를 콘솔창에 출력한 예시

let arr = [1, 2, 3, 4, 5];
arr.forEach(function (arr, index) {
  console.log(index);
});

// 0
// 1
// 2
// 3
// 4
```

② array.filter()

모든 배열의 요소 중에서 특정 조건을 만족하는 요소를 걸러내는 메소드로, 조건에 맞는 데이터만 분류할 때 사용. 특정 조건을 만족하는 새로운 배열을 필요로 할 때 사용.

‣ 특정 조건의 예시

number 타입을 요소로 갖는 배열에서 짝수만을 걸러내거나, 특정 숫자 보다 작거나 큰 수만을 걸러낸다.

string 타입을 요소로 갖는 배열에서 길이가 10 이하인 문자열만 걸러내거나, 특정 문자열만 걸러낸다.

✷ map, filter, reduce와 같은 함수는 기본적으로 순차적으로 값에 접근한다라는 개념을 내포하고 있다.
→ 여기서 걸러내는 기준이 되는 특정 조건은 filter 메소드의 인자로 전달된다. 전달되는 조건은 함수의 형태.

filter 메소드는 걸러내기 위한 조건을 명시한 함수를 인자로 받기 때문에 고차함수이다.

→ 배열의 요소를 인자로 전달되는 콜백 함수에 다시 전달한다.

콜백 함수는 전달받은 배열의 요소를 받아 함수를 실행하고, 콜백 함수 내부의 조건에 따라 참(true) 또는 거짓(false)을 리턴해야 한다. 적어도 filter 메소드는 이런 함수를 기대하고 있다.

```js
// 배열의 요소가 숫자일 때의 예시

// 걸러낼 조건을 변수로 하나 선언한 후 함수를 할당한다
let isEven = function (num) {
  return num % 2 === 0;
};

let arr = [1, 2, 3, 4, 5];
// 소괄호 안에 선언해준 변수의 이름을 쓴다
let output = arr.filter(isEven);
console.log(output);

// (2) [2, 4]
// 배열의 요소가 문자열일 때 예시

let isMoreThan5Length = function (str) {
  return str.length >= 5;
};

let arr = ["coffee", "tea", "juice", "wine", "cocktail"];
let output = arr.filter(isMoreThan5Length);
console.log(output);

// (4) ['coffee', 'juice', 'cocktail']
```

이번에는 배열의 요소가 객체일 때다.

```js
// 배열의 요소가 객체일 때의 예시

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let female = profile.filter(function (profile) {
  return profile.gender === "female";
});

console.log(female);
// (3) [{...}, {...}, {...}]
// ‣ 0: { name: 'Haley', age: 21, gender: 'female' }
// ‣ 1: { name: 'Emily', age: 25, gender: 'female' }
// ‣ 2: { name: 'Abigail', age: 19, gender: 'female' }
```

이렇게 사람들의 프로필이 있다고 했을 때, 성별이 여자인 사람들만 걸러내고 싶다면 배열에서 변수를 하나 지정해서 filter함수를 할당해준다.

return값은 배열에서의 요소인 객체 중, 키(gender)의 값이 'female'을 갖고 있는 요소 그 자체들만 걸러낸다.

console.log(female); 을 해보면 객체 요소들 중 gender의 값이 'female'인 요소들만 걸러져 나왔다.

이름이나 나이는 기준이 정해져 있지 않기 때문에 filter로 거를 수는 없지만, 성별은 여자 혹은 남자로만 지정이 되기 때문에 제대로 된 기준을 잡아 filter로 걸러낼 수 있다.

물론, 'gender'의 값 자체만 배열의 요소로 걸러내고 싶을 때는 바로 아래에 나올 map()함수를 사용하면 된다.

③ array.map()

기존 배열을 변형하여 새로운 배열로 생성한다. 배열의 각 요소가 특정 함수(논리)에 의해 다른 요소로 지정된다. // 지정 === map

여기서 특정 함수란, 배열의 각 요소들을 어떠한 결과값으로 내기 위한 '행동' 쯤으로 이해하면 좋겠다. 특정 함수는 내가 직접 작성해야 하며 그 함수를 인자로 넣어준다.

가장 간단한 예시를 들자면 다음과 같다.

```js
let arr = [1, 2, 3, 4, 5];

let result = arr.map(fucntion(ele) {
return ele + 2;
});

console.log(result);
// (5) [3, 4, 5, 6, 7]
```

하나의 데이터를 다른 데이터로 맵핑(mapping) 할 때 사용한다.

```js
let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let profileNames = profile.map(function (profile) {
  return profile.name;
});
console.log(profileNames);
// (7) ['Haley', 'Emily', 'Harvey', 'Alex', 'Abigail', 'Sam', 'Sebastian']

let profileGenders = profile.map(function (profile) {
  return profile.gender;
});
console.log(profileGenders);
// (7) ['female', 'female', 'male', 'male', 'female', 'male', 'male']

let profileAges = profile.map(function (profile) {
  return profile.age;
});
console.log(profileAges);
// (7) [21, 25, 29, 21, 19, 20, 20]
```

profile이라는 이름의 배열 안에 요소는 객체이다. 객체의 속성은 name과 age, gender, 그리고 그에 해당하는 값들이다.

여기서 name이나 gender, 혹은 age의 값만 배열의 요소로 주고 싶다면 map을 사용할 수 있다.

이와 비슷하게 예시를 하나 더 들어본다.

웹툰 '바리공주'의 171회차까지의 회차모음의 정보가 객체에 들어있고, 각 회차의 부제만을 담은 배열을 리턴하는 조건을 작성했다.

일단 수도 코드를 작성하면

```js
// 배열의 각 요소: 171회차 까지의 회차 모음 정보
// 특정 논리: 그 회차의 부제만 배열의 요소로 담는다.
// 다른 요소: 각 회차의 부제

let princessBari = [
{
id: 1,
bookType: 'cartoon',
title: '바리공주',
subtitle: '미영귀1',
createAt: '2017✷12✷15',
genre: '판타지 드라마',
artist: '김나임',
},
{
id: 2,
<✷✷이하 생략✷✷>
}
]

let findSubtitle = function(cartoon) {
return cartoon.subtitle; // 웹툰의 부제를 리턴하는 함수
}

let subtitles = cartoon.map(findSubtitle);
```

이런 식으로 map()메소드를 사용하면 1회부터 171회차 까지의 부제들만 배열의 요소로 담을 수 있다.

✷ map과 filter를 섞은 예시

① profile이라는 배열의 요소는 객체이다.

객체의 속성이 있을 때 이 중 age의 값이 20인 요소만 배열의 요소로 갖는다.

```js
let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let allAges = profile.map(function (profile) {
  return profile.age;
});
console.log(allAges);
// (7) [21, 25, 29, 21, 19, 20, 20]

let ageIs20 = allAges.filter(function (allAges) {
  return allAges === 20;
});
console.log(ageIs20);
// (2) [20, 20]
```

② ①번과 같은 배열로 문제를 푼다고 하자.

성별이 여자인 사람의 이름만 리턴한다.

```js
let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let female = profile.filter(function (profile) {
  return profile.gender === "female";
});

let allNames = female.map(function (female) {
  return female.name;
});

console.log(allNames);
// (3) ['Haley', 'Emily', 'Abigail']
```

④ array.reduce()

기본 구문 // array.reduce(요소의 순서를 결정하는데 사용할 함수 이름)

배열의 각 요소를 특정 함수(방법)에 따라 원하는 하나의 형태로 합친다(reduce).

<mark>초기값을 정할 수 있으나 정하지 않았을 때에는 배열의 첫번째 요소가 초기값이 된다.</mark> 이 초기값은 누적값의 기본이 된다.

```js
let arr = [1, 2, 3];

let total = arr.reduce(fucntion(acc, cur) {
console.log(acc, cur);
return acc + cur;
});
console.log(total);

// 1 2
// 3 3
// 6
```

arr라는 배열의 요소가 1, 2, 3일 때 어떤 방식으로 reduce가 되어 최종적인 값이 6이 나오는 지 써보았다.

```js
let arr = [1, 2, 3];
let result = (acc, cur) => acc + cur;

console.log(acc.reduce(result));
// 6
```

위의 예시처럼 return을 사용하지 않고 화살표 함수를 사용하여 짧게 쓴 것이다. 결국 위의 예시와 지금의 예시는 같은 것.

이번에는 배열의 요소가 객체인, 문자열의 값을 리턴하는 예시다.

```js
function joinName(resultStr, profile) {
  resultStr = resultStr + profile.name + ", ";
  return resultStr;
}

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

profile.reduce(joinName, "");
// 'Haley, Emily, Harvey, Alex, Abigail, Sam, Sebastian, '
function joinGender(resultStr, profile) {
  resultStr = resultStr + profile.gender + ", ";
  return resultStr;
}

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

profile.reduce(joinGender, "");
// 'female, female, male, male, female, male, male, '
```

✷ map과 reduce의 차이

map() 객체의 요소의 값을 배열의 형식으로, 문자열을 하나하나를 배열의 요소로 리턴했다면 reduce() 객체의 요소의 값을 문자열의 형식으로, 객체의 값을 한 문자열에 전부 넣어주었다는 것이 다르다.

```js
let arr = [1, 2, 3, 4, 5];

arr.reduce((acc, cur, idx) => {
  return acc + `${idx}번째 인덱스는 ${cur}이다. `;
}, "");
// '0번째 인덱스는 1이다. 1번째 인덱스는 2이다. 2번째 인덱스는 3이다. 3번째 인덱스는 4이다. 4번째 인덱스는 5이다.'
```

이렇게 idx라는 인자를 넣어주어 순서번호(idx)를 넣어주며 하나의 문자열로 만들 수도 있다.

✷ 초기값을 직접 넣어줌과 넣어주지 않음의 차이에 대한 예시

```js
// 초기값을 넣지 않은 예시

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let totalAges = profile.reduce(function (acc, cur) {
  return acc + cur.age;
});

console.log(totalAges);
// [object Object]252921192020
```

```js
// 초기값을 넣은 예시

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let totalAges = profile.reduce(function (acc, cur) {
  return acc + cur.age;
}, 0);

console.log(totalAges);
// 155
```

프로필의 배열의 요소는 객체이다. 그 객체의 속성 중 age의 값의 합을 구하려 reduce를 쓴 예시이다.

그런데 위와 아래가 좀 다르다. 똑같이 reduce를 해서 합을 구하고 싶었는데, 위는 답이 나오긴 나오는데 뭔가 좀 이상한 형태로 나오고, 아래는 정상적으로 155라는 합이 나왔다.

여기서 초기값을 주지 않음과 초기값을 0으로 설정한 것의 차이가 드러난다.

첫번째는 초기값을 주지 않았다. 그 말은, 초기값이 첫번째 요소가 된다는 말인데, 이 배열에서의 첫번째 요소는 객체이다.그래서 첫번째 요소인 객체 자체에서 age의 값을 하나 하나 더한 것이다.

두번째는 초기값을 0으로 지정해주었다.

초기값을 0으로 지정해주었기 때문에 0부터 age의 속성값을 하나 하나 누적해서 더해주었다.

즉, 0 + 21 + 25 + .... 20까지 더해준 값이 155가 나오는 것이 맞기 때문에 내가 원하는 age의 값을 모두 더한 값이 나온다.

이것은 문자열의 값을 reduce할 때도 같다.

```js
// 초기값을 넣지 않은 예시

let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

profile.reduce((acc, cur, idx) => {
  return acc + `${idx}번째는 ${cur.name}이다. `;
});
// '[object Object]1번째는 Emily이다. 2번째는 Harvey이다. 3번째는 Alex이다. 4번째는 Abigail이다. 5번째는 Sam이다. 6번째는 Sebastian이다.'
```

```js
// 초기값을 빈 문자열로 넣은 예시

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

profile.reduce((acc, cur, idx) => {
return acc + `${idx}번째는 ${cur.name}이다. `
}, '');
// '0번째는 Haley이다. 1번째는 Emily이다. 2번째는 Harvey이다. 3번째는 Alex이다. 4번째는 Abigail이다. 5번째는 Sam이다. 6번째는 Sebastian이다.'
첫번째는 역시 초기값을 지정해주지 않아 초기값은 객체가 되었다.

원하는 대로 문자열이 리턴되지 않는다.

두번째는 초기값을 ''빈 문자열로 지정해주었다. ''빈 문자열부터 차례대로 문자열이 더해진다.

원하는 대로 문자열이 출력된다.

⑤array.find()

: 단 하나의 결과값만 출력하며 원하는 결과값이 나오는 즉시 반복문을 종료함.

즉, 주어진 판별 함수를 만족하는 첫 번째 요소의 값을 반환

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

let findName = profile.find(function(profile) {
return profile.name === 'Harvey';
});

console.log(findName);
// { name: 'Harvey', age: 29, gender: 'male' }
```

예시에서는 배열의 요소로 객체를 들었지만, 찾고자 하는 값만 정확하다면 배열 안에서의 문자열도 되고, 숫자도 가능하다.

```js
let profile = [
  { name: "Haley", age: 21, gender: "female" },
  { name: "Emily", age: 25, gender: "female" },
  { name: "Harvey", age: 29, gender: "male" },
  { name: "Alex", age: 21, gender: "male" },
  { name: "Abigail", age: 19, gender: "female" },
  { name: "Sam", age: 20, gender: "male" },
  { name: "Sebastian", age: 20, gender: "male" },
];

let findAge = profile.find(function (profile) {
  return profile.age === 20;
});

console.log(findAge);
// { name: 'Sam', age: 20, gender: 'male' }
```

✷ 그런데 왜 age의 값이 20을 갖는 객체는 2개인데, 왜 1개만 나오는가?

제일 처음에도 써놓았지만, 판별 함수에 만족하는 제일 첫 번째 요소를 반환해주는 것이 find이다. age의 속성값이 20인 객체 중에 제일 처음으로 나오는 것으로 반환해준 것이다.

⑥array.sort() // 정렬 메소드

정렬할 Array의 요소의 개수가 2개 미만일 경우 ‘sort is not a function’ 오류가 난다.

array.sort()는 원래 배열을 바꾼다. 만약 원래 배열을 수정하지 않으려면 arr.slice()로 복사를 해두고 sort를 사용한다.

```js
let arr = [12, 4, 6, 7, 3, 236, 731];

arr.sort();
// (7) [12, 236, 3, 4, 6, 7, 731];

arr.sort(function(a, b) {
// 오름차순
return a ✷ b;
});
// (7) [3, 4, 6, 7, 12, 236, 731]

arr.sort(function(a, b) {
// 내림차순
return b ✷ a;
});
// (7) [731, 236, 12, 7, 6, 4, 3]
```

제일 처음 쓴 arr.sort();는 정렬이 되기는 했지만 제대로 정렬이 되지 않았다. 만약 오름차순과 내림차순으로 정렬을 하기 위해서는 아래에 써준 것처럼 써주어야 한다.

문자열도 정리할 수 있다.

```js
// 이름 오름차순

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

profile.sort(function(a, b) {
return a.name < b.name ? ✷1 : a. name > b.name ? 1 : 0;
});
// (7) [{...}, {...}, {...}, {...}, {...}, {...}, {...}]
// ‣ (0): { name: 'Abigail', age: 19, gender: 'female' }
// ‣ (1): { name: 'Alex', age: 21, gender: 'male' }
// ‣ (2): { name: 'Emily', age: 25, gender: 'female' }
// ‣ (3): { name: 'Haley', age: 21, gender: 'female' }
// ‣ (4): { name: 'Harvey', age: 29, gender: 'male' }
// ‣ (5): { name: 'Sam', age: 20, gender: 'male' }
// ‣ (6): { name: 'Sebastian', age: 20, gender: 'male' }
```

```js
// 이름 내림차순

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

profile.sort(function(a, b) {
return a.name > b.name ? ✷1 : a.name < b.name ? 1 : 0;
});
// (7) [{...}, {...}, {...}, {...}, {...}, {...}, {...}]
// ‣ (0): { name: 'Sebastian', age: 20, gender: 'male' }
// ‣ (1): { name: 'Sam', age: 20, gender: 'male' }
// ‣ (2): { name: 'Harvey', age: 29, gender: 'male' }
// ‣ (3): { name: 'Haley', age: 21, gender: 'female' }
// ‣ (4): { name: 'Emily', age: 25, gender: 'female' }
// ‣ (5): { name: 'Alex', age: 21, gender: 'male' }
// ‣ (6): { name: 'Abigail', age: 19, gender: 'female' }
```

이름을 기준으로 오름차순과 내림차순으로 정리해보았다. 나이까지는 정렬되지 않았다.

이번엔 나이 순으로 정렬한 예시다.

```js
// 나이 오름차순

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

let sortingField = 'age';
profile.sort(function(a, b) {
return a[sortingField] ✷ b[sortingField];
});

// (7) [{...}, {...}, {...}, {...}, {...}, {...}, {...}]
// ‣ (0): { name: 'Abigail', age: 19, gender: 'female' }
// ‣ (1): { name: 'Sam', age: 20, gender: 'male' }
// ‣ (2): { name: 'Sebastian', age: 20, gender: 'male' }
// ‣ (3): { name: 'Haley', age: 21, gender: 'female' }
// ‣ (4): { name: 'Alex', age: 21, gender: 'male' }
// ‣ (5): { name: 'Emily', age: 25, gender: 'female' }
// ‣ (6): { name: 'Harvey', age: 29, gender: 'male' }
```

```js
// 나이 내림차순

let profile = [
{ name: 'Haley', age: 21, gender: 'female' },
{ name: 'Emily', age: 25, gender: 'female' },
{ name: 'Harvey', age: 29, gender: 'male' },
{ name: 'Alex', age: 21, gender: 'male' },
{ name: 'Abigail', age: 19, gender: 'female' },
{ name: 'Sam', age: 20, gender: 'male' },
{ name: 'Sebastian', age: 20, gender: 'male' }
]

let sortingField = 'age';
profile.sort(function(a, b) {
return b[sortingField] ✷ a[sortingField];
});

// (7) [{...}, {...}, {...}, {...}, {...}, {...}, {...}]
// ‣ (0): { name: 'Harvey', age: 29, gender: 'male' }
// ‣ (1): { name: 'Emily', age: 25, gender: 'female' }
// ‣ (2): { name: 'Haley', age: 21, gender: 'female' }
// ‣ (3): { name: 'Alex', age: 21, gender: 'male' }
// ‣ (4): { name: 'Sam', age: 20, gender: 'male' }
// ‣ (5): { name: 'Sebastian', age: 20, gender: 'male' }
// ‣ (6): { name: 'Abigail', age: 19, gender: 'female' }
```

⑦array.every() & array.some()

‣ every: 배열 안의 모든 데이터가 조건을 만족하는 경우 true. else는 false

‣ some: 배열 안의 데이터 중 하나라도 조건을 만족하면 true. else는 false

```js
let macs = [
{name: 'macbookAir', ram: 16},
{name: 'macbookPro', ram: 32},
{name: 'macbookMax', ram: 64},
{name: 'newMacbook, ram: 8},
]

let everyMacsAvailable = macs.every(function(macs) {
return macs.ram > 16;
});
console.log(everyMacsAvailable);
// false

let someMacsAvailable = macs.some(function(macs) {
return macs.ram < 16;
});
console.log(someMacsAvailable);
// true
```

같은 조건에서 every()메소드는 모두 만족하는 조건이 아니기 때문에 false를 반환하고,

some은 하나라도 만족하는 조건이 있기 때문에 true를 반환한다.

## 4. 추상화

복잡한 어떤 것을 압축해서 핵심만 추출한 상태로 만드는 것

예를 들어, 개발자 도구 콘솔에 어떤 코드를 입력한다고 가정하자.

```js
function sum(a, b) {
  return a + b;
}
let result = sum(1, 2);
console.log(sum);
// 3
```

컴퓨터가 어떤 과정을 거쳐 3을 내주는지는 모르지만 어쨌든 3을 출력하여 우리는 3이라는 답을 얻어냈다.

이처럼 자바스크립의 문법(syntax)을 올바르게 사용하는 것만으로 다양한 프로그램을 (자바스크립트가 없었을 때) 보다 쉽게 작성할 수 있다.

고민거리는 줄어들고, 문제의 해결이 더 쉬워지는 것이 추상화의 이점이다. 그래서 추상화 = 생산성의 향상이다. 추상화의 관점에서 함수는 사고 / 논리의 묶음이다.

```js
function getAverage(data) {
  let sum = 0;
  for (let i = 0; i < data.length; i++) {
    sum = sum + data[i];
  }
  return sum / data.length;
}

let output = getAverage([1, 2, 3]);
console.log(output);
// 2

output = getAverage([4, 2, 3, 6, 5, 4]);
console.log(output);
// 4
```

이 코드를 봤을 때, 우리는 함수가 배열을 전달받아 이 배열의 평균값을 내줌을 알 수 있다.

즉 함수는 값(배열)을 전달받아, 이 값을 가지고 복잡한 작업(평균값을 내줌)을 수행한다. 이는 값 수준에서의 추상화이다.

그러니까, 단순히 값만 전달 받아 처리하는 수준이라는 거다.

고차함수는 이런 값 수준의 추상화를 사고 수준의 추상화로 끌어올릴 수 있다. 값 수준에서의 추상화가 단순히 값만 전달받았다면, 사고 수준의 추상화는 함수를 전달받아 처리한다는 것이다.

즉, **<mark>고차함수 = 함수를 전달 받는다 / 함수를 리턴한다 = 함수(사고)에 대한 복잡한 논리(로직)은 감춰져 있다 = 사고 수준에서의 초상화다.</mark>**
