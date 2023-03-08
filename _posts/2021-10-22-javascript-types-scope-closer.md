---
layout: single
title: "D+17 원시/참조자료형, 스코프와 클로저"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

원시 자료형과 참조 자료형, 스코프와 클로저의 내용 정리.

## 1. 원시 자료형과 참조 자료형

① 원시 자료형(primitive data type): 객체가 아니면서 메소드를 갖지 않는 6가지 타입

⇒ 문자열, 숫자, boolean(true or false), null, undefined, bigint, symbol이 포함된다.

⇒ 하나 하나의 변수에 각각의 값을 저장하여 꺼내온다.

⇒ 원시 타입에서 원시 타입의 값을 복사해올 때는 원래 타입에 영향을 미치지 않는다.

② 참조 자료형(reference type): 원시 자료형이 아닌 모든 것

⇒ 배열, 객체, 함수가 대표적이다.

⇒ 하나의 변수에 주소가 저장된다.

이런 특별한 동적으로 크기가 변하는 데이터를 보관하는 다른 공간(heap)에 많은 값을 보관하는 식이다.

⇒ 참조 타입에서 참조 타입의 값을 복사해올 때는 복사해온 값이 변하면 원래 타입에도 값이 변해 영향을 미친다.

✷ 참조 자료형에서 ===을 쓰는 것은 주소값이 같은 지에 대한 여부이기 때문에 []===[]라고 하면 false로 리턴된다. {} === {}도 마찬가지.

✷ 참조? 변수를 읽어오는 것이 아닌가요?

변수의 주소를 "참조"하여 실제 변수가 있는 장소에 어떤 데이터가 있는지 도착하고 나서야 비로소 "읽을 수" 있기 때문에 변수를 읽는다 보다는 "참조"한다 라고 말한다.

