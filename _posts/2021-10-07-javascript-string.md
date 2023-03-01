---
layout: single
title: "D+3 문자열(typeof String)"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

자바스크립트의 문자열.

## 1. 문자열

문자열(String), 일상생활에서 모든 글자의 나열을 문자열이라고 한다.

ex)

```javascript
"Hello", "Hello World", "사과";
```

코드와 문자열을 구분하기 위하여 ''(작은 따옴표) / ""(큰 따옴표)를 사용한다.

‣ 문자열 구분은 자동완성 기능처럼 문자열을 직접 사용하는 소프트웨어를 만드는 일에도 사용할 수 있고, 날짜를 나타내는 숫자를 문자열로 변경해 01과 같이 나타낼 수도 있다.

‣ 문자열은 String, 문자는 Charactor, 줄여서 char라고 표현할 수 있다. char가 포함된 메소드도 있다.

‣ str[index]

ex)

```javascript
var str 'Apple'
console.log(str[0]); // 'A'
console.log(str[4]); // 'e'
console.log(str[10]); // undefined
```

0이 첫 번째 글자이다. → index로 접근은 가능하지만 사용하지는 못한다(새로 할당하지 않는 한 read-only, 값이 바뀌지 않는다)

예를 들어 주어진 문자열의 특정 문자를 바꾸고 싶을 때,

```javascript
str[0] = "O";
console.log(str); // 'Apple' not 'Opple'
```

실제로 바뀌지 않는다는 것을 알 수 있다.

-, + 연산자를 쓸 수 있음.

ex)

```javascript
var str1 = "Favorite";
var str2 = "Fruit";
var str3 = "1";
console.log(str1 + str2); // 'FavoriteFruit'
console.log(str3 + 7); // '17'
```

‣ 띄어쓰기가 자동으로 되는 것은 아님.

→ 문자열 '1' 과 숫자열 7이 합쳐지면 문자열 '17'이 나옴.

→ str1.concat(str2, str3, ... );의 형태로도 나옴.

‣ length property: 문자열의 전체 길이 반환

```javascript
var str = "Codestates";
console.log(str.length); // 10
```

- str.indexOf (searchValue)

: 문자열에서 특정 문자열을 찾고 검색된 문자열이 첫번째로 나타나는 위치 index를 리턴

⇒ 찾을 문자열이 없으면 -1 리턴하며 찾을 때는 대소문자를 구분한다.

⇒ str.indexOf(searchValue)

⇒ str.indexOf(searchvalue, position)

// position은 optional, 기본값은 0. 문자열에서 searchvalue를 찾기 시작할 위치.

ex)

```javascript
// 0 ←'Red'는 0번째 index부터 떨어지기 때문에 값이 0이 나옴
"Red Apple".indexOf("Red");

// 5
// ←'Apple'은 띄어쓰기 포함 5번째 index부터 떨어지기 때문에 값이 5가 나옴
"Red Apple".indexOf("Apple");

// -1
// ←'red'라는 문자열은 없기 때문에 -1로 나옴
"Red Apple".indexOf("red");

// 5
// ←처음 나온 index인 Apple을 기준으로 삼기 때문에 뒤에 같은 문자열이 반복되어도 첫 번째 것으로 나옴
"Red Apple Apple".indexOf("Apple");

// 2
// ←lastIndexOf는 뒤에서부터 세기 때문에 더 앞에 p가 있지만 뒤에 있는 두 번째 index p의 값이 나옴
"Apple".lastIndexOf("p");
```

ex) searchvalue만 입력한 경우

```javascript
const str = "abab";

document.writeln(str.indexOf("ab")); // 0
document.writeln(str.indexOf("ba")); // 1
document.writeln(str.indexOf("abc")); // -1
document.writeln(str.indexOf("AB")); // -1
```

```
1. 문자열 'abab'에서 'ab'가 처음으로 나타나는 위치의 인덱스 값을 리턴하기 때문에 0.
2. 문자열 'abab'에서 'ba'가 처음으로 나타나는 위치의 인덱스 값을 리턴하기 때문에 1.
3. 문자열 'abab'에는 'abc'라는 문자열이 없으므로 -1.
4. 문자열 'abab'에 대문자 'AB'는 없기 때문에 -1.
```

ex) position값을 입력한 경우

```javascript
const str = "abab";

document.writeln(str.indexOf("ab")); // 0
document.writeln(str.indexOf("ab", 1)); // 2
```

```
1. position이 입력되지 않으면 position의 값은 0으로 처리된다.
   'abab'문자열의 0번째 인덱스부터 'ab'문자열을 찾고,
   0번째 인덱스에서 문자열 'ab'를 발견했기 때문에 0 리턴.

2. position값을 1로 입력했기 때문에 'abab'문자열의 1번째 인덱스부터 'ab'문자열을 검색한다.
   0번째 인덱스에 있는 ab는 무시한다.
```

‣ str.match(변수)

match() 함수는 찾고 싶은 단어가 있는 경우 해당 텍스트가 그 단어를 포함하고 있는지 찾을 때 사용한다.