![](https://blog.kakaocdn.net/dn/PxMCe/btriycJzdEu/Kp6exgcEguOTJMB0Yxb25k/img.png)
(함수 선언과 변수 선언에서 알아두어야 할 기본내용)

✅ **<mark>매개변수: 함수가 정의될 때 정해놓는 것</mark>**

✅ **<mark>전달인자: 함수가 사용될 때 들어가는 것</mark>**

## 2. 스코프(scope)

① 스코프의 정의

![](https://blog.kakaocdn.net/dn/JbhA9/btripF0gad7/m6ckVCZ13S2HpWfnHFEht0/img.png)
(안쪽 스코프의 범위와 바깥쪽 스코프의 범위를 콘솔창에 찍은 예시)

변수에 접근할 수 있는 범위가 존재한다.

**중괄호(블록) 안쪽에 변수가 선언되었는가, 바깥쪽에 변수가 선언되었는가**가 중요한데, 이 범위를 스코프라고 부른다.

즉, 한마디로 <mark>변수 접근 규칙에 따른 유효 범위</mark> 라고 말할 수 있다.

상기 예시는 username이 바깥쪽에 변수로 선언되어 있고, 그 변수를 if 조건문 안쪽에 쓴다.

message 또한 안쪽에서 선언되어 불러온다. 그래서 if 조건문 안에 있는 console.log는 메시지가 출력된다.

그러나 바깥쪽의 console.log는 message가 안쪽에 변수로 선언되어 있기 때문에 범위를 벗어났다. 그래서 참조 에러가 뜬다.

사진처럼 검정색 화살표로 표시된 범위를 안쪽 스코프, 빨간색 범위는 바깥쪽 스코프라고 부른다.

![](https://blog.kakaocdn.net/dn/c2xE1G/btriycIiDka/wAlQpO9oCURxvHKiGfyRT0/img.png)
(함수에 의해 스코프의 범위가 나뉜 예시)

바깥쪽에 선언된 변수 greeting이 이번엔 안쪽 스코프 범위에 있는 함수 greetSomeone에 들어왔다.

리턴값을 변수 greeting + ' ' + 함수 안쪽에 선언된 변수 firsName으로 console.log 함수 greetSomeone의 결과값이 잘 나온다.

그러나 두번째로 쓴 console.log(firstName)은 역시 값이 반환되지 않는다. 그 이유는 위에서 말한 것과 동일하다.

firstName은 안쪽에서 선언된 것이기 때문에 바깥쪽 범위에 있는 변수가 아니기 때문에 불러올 수 없다.

✅ **<mark>바깥쪽 스코프에서 선언한 변수는 안쪽 스코프에서 사용 가능,</mark>**

**<mark>안쪽에서 선언한 변수는 바깥쪽 스코프에서는 사용 불가능.</mark>**

② 스코프의 규칙

‣ 안쪽 스코프에서 바깥쪽 스코프로의 접근은 가능하지만, 반대는 불가능하다.

⇒ 안쪽 스코프에서 변수 선언 키워드를 쓰지 않고 호출한 상태에서의 재할당이 가능하다. 반대로는 불가능.

‣ 스코프는 중첩이 가능하다(함수 안에 함수를 쓸 수 있는 것처럼).

![](https://blog.kakaocdn.net/dn/bAp4GJ/btriuh4M6Bj/kLgcqvCtQ4HFk83nl4nNGK/img.png)
(안쪽 스코프와 바깥쪽 스코프의 관계, 중첩 가능 설명 그림)

‣ 바깥쪽 스코프 중에서도 가장 바깥쪽의 스코프는 **전역 스코프(global scope)**라고 부른다.

전역을 제외한 모든 스코프는 **지역 스코프(local scope)**라고 부른다.

이 사진에서는 a만 전역 스코프, 나머지 b, c, d는 지역 스코프이다.

![](https://blog.kakaocdn.net/dn/bSAoup/btriyaX29b1/19CkHPG3ydTnmck5e3WXRK/img.png)

(전역변수와 지역변수의 예시)

‣ 가장 바깥쪽에 있는 변수는 전역 변수, 안쪽에 들어와 있는 변수는 지역 변수라고 부른다.

‣ 전역 변수는 스코프 전역에서 사용이 가능하다.

‣ 지역 변수는 {}중괄호 안쪽에서만 접근할 수 있는 변수다.

⇒ 그래서 바깥쪽 스코프에 선언된 전역 변수는 안쪽에서 사용이 가능한 것이다.

<mark style="background-color: #F6B4C1">지역 변수는 전역 변수보다 더 높은 우선순위를 가지게 된다(중괄호 안쪽에서 사용이 가능하기 때문에).</mark>

![](https://blog.kakaocdn.net/dn/svpWy/btriuktQmco/INxAwg0adglNkKPKS6lFW0/img.png)

우선 지역 변수로 선언되어 할당된 값 'parkhacker'는 showName함수 내의 console.log(name);으로 했을 때 지역 변수로 내려온다.

showName함수 안에 선언된 name변수는 지역 변수이고, 지역 변수는 전역 변수보다 우선 순위가 높기 때문이다.

✷ 쉐도잉(variable shadowing)

동일한 변수 이름으로 인해 바깥쪽 변수가 안쪽 변수에 의해 가려지는(shadow) 현상

이제 지역 변수를 벗어나 쓰여진 console.log(name);은 kimcoding이 내려온다.

여기서의 name은 안쪽 스코프에서 작성된 지역 변수에 접근할 수 없는 스코프의 규칙에 의해서 전역 변수다.

그 다음 console.log(name);을 썼을 때도 전역 변수가 그대로 내려온다.

이 역시 앞에서 언급한 스코프의 규칙과 동일하다.

그래서 전역 변수가 'kimcoding'이라는 값으로 먼저 할당되었기 때문에 전역 변수 그대로 내려온다.

![](https://blog.kakaocdn.net/dn/bT3n5x/btrivPNvAA7/ESMJvdnoI2i4XO10f4XsZK/img.png)

(지역변수와 전역변수가 다르게 내려오는 예시)

앞의 예시에서 지역 변수에는 let을 붙였지만, 이번에는 지역 변수명 앞에 let이 붙지 않았다.

지역 스코프에서 새로 선언되지 않으면 그냥 다 같은 변수다. 즉, 안쪽 스코프에 쓰인 name은 전역 변수 name과 같다.

다만 전역 변수에서 처음 할당한 값이 안쪽 스코프에서 다른 값으로 바뀐 것이다(재할당됨).

처음에 name이라는 변수를 'kimcoding'이라는 값으로 할당하여 전역 변수가 내려오는 도중에, showName함수 안에 name이라는 값을 'parkhacker'로 바꿔버렸다.

이 name은 지역 변수이고, 함수 안의 console.log(name);은 우선 순위인 지역 변수가 내려온다.

다음 함수 바깥에 쓰인 console.log(name);이다. 이 때는 앞에서도 계속 언급했지만, 안쪽 스코프에 쓰인 지역 변수에 접근을 할 수 없기 때문에 전역 변수인 'kimcoding'이 내려온다.

이제 그 다음 console.log(name);이다.

앞에서 전역 변수의 값이 내려왔고, 이 이후에는 전역 변수 name의 값이 바뀐 값으로 취급하고, 바뀐 값은 'parkhacker'이다.

그래서 마지막 console.log(name);은 'parkhacker'가 된다.

③ 스코프의 종류

‣ 블록 스코프: {}중괄호를 기준으로 구분되는 범위

![](https://blog.kakaocdn.net/dn/vSYT4/btriwI8r9FD/WKXSJnN7Z03upvf0kudfj1/img.png)

(블록 스코프의 예시)

![](https://blog.kakaocdn.net/dn/zQOqe/btrisMxRI4W/CD81y2gEHzpSjkKLGurmA1/img.png)

(함수 스코프의 예시)

‣ function 키워드가 등장하는 함수 선언식 및 함수 표현식은 함수 스코프를 만든다.

✷ 주의사항: 화살표 함수는 블록 스코프다.

![](https://blog.kakaocdn.net/dn/q5g6Q/btriycn1VyQ/JgtMDA8k80jr66OS1S6Jp0/img.png)

## 3. var, let, const의 차이점

var는 function scope이고, let, const는 block scope이다.

실제로 var 명령어로 변수를 선언하여 js파일과 html파일을 만들고, html파일을 크롬 브라우저로 연 후 개발자 도구의 소스에 들어가 js 파일을 열어보았다.

return에 breakpoint를 걸고 페이지를 새로고침 해보았을 때 scope에 지역 변수가 3개(this 제외) 떴다.

![](https://blog.kakaocdn.net/dn/oJizD/btrirxgnszx/LZor6ihfiAYbNHaMiswP71/img.png)

함수 greetingSomeone 안에 정의된 모든 변수를 지역 변수에서 사용 가능한 것을 확인했다.

이제 js파일에서 var를 let으로 바꿔보고 똑같이 해봤다

(참조 오류에 가려진 텍스트는 let greeting = 'Good Night';)

![](https://blog.kakaocdn.net/dn/nSWWU/btritLZRmCz/L22YF2g7CiBoj8PvRNQLQ0/img.png)

greeting이라는 변수는 if문 안에 선언되어있고, return문은 if문 바깥에 써있다.

즉, 반복문을 벗어난 return문에서의 변수 greeting은 사용할 수 없게 되었다.

![](https://blog.kakaocdn.net/dn/cUtBgw/btrioFMNlGz/0SnhOBPezwcG4x66VJWW0K/img.png)

greeting변수는 block안쪽에서만 접근이 가능하다. ↓

![](https://blog.kakaocdn.net/dn/JCFzr/btripwaXFGS/z1W7hkGXmKZXRGJ2EgGjkK/img.png)

debugger라는 명령어가 들어가있는 범위 안에서만 저장되어 있는 블록 스코프의 변수가 greeting.

반면 var는 이런 블록 스코프를 무시했고, 재선언을 했지만 에러도 나지 않았다. 이것이 var 대신 let과 const를 쓰는 이유다.

✷ var와 let의 차이점

‣ 호이스팅: 자바스크립트 코드를 실행시키기 전에 선언된 변수와 함수를 가져가 메모리에 저장시키는데, 함수가 실행되기 전에 안에 있는 변수들을 범위의 최상단으로 끌어올리는 것.

ex)

```javascript
console.log(a);
ReferenceError: a is not defined

console.log(a);
var a  = 1;
console.log(a);
// 에러가 뜨지 않고 undefined 1로 나옴.
// —> 자바스크립트 엔진이 a라는 변수를 미리 저장해두고
// console.log(a)부터 읽어서 undefined라는 값을 내주고 그 다음에 1이라는 값을 내줌.
```

‣ var는 호이스팅 시 변수의 선언과 초기화(undefined로)를 같이 시킴

‣ var는 지역변수와 전역변수의 개념이 확실하지 않다.

→ var는 함수만 지역변수로 호이스팅이 되고 나머지는 전부 전역변수로 올린다.

‣ let도 호이스팅은 되지만 TDZ(Temporal Death Zone, 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 공간) 라는 개념이 있어 변수가 선언이 되어 기억된 것은 알지만, 변수의 초기화문이 나오기 전까지는 접근할 수 없다.

즉, 변수가 선언된 라인 전까지는 변수를 쓸 수 없다.

조금 더 간단한 예시를 들어보면

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i); // 5번 반복
}
console.log("final i:", i);
```

let 키워드를 써서 반복문을 썼을 때 바깥쪽에 쓰여진 console.log는 Reference Error가 뜬다.

블록 스코프 안에서 정의된 변수 i는 블록 범위를 벗어나는 즉시 접근할 수 없기 때문이다.

```javascript
for (var i = 0; i < 5; i++) {
  console.log(i); // 5번 반복
}
console.log("final: i", i);
```

var 키워드를 써서 반복문을 썼을 때다.

<mark style='background-color: yellow'>var 키워드는 for 문이 만들어낸 블록 스코프를 무시하기 때문에 블록을 벗어났음에도 불구하고 변수 i에 접근할 수 있다.</mark>

그러므로 결과는 5가 나온다.

|                |     var     |            let             |           const            |
| :------------: | :---------: | :------------------------: | :------------------------: |
|    유효범위    | 함수 스코프 | 블록 스코프 및 함수 스코프 | 블록 스코프 및 함수 스코프 |
| 값 재할당 여부 |    가능     |            가능            |           불가능           |
|  재선언 여부   |    가능     |           불가능           |           불가능           |

## 변수 선언에서의 주의점(전역객체 window의 이해)

‣ window객체(only 브라우저)

✅ var로 선언된 전역 변수 및 전역 함수는 window객체에 속하게 된다.

개발자 도구를 열어 콘솔에 window라고 입력하면

```
window;
Window {
  window: Window, self: Window, document: document, name: '', location: Location, …
}
```

이렇게 객체 하나를 조회할 수 있다.

이 객체는 브라우저의 창(window)을 의미하는 객체이지만 이와 별개로 전역 영역을 담고 있기도 하다.

함수 선언식으로 함수를 선언하거나, var로 전역 변수를 만들면, window 객체에서도 동일한 값을 찾을 수가 있다.

⇒ window 객체는 모든 객체가 소속된 객체이고, 전역객체이면서, 창이나 프레임을 의미한다.

✅ 전역 변수는 최소화하기

전역 변수는 가장 바깥 스코프에 정의한 변수이며 어디서든 접근이 가능하다.

모든 변수를 바깥으로 빼면 스코프 걱정을 안해도 될텐데 라는 생각을 했지만, 그다지 좋은 생각이 아니었다.

전역 변수는 편리한 대신 side effect(다른 함수나 로직에 의해 의도되지 않은 변경)가 발생할 수 있다.

side effect(부수 효과)를 최소화하면 의도되지 않은 변경을 줄일 수 있어

이에 따른 오류로부터 보다 안전하게 값을 보호할 수 있다.

✅ var는 블록 스코프를 무시하며 재선언을 해도 에러를 내지 않는다.

같은 스코프에서 동일한 이름의 변수를 재선언하는 것은 버그를 유발한다. 따라서 let, const를 주로 사용하는 것이 좋겠다.

또한 전역 변수를 var로 선언하는 경우 브라우저의 내장 기능을 사용하지 못하게 만들 수도 있다.

🚫 선언 없는 변수 할당 금지

var, let, const과 같은 선언 키워드를 쓰지 않고 변수를 할당하지 말라는 뜻이다.

**선언 없이 변수를 할당하면, 해당 변수는 var로 선언한 전역 변수처럼 취급된다.**

![](https://blog.kakaocdn.net/dn/bju5vM/btrizyZgCOK/C5kcWgHKXan6aU3xP1XuS0/img.png)

예시 사진에서처럼 age라는 변수를 선언 키워드 없이 할당했다. 저 age라는 변수는 이제 전역 변수로 취급되었다.

그래서 함수 안에 있는 console.log(age);의 출력값도 90, showAge();를 거친 console.log(age);와 console.log(window.age);의 값도 전부 90으로 출력된다.

✅ strict mode 발동과 취소

사실 이런 것은 애초에 브라우저에서 방지해준다면 더 안전하게 코드를 작성할 수 있다.

Strict Mode는 브라우저가 보다 엄격하게 작동하도록 만들어준다. 바로 앞에서 언급한 선언 없는 변수 할당의 경우도 Strict Mode는 에러로 판단한다.

Strict Mode를 적용하는 방법은 js 파일 스크립트 최상단에 'use strict' ('' 따옴표도 포함해서 써줘야함) 입력한다.

strict mode가 발동되면 취소할 수 없다. 취소할 수 있는 명령어도 없다.

✷ 변수를 정의하는 방법(정리)

let 외에도 var 키워드를 사용하는 방법이 있다.

var 키워드로 정의한 변수는 블록 스코프를 무시하고, 함수 스코프만 따른다.

그러나 모든 블록 스코프를 무시하는 건 아니고 화살표 함수의 블록 스코프는 무시하지 않는다.

함수 스코프는 함수의 실행부터 종료까지이고, var 선언은 함수 스코프의 최상단에 선언된다.

선언 키워드 없는 선언은 최고 스코프에 선언된다.

함수 내에서 선언 키워드 없는 선언은, 함수의 실행 전까지 선언되지 않은 것으로 취급한다.

보통 코드를 작성할 때 블록은 들여쓰기가 적용되고, 그 구분이 시각적으로 분명해서 많은 사람들은 블록 스코프를 기준으로 코드를 작성하고, 생각한다.

그러나 var는 이 규칙을 무시하기 때문에 블록/함수 스코프에 대한 이해가 없으면 코드가 다소 혼란스러울 수 있다. 즉, var 보다는 let 으로 변수 선언을 하는 것을 권장한다.

## 4. 클로저(closure) 함수

함수가 선언된 환경의 스코프를 기억하여 함수가 스코프 밖에서 실행될 때에도 이 스코프에 접근할 수 있게 하는 기술.

어떤 함수를 렉시컬 스코프 밖에서 호출해도, 원래 선언되었던 렉시컬 스코프를 기억하고 접근할 수 있도록 하는 특성.

외부 함수에 접근할 수 있는 내부 함수 혹은 이러한 원리를 일컫는 용어.

스코프에 따라서 내부함수의 범위에서는 외부 함수 범위에 있는 변수에 접근이 가능하지만 그 반대는 실현이 불가능하다.

① 클로저 함수의 특징

‣ 함수가 함수를 리턴한다고?

![](https://blog.kakaocdn.net/dn/IGGiA/btriwxzSpBi/VPeJMgo7JlZXhM6irU5yk1/img.png)

(함수를 리턴하는 함수라는 것을 보여주기 위한 예제)

화살표 함수가 두 개? 함수의 호출이 두 번 일어났다. 즉, 리턴값은 함수의 형태이고, adder는 함수를 리턴하는 함수다.

![](https://blog.kakaocdn.net/dn/tK9h5/btrizVmxN6w/fMkBZV3D2SshnIVVNWkw81/img.png)

(클로저 함수의 리턴값 예제)

앞에서 adder함수를 보여준 예제와 같은 동작을 하는 코드 사진이다.

클로저 함수는 **함수를 리턴하는 함수가 클로저의 형태를 만든다.**

- 클로저는 리턴하는 함수에 의해 스코프(변수의 접근 범위)가 구분된다.

클로저의 핵심은 스코프를 이용해서 변수의 접근 범위를 닫는(closure; 폐쇄)데에 있다.

따라서, 함수를 리턴하는 것만큼이나, **변수가 선언된 곳이 중요하다.**

![](https://blog.kakaocdn.net/dn/eBgiI6/btriwx7R0wQ/ksr2jFKwVO8v20pOI0Vwt0/img.png)

(외부 함수(바깥쪽 스코프)와 내부 함수(안쪽 스코프)의 예제)

그림에서 보다시피, 초록색이 외부 함수이고, 빨간색이 내부 함수다.

그렇다면 외부 함수는 내부 함수의 변수 y에 접근이 가능한가? 또, 내부 함수는 외부 함수의 변수 x에 접근이 가능한가?

✅ 첫번째 질문의 대답은 No, <mark>바깥쪽 스코프에서 안쪽 스코프로의 접근은 불가능하다.</mark>

✅ 두번째 질문의 대답은 Yes, <mark>안쪽 스코프는 바깥쪽 스코프에서 선언된 변수에 접근 가능하다.</mark>

![](https://blog.kakaocdn.net/dn/XP35M/btriBBV8z3B/XsvgzlLrd5kKq9oFBVuQz0/img.png)

↑ 클로저 함수의 특징 두번째는 <mark style="background-color: #F6B4C1">내부 함수는 외부 함수에 선언된 변수에 접근 가능하다</mark>는 것을 알 수 있다.

ex)

![](https://blog.kakaocdn.net/dn/bE358O/btriAHca3wK/k60rSAyOEVOFxMNzn3tEV1/img.png)

큰 빨간색 네모는 외부 함수, 초록색 네모는 내부 함수이다.

그리고 빨간색 네모 쳐진 var 변수는 외부 함수에 정의되어 있는 지역 변수이다.

이 내부 함수에서 title이라는 변수를 사용하려 할 때 내부 함수 안에 title이라는 지역 변수가 존재하지 않는다면 자바스크립트는 이 내부 함수를 포함하고 있는 외부 함수에서 title이라는 변수를 찾게 된다.

② 클로저 함수의 활용

![](https://blog.kakaocdn.net/dn/cYO9P8/btriuYx4Qck/Owibhrdx65XkQwJ0KBgjsk/img.png)

(외부 함수의 실행이 끝난 후에도 계속해서 사용할 수 있는 것을 보여주는 예시)

일반적인 함수는 함수 실행이 끝나고 나면 함수 내부의 변수를 사용할 수 없지만

**클로저는 외부 함수의 실행이 끝나더라도 외부 함수 내 변수가 메모리 상에 저장된다.**

변수 add5에는 클로저를 통해 리턴한 함수가 담겨 있고, adder함수에서 인자로 넘긴 5라는 값을 x 변수에 담은 채로 계속 남아있다.

![](https://blog.kakaocdn.net/dn/bn9ayx/btriAqT3AIL/i7gjXUQhgMjY504KHBd7wK/img.png)

(함수 실행이 끝난 후 add5라는 변수를 활용하는 예시)

ex)

![](https://blog.kakaocdn.net/dn/Z5JDN/btriDxlS3xa/rlizMRLWi5qK22Jof641KK/img.png)

빨간색 네모 쳐진 부분이 outer라는 외부 함수, 초록색으로 표시한 부분이 내부 함수이다.

그 내부 함수를 리턴하고 있다. inner라는 변수에 outer함수를 할당하도록 선언했다.

그렇다면 저 outer 함수를 실행한 결과는 내부 함수를 inner에 담는 것이다.

이제 inner라는 변수에 담겨있는 함수를 호출하면 outer함수에 담겨있는 변수의 할당값 'coding everybody'가 출력된다.

앞에서도 언급했지만, 일반적인 함수라면 return이 되었으니 outer 함수는 종료된다.

그러나 inner라는 변수에 함수를 호출한 순간에는 console.log(title); 구문을 실행한다는 것이다.

그런데 실행하려는 구문에 title은 내부 함수가 아닌 외부 함수에 존재하는 값이다.

즉, 외부 함수는 이미 종료되었지만 내부 함수에서 이미 종료된 외부 함수에 접근하고 있고, 그 접근은 성공적으로 이루어진다.

그래서 inner();를 호출하면 외부 함수의 변수의 할당 값인 'coding everybody'가 출력된다.

✅ 내부 함수를 포함하고 있는 외부 함수에 접근할 수 있고, 그 외부함수가 종료된 후에도 내부 함수를 통해 접근할 수 있다.

✅ **스코프 체인(=클로저 함수와 같은 말)**

스코프 체인은 scope의 가장 내부에서 scope chain을 따라 바깥쪽으로 검색을 하게 된다.

식별자를 찾을 때 일단 자신이 속한 스코프에서 찾고 그 스코프에 식별자가 없으면 상위 스코프에서 다시 찾아 나간다.

이 현상을 스코프 체인 이라고 하며 **스코프가 중첩되어있는 모든 상황에서 발생한다.**

예시를 들어보자.

ex)

①번 예시

```javascript
function outer() {
  const a = "a";
  console.log(a);
}

outer(); // a
```

②번 예시

```javascript
function outer() {
  const a = "a";
  const b = "b";
  function inner() {
    const a = "a";
    console.log(b);
  }
  inner();
}

outer(); // b
```

③번 예시

```javascript
const c = "c";
function outer() {
  const a = "a";
  const b = "b";
  function inner() {
    const a = "a2";
    console.log(c);
  }
  inner();
}

outer(); // c
```

⇒ ①,②,③번 예시에서 볼 수 있는 이것들이 바로 스코프 체이닝이다.

```
①번에서는 outer함수에 a 변수를 선언하여 'a'라는 값을 할당했다. 그렇게 outer함수를 호출하면 답은 a가 된다.


②번에서는 outer함수에 a, b변수를 선언하여 각각 'a'와 'b'라는 값을 할당했다.
그 상태에서 안에 inner함수를 넣어 a 변수를 선언하여 'a2'라는 값을 할당하고 console.log(b);를 구한다.
여기서 inner함수는 지역함수, outer함수는 전역함수가 된다.
지역함수에서 a 변수를 'a2'라고 선언했지만 b의 값을 구하는 것이 목적이기 때문에 그 상태에서 inner함수를 호출하면 b를 inner에서 찾을 수 없으므로 outer함수가 있는 위쪽으로 향한다. outer함수에는 b 라는 변수가 'b'로 할당되어 있다.

그래서 정답이 b가 된다.


③번 문제도 마찬가지다. 이번엔 함수를 먼저 선언하지 않고 c라는 변수에 'c'라는 값을 할당하여 선언했다.
그렇게 outer와 inner함수를 선언하고, inner함수 안에 console.log(c);를 구한다.
그렇게 inner함수를 호출하고, outer함수를 호출한다.
②번과 마찬가지로 inner함수에는 c의 값을 구할 수 있는 변수가 없기 때문에 outer함수가 있는 위쪽으로 올라간다.
그런데 outer함수에도 c가 없다. 그러면 위에 있는 전역 변수인 c까지 올라가게 된다.

그래서 정답이 c가 된다.
```

[④번 예시에서는 정답이 어떻게 될까?](https://github.com/codestates/agora-states/discussions/1716)

```javascript
const c = "c";
function outer2() {
  const d = "d";
  function outer() {
    const a = "a";
    const b = "b";
    function inner() {
      const a = "a2";
      console.log(d);
    }
    inner();
  }
}

outer2();
```

이렇게 실행시키면 inner(); is not defined라는 참조 오류가 뜨는 이유가 뭘까?

기본적으로 내부에서 외부로는 참조가 가능하지만, 외부에서 내부로는 참조가 불가능하다.

실제로 이 코드에서 inner함수에서 outer2함수로의 참조가 가능해서 console.log(d);는 출력이 되지만,

inner함수를 호출하고 outer함수에서의 참조를 거치지 않고 바로 outer2함수의 호출을 했기 때문에

inner함수에서의 참조 오류가 뜬다.

그렇다면 이 코드에서 outer2를 참조하여 console.log(d);를 출력할 수 있게 하려면 어떻게 바꿔주어야 할까?

```js
const c = "c";
function outer2() {
  const d = "d";
  function outer() {
    const a = "a";
    const b = "b";
    function inner() {
      const a = "a2";
      console.log(d);
    }
    inner();
  }
  outer();
}
outer2(); // d
```

간단하다. outer함수도 순차적으로 참조하게끔 만들어주면 된다.

② 클로저 함수의 응용

‣ 특정 데이터를 스코프 안에 가두어 둔 채로 계속 사용할 수 있게 해준다.

![](https://blog.kakaocdn.net/dn/GGAK9/btriuUWU1eI/pgr2QIKpn0asg70rwA7g5k/img.png)

(클로저를 이용해 HTML을 만드는 예시)

지금 이 예시에서는 divMaker라는 함수는 tag라는 변수 안에 'div'라는 문자열을 담아 계속 사용할 수 있게 만들었고,anchorMaker함수는 tag변수 안에 'a'라는 문자열을 담아두고 있다.

'div'와 'a'라는 특정 데이터를 스코프 안에 담아 계속 사용할 수 있도록 만들어준 것이다.

‣ 클로저 모듈 패턴

클로저를 이용해 객체에 담아 여러 개의 내부 함수를 리턴하도록 만든다.

![](https://blog.kakaocdn.net/dn/mpbkD/btriz7AwIPP/rT0C0q1ObrkokeoEK2Iw90/img.png)

(객체에 여러 개의 내부 함수를 리턴하도록 만든 예시)

‣ 정보의 접근 제한(캡슐화)

그렇다면 위의 예시에서 makeCounter 함수를 바꾸지 않고 value변수에 값을 새롭게 할당할 수 있을까?

'외부 스코프에서는 내부 스코프의 변수에 접근할 수 없다'는 규칙에 의해 어떤 경우에도 value는 직접 수정이 불가능하다.

대신, 리턴하는 객체가 제공하는 메소드를 통해 value 값을 간접적으로 조작할 수 있다.

✷ 왜 그럴까?

만일 스코프로 value 값을 감싸지 않았더라면, value 값은 전역 변수여야만 했을 것이지만 makeCounter라는 함수가 value 값을 보존하고 있기 때문에, 전역 변수로 따로 만들 필요가 없다.

③ 클로저 함수를 쓸 때 일어나기 쉬운 실수

ex)

![](https://blog.kakaocdn.net/dn/UfkbT/btriDx0wMin/kbuOgI0t3iqdKxya4t3eR0/img.png)

클로저를 사용하는 과정에서 일어나기 쉬운 실수를 예제로 만들어서 개발자 도구에 직접 실행을 해보았다.

우선 arr를 빈 배열로 할당하고 i는 0부터 시작, 5번 반복하면서 arr의 [i], 즉 배열의 순서번호(인덱스 넘버)는 함수로 정의하고, 그 함수는 i라는 변수를 사용하는데 이 때 i는 증감문에 있는 i와 같다.

즉, 이 배열에 저장되어 있는 함수를 호출할 때, 함수가 정의되어 있는 시점에서 console.log(i);를 출력하도록 하는 것이다.

for in문을 사용하여 배열 안에 있는 순서번호(인덱스 넘버)를 하나씩 꺼낸 후( (arr[index]) 라고 적는다) 함수를 호출하면

```js
for (var index in arr) {
  console.log(arr[index]());
}
```

console.log(i); 가 실행된다.

여기서 i가 함수가 생성된 시점에서의 문맥의 i의 값, 즉 앞에 써준 for문의 증감문인 i++의 i가 호출이 된다고 했을 때 i는 0부터 4까지 출력된다는 것이 기대하는 값이다.

그러나 실제로는 5만 5번 나온다. 이 부분은 console.log(i);를 return i;로 바꿔도 똑같았다.

return i;로 써주면 이제 함수의 값이 i로 리턴이 되고, 리턴된 i는 arr[index]();로 들어가게 되어 console.log를 실행시키면 0부터 4까지 나올 것이라 생각했지만 아니었다.

기대한 값이 나오지 않는 이유는 증감문에 써있던 i의 값이 정의했던 함수의 외부 변수의 값이 아니기 때문이다. 이 말은 함수에서 참조할 만한 외부 변수의 값이 없었다는 말이 된다.

그렇다면 코드를 어떻게 수정할 수 있을까?

![](https://blog.kakaocdn.net/dn/OeNll/btriBADIrKn/WC27Nzf188j7mEPJDzKl91/img.png)

위에서 언급했듯 i는 외부 변수값이 아니었기 때문에 증감을 하지 않고 그대로 5만 내려왔다. 일단 사진에서는 외부 함수와 내부 함수의 범위를 보다 정확하게 알기 위해 다시 표시해준다.

① 우선 원래 써주지 않았던 외부 함수를 하나 정의해준다.

```js
arr[i] = function() { // 외부 함수 정의
  function() {
    return i;
  }
}
```

② 이제 저 외부 함수를 바로 호출해준다.

```js
arr[i] = function() {
  function() {
    return i;
  }
}(); // 외부 함수 호출
```

여기까지하면 이제 내부 함수를 리턴하게 되는데, 그 리턴된 내부 함수가 배열에 담기게 된다.

하지만 여기서 i의 값은 아직 전역 변수, 즉 증감문의 i를 바라보고 있는 상태이기 때문에 아직 끝나지 않았다.

③ 이제 정확히 어떤 값을 호출할 지를 정해주어야 한다.

```js
arr[i] = function() {
  function() {
    return i;
  }
}(i); // 외부 함수의 매개 변수의 인자값을 i로 설정해준다.
```

④ 외부 함수에 id라고 하는 매개 변수를 가지게 해준다. 이 매개 변수는 곧 지역변수와 같은 역할을 하기 때문이다.

```js
arr[i] = (function (id) {
  // 지역 변수와 같은 역할을 하는 매개변수 설정
  return function () {
    return id; // ⑤ 그 지역 변수를 리턴하게 한다.
  };
})(i);
```

여기까지 하면 이제 반복문이 실행될 때마다 외부 함수가 실행이 될 것이다.

이 외부 함수는 실행이 되면서 id라고 하는 매개 변수의 값으로 증감문의 i의 값을 받아 내부 함수로 전달을 해준다.

전달과 동시에 내부 함수로 리턴을 하고, 그 내부 함수는 안에서 외부 함수의 지역 변수 id를 리턴하고 있다.

여기까지 했다면 개발자 콘솔을 돌렸을 때 값은 0 1 2 3 4가 나온다.

내부 함수의 지역 변수 id가 외부 함수의 지역 변수 id에 접근할 수 있었기 때문이고, 그 함수가 만들어지는 시점에서의 i값을 외부 함수가 id라고 하는 지역 변수로 가지고 있었기 때문이다.

그래서 외부 함수에 내부 함수를 호출하게 되면 외부 함수의 지역 변수 값 id를 리턴하게 된다.

⇒ 즉, 원래 써주었던 함수를 내부 함수라고 생각하고, **내부 함수를 감쌀 외부 함수를 하나 써주고 외부 함수의 지역 변수의 값을 내부 함수가 참조하도록 하면 된다.**