또한 정규표현식을 사용하여 특정 패턴을 검색하는 것 역시 가능하다.

✷ str.indexOf와 str.match()

포함하고 있는 것을 찾는다는 것에서는 같다.

그러나 indexOf는 찾는 단어의 위치를 indexnumber만 리턴하고, match는 단어 자체를 리턴한다는 점에서 다르다.

ex)

```javascript
let str = "I love coffee.";
str.match(coffee);
// coffee라는 단어가 string안에 포함되어 있기 때문에 coffee를 리턴한다.
```

정규표현식에서 리턴하는 것도 가능하다(정규표현식은 따로 게시글 적어둠)

```javascript
let str = 'I love coffe, I love tea, I love you all.';
let test = /love/ig; // 찾을 단어를 / / 사이에 적어야 한다. 만약 / 하나만 쓰면 에러남.

str1 = str.match(test);
test라는 변수를 써서 정규표현식 코드를 작성하고, ig라는 것은 대소문자 구분 없이 전부 찾게 하기 위해 썼다.
// 결과값 (3) ['love', 'love', 'love']
```

✷ str.includes(searchValue); // true or false값을 리턴함

ex)

```javascript
"Red Apple".includes("Red"); // true
"Red Apple".includes("red"); // false
```

- str.split(seperator) → 분리 기준이 될 문자열

return value: 분리가 된 문자열이 포함된 배열

ex)

```javascript
var str = "Hello Everybody Nice To Meet You";
console.log(str.split(" "));
// ['Hello', 'Everybody', 'Nice', 'To', 'Meet', 'You']
```

⇒ csv형식 사용 시 유용

```
ex) let csv = 연도, 제조사, 모델, 설명, 가격

              1997,Ford,E350,"ac, abs, moon",3000.00

              1999,Chevy,"Venture ""Extended Edition""","",4900.00

              1999,Chevy,"Venture ""Extended Edition, Very Large""",,5000.00

              1996,Jeep,Grand Cherokee,"MUST SELL! air, moon roof, loaded",4799.00

      csv.split(',') [콤마 별로 내용이 분리되어 나오게 됨]

     줄바꿈을 표현하고 싶을 때는 csv.split('\n')
     [줄바꿈 된 것으로 한 줄 한 줄 정보가 나오게 됨]
```

‣ str.substring(start, end) → index의 시작과 끝을 넣어놓고 그 구간에 있는 문자열을 반환할 때 사용함

ex)

```javascript
var str = "abcdefghij";

// 'abc'←0부터 3 사이에 있는 문자열을 가져오되, 3은 포함하지 않음
console.log(str.substring(0, 3));

// 'abc'←start와 end의 순서가 바뀌어도 가져오는 것은 상관없이 잘 된다
console.log(str.substring(3, 0));

// 'abcd'←음수는 0으로 취급
console.log(str.substirng(-1, 4));

// 'abcdefghi'←index를 초과하는 숫자가 나오면 처음부터 끝까지 전부 나옴
console.log(str.substring(0, 28));
```

‣ str.substr(start, end)

ex)

```javascript
var str = "Hello World";
console.log(str.substr(1, 4)); // [ello]
```

시작과 끝을 넣어놓고 그 구간에 있는 문자열을 반환할 때 사용한다.

다만, str.substr은 끝부분도 포함한다.

‣ str.slice(start, end)←처음과 끝부분의 범위를 지정해서 잘라냄. 끝부분은 포함하지 않음.

ex)

```javascript
var str = "Hello World";
console.log(str.slice(0, 5)); // [Hello]
```

‣ str.reapeat(n) ←문자열을 n번 반복 연결한 문자열 반환

n에는 반복할 횟수(정수)가 들어가며, n을 생략하거나 0이 들어갈 경우에는 빈 문자열을 반환한다.

Array(n+1).join(str) ←문자열을 n+1번 반복 연결한 문자열 반환

반복할 횟수보다 +1 해주어야 함.

‣ str.toLowerCase() / str.toUpperCase() ⇒ 소문자 변환/대문자 변환

ex)

```javascript
console.log("APPLE".toLowerCase()); // 'apple'
console.log("apple".toUpperCase()); // 'APPLE'
```

✷ <mark>**모든 string method는 immutable, 원본이 변하지 않는다.**</mark>

ex)

```javascript
var str = "Red Apple";
console.log(str.substring(0, 4)); // 'Red '
str; // 'Red Apple'
```

⇒ method에 대한 결과값을 도출해냈을 뿐, 원본 string은 변하지 않았음

⇒ array method는 immutable과 mutable을 잘 구분해야 함

‣ Math.floor() // () 안의 인자를 내림

‣ Math.abs() // () 안의 절댓값. 양수, 0이면 양수 음수일 때도 양수

‣ Math.max() // 주어진 숫자들 중 가장 큰 값을 반환함.

‣ Math.min() // 주어진 숫자들 중 가장 작은 값을 반환함.

‣ str.join('') // 문자열 사이에 구분자를 넣어줄 수 있다.

ex)

```javascript
let str = ["A", "B", "C", "D", "E"];
```

우리는 이 각각 떨어진 문자열들을 하나로 합치고 싶다. 그렇다면 str.join('')을 이용하여 할 수 있다.

```javascript
str.join(""); // 결과값은 ABCDE로 나올 것이다.
str.join("and"); // 결과값은 AandBandCandDandE로 나올 것이다.
str.join("-"); // 결과값은 A-B-C-D-E
```

''와 'and'를 넣었는데 이렇게 나온다.

다시 예시의 string으로 돌아와보자. str을 A, B, C, D, E가 전부 떨어진 하나의 독립 문자열들의 모임으로 해놨다.

그래서 이 떨어진 문자열들을 ''(빈 문자열)과 - (하이픈)이라는 구분자를 사용하여 A, B, C, D, E라는 문자열들을 구분하기로 결정한 것이다. 마찬가지로 'and'를 넣었을 때도 마찬가지다.

‣ str.trim()

공백을 없애줄 때 사용한다.

ex)

```javascript
let str = " Hello, Everybody! ";
str.trim(); // 'Hello, Everybody!'
```

앞뒤로 있었던 공백이 사라졌다.

'Hello,'와 'Everybody!'사이에 있는 공백은 사라지지 않는 이유는 그 자체가 하나의 string이기 때문이다.

string을 제외한 공백을 없애줄 때 사용하는 함수이다.

다른 함수들과 달리 trim()은 따로 parameter를 써주지 않는다.

‣ str.replace(searchValue, newValue) // 문자열 내의 특정 문자열을 치환해 주기 위해서 사용함

replace() 함수는 searchValue, newValue를 파라미터로 입력받고

문자열에서 searchValue를 찾아서 newValue로 치환한다.

```javascript
let str = "apple, mac, ios";

// str에 있는 'ios'를 'android'로 변경하겠다는 말이다.
let replaced_str = str.replace("ios", "android");

// <br/n>태그를 이용하여 str를 입력한 후 줄바꿈을 하겠다는 말이다.
document.write("변경 전 : ", str, "<br/n>");

// <br/n>태그에서 줄바꿈을 했으니 이제 줄바꿈을 하지 않겠다는 말이다.
document.write("변경 후 : ", str, "<br/>");
```

✷ document.write은 문서에 의해 열린 문서 스트림에 텍스트 문자열을 쓰겠다는 말이다.

=== 내가 열어두었던 빈 브라우저 창에 ( )에 쓴 텍스트 문자열들을 쓴다는 의미.

그래서 입력값은

```
변경 전 : apple, mac, ios
변경 후 : apple, mac, android
```

로 된다.

두 번 이상 쓰면 str.replace했을 때 첫 번째로 발견한 문자열만 바뀐다.

```javascript
let str = "apple, mac, ios, ios";
let replaced_str = str.replac("ios", "android");
document.write("변경 전 : ", str, "<br/n>");
document.write("변경 후 : ", str, "<br/>");
```

입력값이

```
변경 전 : apple, mac, ios, ios
변경 후 : apple, mace, android, ios
```

로 바뀐 것을 알 수 있다.

다 바뀌게 하려면 정규식을 활용하면 된다.

```javascript
let str = "apple, mac, ios, ios";

// 슬래쉬(/)로 감싸서 파라미터가 정규식임을 알려주고,
// g(global match)라는 modifier를 붙여 전부 치환해달라고 명령했다.
let replaced_str = str.replac(/ios/g, "android");
document.write("변경 전 : ", str, "<br/n>");
document.write("변경 후 : ", replace_str, "<br/>");
```

입력값은

```
변경 전 : apple, mac, ios, ios
변경 후 : apple, mace, android, android
```

‣ replace()함수는 대소문자를 구분한다.

```javascript
let str = "apple, mac, IOS"; // IOS가 대문자다.
let replaced_str = str.replace("ios", "android");
document.write("변경 전 : ", str, "<br/n>");
document.write("변경 후 : ", str, "<br/>");
```

입력값은

```
변경 전 : apple, mac, IOS
변경 후 : apple, mac, IOS
```

아까와는 다르게 ios가 android로 바뀌지 않았다.

대소문자를 구분하기 때문에 str에 ios가 없다는 것을 알았기 때문에 치환이 안 된다.

대소문자를 구분하지 않고 치환하게 하기 위해서는 정규식을 사용한다.

```javascript
let str = "apple, mac, IOS";

// 슬래쉬(/)로 감싸서 파라미터가 정규식임을 알려주고,
// i(ignore case)라는 modifier를 붙여 대소문자를 구분하지 말라고 알려주었다.
let replaced_str = str.replace(/ios/i, "android");
document.write("변경 전 : ", str, "<br/n>");
document.write("변경 후 : ", str, "<br/>");
```

```
변경 전 : apple, mac, IOS
변경 후 : apple, mac, android
// 원래 'IOS'와 'ios'는 서로 다른 문자열로 취급하지만, 대소문자를 구분하지 말라고 알려주었기 때문에 치환되었다.
```

✷ String.prototype.match() → 문자열이 정규식과 매치되는 부분을 검색함.
