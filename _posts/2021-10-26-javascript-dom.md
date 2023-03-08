---
layout: single
title: "D+21 DOM"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

DOM 관련 전반적인 정리

## 1. DOM(Document Object Model)

프로그래머 관점에서 바라본 HTML.

⇒ HTML 요소를 Object(JavaScript Object / 객체)처럼 조작(Manipulation)할 수 있는 Model

⇒ document라는 전역변수로 접근 가능

✷ 그렇다고 DOM이 Javascript는 아님! 단지 DOM의 구조 접근을 Javascript를 이용해서 할 뿐!

① HTML에 Javascript 적용하기

script태그를 이용한다.

```
<script src="index.js"></script>
```

웹 브라우저가 작성된 코드를 해석하는 과정에서 script 요소를 만나면 HTML 해석을 잠시 멈추고 script 요소를 먼저 실행한다.

✅ script 요소는 등장과 함께 실행된다.

✷ script태그를 추가하는 두 가지 사례

‣ header태그에 추가함

body에 들어가는 script는 진행되지 않는다. script요소가 이미 head에서 실행됐기 때문이다.

‣ </body>가 끝나기 전에 추가함

html의 body가 모두 진행되고 script요소가 실행되기 때문에 모든 script가 진행된다.

따라서 <body>태그 마지막에 script요소를 넣어줘야 바르게 진행된다.

✷ html파일에서 우리가 알 수 있는 사실을 컴퓨터로 전달하는 방법

![](https://blog.kakaocdn.net/dn/bMAKPt/btriJvvOBQu/ReiOwBtQfkkYVe4IbBCJuK/img.png)

body 엘리먼트의 자식을 알아내라고 사람한테 얘기하면 파일을 직접 보고 알아내는 것이 일반적일 것이다. 하지만 이것을 컴퓨터에 전달할 때는 어떻게 해야 할까?

자바스크립트에서 DOM은 document 객체에 구현되어 있다. 이것을 알아보기 위해 위에 예제를 하나 만들었는데, 다음 질문에 대한 답을 어떻게 찾을 수 있을까?

- body 엘리먼트의 자식 엘리먼트(element)는 총 몇 개인가?
- id의 이름이 news-contents 인 div 엘리먼트의 부모 엘리먼트는 무엇인가?
- id의 이름이 first인 div엘리먼트를 포함해서 모든 자식 엘리먼트의 class 이름을 console.log를 사용하여 확인하는 방법은?

✷ body 태그의 속성 & 자식 엘리먼트의 개수를 콘솔로 구하는 방법

![](https://blog.kakaocdn.net/dn/cDEb9o/btriO1nMJOG/67BcV3yElJ51iULW4c48r1/img.png)

body태그를 찾아볼 때 우리는 콘솔 창에

console.log(document.body)와 console.dir(document.body)라고 입력해 볼 수 있다.

DOM의 구조를 알아볼 때는 console.log보다는 console.dir이 더 유용하다.

사진에서는 보여주지 않았지만, console.log는 html 구조처럼 나오는 반면 console.dir은 DOM을 객체의 모습으로 출력하기 때문이다.

사진에서 전부 보여주지 못하지만, console.log(document.body)를 입력하면 수많은 속성들이 나온다.

이는 HTML 엘리먼트에 지정할 수 있었던 다양한 속성이 이미 객체 내에 존재한다고 생각하면 된다.

✅ $0

$0는 해당 엘리먼트를 선택하면 개발자 도구의 Elements탭 html에서 해당 엘리먼트가 선택되면서 오른쪽에 $0표시가 생긴다. 그 상태에서 콘솔창에 console.dir($0)를 넣어 입력해보면 객체처럼 많은 내용들이 출력된다.

입력해보면 태그 형태, 태그의 클래스 이름, 태그의 아이디 이름, 텍스트, 부모 엘리먼트, 자식 엘리먼트 .... 등등을 볼 수 있다.

```
① tagName
$0.tagName; // "div"

② id
$0.id

③ className
$0.className;

④ classList
$0.classList

⑤ attributes : 속성으로 class, id, length 조회
$0.attributes // id와 class, length가 한 번에 다 나온다

ex)

$0.attributes // NamedNodeMap {0: class, 1: id, class: class, id: id, length: 2}
$0.attributes[0] // class
$0.attributes[1] // id
$0.attributes.length // 2

⑥ textContent, innerHTML
$0.textContent;

ex)

<div class="content">Hello</div>
라는 태그가 있다고 했을 때

$0.textContent = "World";
라고 하면

<div class="content">World</div>
로 내용이 바뀌는 것을 볼 수 있다.

$0.innerHTML;

ex)

<div class="content">Hello</div>
$0.innerHTML = <a href="http://www.abcd.com">abcd</a>
<div class="content">abcd<div>

링크를 넣었을 때 링크가 들어가는 것을 볼 수 있다.

⑦ value: form 입력 값

ex)

<input type="text' class email placeholder="이메일 주소를 입력하시오"></input>
라고 html파일에 입력하고 실제 브라우저 창에 asdf@asdf.com 이라는 이메일 주소를 입력했다면
$0.value // asdf@asdf.com 이라고 나온다.

⑧ dataset: 태그 자체에 데이터를 담고 싶을 때. 화면에 출력되지는 않음.

⑨ event

ex)
<button>Click</button>
$0.onclick = function() {
  console.log('Hello!');
}

or

$0.addEventListener('click', function() {
  console.log('Hello!')
});
라고 구현할 수 있다.
```

그렇다면 body태그의 자식 엘리먼트들은 어떻게 찾을 수 있을까?

![](https://blog.kakaocdn.net/dn/dG6qTG/btriPlTLgHi/HoY0eXGmbqVWxHSjVbzGn1/img.png)

body의 자식(children)을 바로 조회하는 명령어를 입력하면 된다

**<mark>document.body.children;</mark>**

✷ [currentNode](https://webplatform.github.io/docs/dom/TreeWalker/currentNode/)

✷ children(자식 엘리먼트)과 childNode(자식 노드)의 차이점

children은 텍스트 노드를 제외한 태그를 가리키고, childNode는 텍스트 노드와 태그 노드 모두 가리킨다.

![](https://blog.kakaocdn.net/dn/cBRSyS/btri0bvvE9J/mA4KOhY5Dp1tUn91cyqPv1/img.png)

(children과 childNode를 실제로 개발자 콘솔에 입력한 결과 예시)

✷ 부모 엘리먼트를 찾는 방법

일단 나는 위에서 news-contents라는 id를 가진 엘리먼트의 부모가 body엘리먼트 라는 것을 html파일을 보고 알아낼 수 있었다.

그런데 내가 원하는 것은 눈으로 직접 찾지 않고 콘솔창에서 알아내는 방법이다.

부모 엘리먼트를 알아내기 위해서 우선 id가 news-contents 인 엘리먼트를 조회해야 한다. 엘리먼트를 조회하려면, document.body.children 의 첫 번째 엘리먼트를 조회한다.

![](https://blog.kakaocdn.net/dn/lWkA2/btriRZbKnrn/ecNyEJGYk783t2IiSK8O11/img.png)

사실 body의 children을 조회할 때마다 매번 document.body부터 입력해서 children을 찾아가서 첫 번째 두 번째 세 번째... 이렇게 찾아가는 건... 솔직히 너무 귀찮다.

그렇다면 어떻게 할 수 있을까?

![](https://blog.kakaocdn.net/dn/O1BHG/btriQ5Q0zMf/kLrk2pnqKFrsQekWtn7A80/img.png)

따로 변수 선언을 해서 이 정보를 저장해두면 주소를 참조하기 때문에 언제든지 접근할 수 있다.

변수 newsContent(알아볼 수 있는 그 어떤 임의의 이름)를 따로 선언하여 id가 news-contents 인 엘리먼트를 할당한다.

⇒ Node.parentElement: 부모 엘리먼트를 가리키는 속성.

```
<div id = "news-contents">
```

의 부모를 찾기 위해 여러 가지를 이용할 수 있는데, 그중 id를 갖고 있을 때 사용하는 요소 getElementById를 이용하는 예제를 써볼 수 있다.

ex)

```js
let news = document.getElementById("news-contents");
// news라는 이름의 변수에 자식 요소 news-contents를 담는다.

let parent = news.parentNode;
// news의 부모 엘리먼트를 찾아주면 부모 엘리먼트를 가리킬 수 있다.
```

\* parentNode: Node객체의 기본 속성, 특정 엘리먼트의 부모 엘리먼트에 접근하고 싶을 때 사용할 수 있다.

이렇게 입력한 다음 console.dir(parent)를 입력하면 금방 body태그와 그 속성들이 쭉 나온다.

class를 갖고 있을 때는 getElementsByClassName을 사용할 수 있겠다.

\* 태그의 이름을 조회하는 메소드

document.getElementsByTagName('태그이름')

ex)

```
document.getElementsByTagName('div') // <div>태그 이름을 모두 조회한다.
=== document.querySelectorAll('div')와 같다.
```

✷ Node와 element는 무엇이며 무슨 차이가 있는지?

Nodelist와 element(HTML Collection)은 DOM nodes의 모음이다.

즉, 수많은 객체들로 이루어진 document인 것인데, 그 위에 존재하는 모든 객체들을 포괄하는 이름이 Node이다. 그래서 Node는 Element의 상위 개념이다.

Node의 기능을 적용한 객체는 여러 타입이 있는데, 그중 가장 많이 사용되는 타입이 Element이다.

Element는 예를 들자면 div, body 같은 태그들도 특정 타입이다. Node의 종류 안에 Element가 있는 것이라는 말로 보면 되겠다.

⇒ Element // Node.ELEMENT_NODE

✷ id의 이름이 first인 div엘리먼트를 포함해서 모든 자식 엘리먼트의 class의 이름을 console.log를 사용하여 확인하는 방법은?

대략 질문의 의도는 id first도 포함해서 그 안에 있는 모든 자식 엘리먼트들의 class 이름을 쭉 나오게 하라는 말이다.

여기서 알아야 할 것은

✅ 트리 구조

![](https://blog.kakaocdn.net/dn/m3nHj/btriRAwop8v/TRe0iNK9Ys9mRgrKYWKps1/img.png)

(DOM의 구조를 설명할 수 있는 트리 구조)

트리 구조의 특징은 부모가 자식을 여러 개 가지고, 부모가 하나인 구조가 반복되는 것이다.

즉, 부모가 가진 하나 또는 여러 개의 자식 엘리먼트를 조회하는 코드를 작성한다면 여러 번 반복해서 실행하는 코드가 필요하다.

그렇다면 아까의 질문을 수도코드로 작성해보자.

질문: id의 이름이 first인 div엘리먼트를 포함해서 모든 자식 엘리먼트의 class 이름을 console.log를 사용하여 확인하는 방법은?

```js
function consoleLogAllElement(element) {
  // first의 class 이름을 console.log 한다. → id first의 class이름을 나오게 하기 위해 class 이름을 console.log
  // first의 자식 엘리먼트가 있는지 검색한다. →logo, menu-wrapper가 자식 엘리먼트의 class이름
  // logo의 class 이름을 console.log 한다.
  // logo의 자식 엘리먼트가 있는지 검색한다. (없음)
  // menu-wrapper의 class 이름을 console.log 한다.
  // menu-wrapper의 자식 엘리먼트가 있는지 검색한다. →menu, menu, menu, profile-photo
  // 첫 번째 menu의 class 이름을 console.log 한다.
  // 첫 번째 menu의 자식 엘리먼트가 있는지 검색한다. (없음)
  // 두 번째 menu의 class 이름을 console.log 한다.
  // 두 번째 menu의 자식 엘리먼트가 있는지 검색한다. (없음)
  // 세 번째 menu의 class 이름을 console.log 한다.
  // 세 번째 menu의 자식 엘리먼트가 있는지 검색한다. (없음)
  // profile-photo의 class 이름을 console.log 한다.
  // profile-photo의 자식 엘리먼트가 있는지 검색한다. (없음)
  // 자식 엘리먼트를 모두 탐색했음
  // 함수 실행이 종료된다.
}
```

이런 식으로 반복 과정을 거쳐야 한다.

## 2. DOM의 CRUD

document 객체를 통해서 HTML 엘리먼트를 만들고(CREATE), 조회하고(READ), 갱신하고(UPDATE), 삭제(DELETE)하는 방법.

① Create

DOM으로 HTML을 조작하는 방법 중 기초적인 부분인 새로운 element를 만드는 방법

‣ 새로운 엘리먼트를 만든다.

```js
document.createElement("div");
```

제일 첫 번째로 documnet.creatElement라는 명령을 사용하여 새로운 div엘리먼트를 만들었다.

하지만 아직 안에 그 무엇도 들어가지 않았다.(추가된 엘리먼트는 맨 뒤에 붙는다.)

‣ 새로 만든 엘리먼트를 변수 tweetDiv에 할당한다(변수의 이름은 임의로 정한다).

```js
const tweetDiv = document.createElement("div");
```

하지만 아무 변화도 없다. 아직 만든 div 엘리먼트는 그 어디에도 연결되지 않은 상태다. 공간은 만들어졌지만, 그 공간은 그냥 공중에 떠있는 상태라고 생각하면 조금 편하겠다.

✅ [append](https://webruden.tistory.com/634), [appenChild](https://webruden.tistory.com/634)

위에서 우리는 tweetDiv라는 변수를 선언해서 새롭게 만든 div엘리먼트를 할당해줬다.

하지만 언급했듯이 공중에 떠있는 상태다. 이것을 눈에 보이게 하려면 append를 사용해준다.

```js
document.body.append(tweetDiv); // 공중에 떠있는 상태인 tweetDiv를 body태그에 append해준다.
```

하지만 아무 내용도 보이지 않고, 변화도 보이지 않는데, 내가 잘못했나? 라고 생각이 들 땐 개발자 도구 콘솔 창에서 Elements를 확인하면 된다. 잘 추가된 것을 확인할 수 있다.

그렇다면 왜 내용이 보이지 않을까? 새로운 엘리먼트를 만들 때 새로운 내용을 추가해주지 않아서 그런 것뿐이다.
(내용 넣는 방법은 Update에서 조금 더 자세히 쓴다)

✷ id와 class 추가하는 방법

```js
document.createElement("div");
const div = document.createElement("div");

div.id = "testId"; // ''안에 id로 쓸 이름을 넣어준다.
div.className = "testClass"; // 마찬가지로 class에 쓸 이름을 넣어준다.
```

② Read

✅ querySelector, querySelectorAll

DOM으로 HTML 엘리먼트의 정보를 조회하기 위해서는 querySelector의 첫 번째 인자로 셀렉터(Selector)를 전달하여 확인할 수 있다.

셀렉터로는 HTML 태그, id, class 가 가장 많이 사용된다.

ex)

```js
const oneTweet = document.querySelector(".tweet");
```

⇒ 클래스 이름이 tweet인 HTML 엘리먼트들을 조회한다.

그러나 클래스 이름이 tweet인 엘리먼트들은 엄청 많은데, 이렇게 변수 oneTweet에 선언하여 할당한 클래스 tweet은 단 하나다.

모든 엘리먼트들을 다 조회할 때 사용하는 것이 바로 querySelectorAll이다.

ex)

```js
const oneTweet = document.querySelectorAll(".tweet");
```

⇒ 클래스 이름이 tweet 인 모든 HTML 엘리먼트를 유사 배열로 받아온다. 이렇게 조회한 엘리먼트들을 배열처럼(배열이 아니지만) for문을 사용할 수 있다.

배열이 아닌 배열을 유사 배열, 배열형 객체(정식 명칭: Array-like Object)라고 한다.
(= 같은 기능을 하는 getElementByTagName('div') // 모든 div 태그들을 조회함)

✷ 유사 배열에서 배열로 바꾸는 방법 (how to convert nodelist into javascript array)

(Nodelist는 배열이 아니라, 노드의 콜렉션이다. 그래서 배열의 메소드는 사용할 수 없다.)

```
① Array.from()
② spread syntax // ex) const divArr = [...div]
③ Array.prototype.slice()
```

⇒①,②번은 옛날 브라우저에서는 안 됨. ③번은 옛날 브라우저에서도 됨.

✷ 위에서 언급했던 getElementById 라던가 getElementByClassName같이 앞에 get이 붙은 메소드는 사실 옛날 방식이지만, 호환성을 위해 가끔 사용해야 할 수도 있다. 이것들은 querySelector와 같은 역할을 한다.

ex)

```js
const getOneTweet = document.getElementById("container");
const queryOneTweet = document.querySelector("#container");

console.log(getOneTweet === queryOneTweet); // true
// container라고 쓴 것은 임의의 문서에 id 이름이 container라고 했을 때 둘이 같다는 의미를 담은 예시.
```

![](https://blog.kakaocdn.net/dn/CU0IV/btriMJHJekz/0RSd8F6fRz5TKO54FFM4zk/img.png)

footer라는 id를 가진 div 안에 새로운 div 엘리먼트를 추가할 것이다.

document.creatElement('div') // div 엘리먼트를 새로 만든다.

```js
const tweetDiv = document.createElement("div");
// tweetDiv라는 변수 안에 새로 만든 div 엘리먼트를 할당한다.

const footer = document.querySelector("#footer");
// id footer의 엘리먼트들을 조회한 값을 footer라는 변수에 할당한다.
```

![](https://blog.kakaocdn.net/dn/FdMnx/btriSLqKEFA/R413IXbjSY6xuhUrrJFaVk/img.png)

개발자 도구에서 Element를 보면 footer안에 새롭게 만들어 준 div 태그가 있는 것을 확인할 수 있다.

✷ 만약 querySelector의 첫 번째 인자를 'div'로 넣으면 어떻게 될까?

document.querySelector()는 선택된 선택자 또는 선택자 그룹과 일치하는 문서 내 첫 번째 Element를 반환한다.
일치하는 요소가 없으면 null을 반환한다.

✷ querySelector의 부모는 꼭 document 객체여야 하는가?

document 하위의 어떤 객체든 자식 엘리먼트를 가지고 있다면 querySelector의 부모가 될 수 있다.

```js
footer.append(tweetDiv); // tweetDiv를 footer에 넣어준다.
```

③ Update

‣ textContent를 사용하여 새로 만든 div 태그 안에 내용을 집어넣을 수 있다.

<mark>기본 구문은 element.textContent = '내용'</mark>

ex)

```js
console.log(tweetDiv); // <div></div>

tweetDiv.textContent = "tweet";
console.log(tweetDiv); // <div>tweet</div>
```

실제로 콘솔 창에 입력하면 브라우저에 tweet이라는 내용이 담긴 div가 나오는 것을 확인할 수 있다.

그러나 이렇게 만든 div는 CSS 스타일링은 적용되지 않는다. CSS 스타일링을 적용하기 위해 classList.add를 사용한다.

ex)

```js
tweetDiv.classList.add("twittler");
console.log(tweetDiv); // <div class="twittler>tweet</div>
```

이제 우리는 CSS파일을 불러와 이 twittler에 CSS 속성을 추가할 수 있다.

```html
<head>
  <link
    rel="stylesheet"
    type="text/css"
    media="screen"
    href="css파일이름.css"
  />
</head>
```

head태그 안에 넣어 연결 가능.

✷ js에서 직접적으로 css속성인 diplay: none을 쓰는 방법

```
숨길 때: (document.querySelector로 불러온 아이디 or 클래스).style.diplay="none";
다시 보이게 할 때: (document.querySelector로 불러온 아이디 or 클래스).style.diplay="block";
```

✷ css파일과 class를 조합하는 방법

```css
.hide {
  display: none;
}
```

html파일에 css파일을 연결시켜 준 후

```html
<link rel="stylesheet" href="style.css" />
```

css 파일에 저렇게 작성하고 저장한다.

그 다음 html파일에 다시 돌아와서 내가 숨기고 싶은 클래스 이름에 hide를 붙여쓴다.

ex)

```html
<div class="a" hide></div>
```

✷ hide와 조합한 class를 js에서 활용하기

```js
// 가려진 것을 보이게 한다
a.classList.remove("hide");

// 보인 것을 다시 가려준다
a.classList.add("hide");
```

✷ setAttribue

정확히 키와 값이 무엇인지 정해준다.

id가 "javascript"이고, textContent가 "awesome"인 a 태그를 생성하기 위해 쓸 코드 예시

```js
let aElement = document.createElement("a");
aElement.setAttibute("id", "javascipt");
// id가 키이고, 'javascript가 값인 것을 setAttribute를 사용하여 정확하게 짚어준다.

aElement.textContent = "awesome";
```

ex) 새로운 html 파일을 만들어 부모 엘리먼트에 자식 엘리먼트를 새로 종속시켜 만들고 추가하는 예시

![](https://blog.kakaocdn.net/dn/dmavPZ/btri5jHaQFR/6fFbkNM7oF3FOrOup59LZk/img.png)

![](https://blog.kakaocdn.net/dn/yK8eu/btri0coJCUr/tZdeClSBYbsWYEyroK9Ul1/img.png)

위와 아래는 똑같은 결과로 나오지만 방식에 따라 다르게 쓸 수 있음을 보여준다. 예시에서는 innerHTML을 사용했지만 textContent를 사용하는 것이 보안상 좋음.

✷ textContent랑 innerHTML의 차이

‣ textContent

노드와 그 자손의 텍스트 콘텐츠를 표현하는 Node 인터페이스의 textContent 속성으로, 노드가 document 또는 Doctype이면 null을 반환한다.

다른 노드 유형에 대해서 주석과 처리 명령을 제외한 모든 자식 노드의 textContent를 병합한 결과 반환. 자식이 없는 경우 빈 문자열.

노드의 textContent를 설정하면, 노드의 모든 자식을 주어진 문자열로 이루어진 하나의 텍스트 노드로 대치한다.

HTML로 분석할 필요가 없다는 점에서 textContent의 성능이 더 좋으며, textContent는 XSS공격의 위험이 없다.

‣ innerHTML

innerHTML은 Element.innerHTML 이라는 이름 그대로 HTML을 반환한다.

간혹 innerHTML을 사용해 요소의 텍스트를 가져오거나 쓰는 경우가 있긴 하지만 textContent가 더 좋다. innerHTML은 보안상의 단점이 있다.

⇒ innerHTML을 사용하게 되면 innerHTML 값을 설정할 때 지정한 값이 HTML이나 XML로 파싱될 때 요소의 내용이 DocumentFragment로 대체된다.

이 때 제어할 수 없는 문자열을 설정할 수 있거나 보안 점검을 거치는 프로젝트일 경우 코드가 거부될 가능성이 있다.

④ Delete

✷ remove와 removeChild

⇒ 지운다는 개념으로 remove와 removeChild가 있지만 진짜 삭제를 해서 없어져버리는 것이 아닌 부모 자식간의 관계를 끊는 것으로 이해하면 좋다.

⇒ remove와 removeChild를 썼을 때 결과는 동일하게 나오지만 remove는 자식 엘리먼트만 참조하고, removeChild는 부모 엘리먼트와 자식 엘리먼트 모두를 참조한다.

![](https://blog.kakaocdn.net/dn/y1HKR/btri3VGLWYZ/6o1Kkbi5o4SrdGr7OfWHwK/img.png)

(remove와 removeChild의 차이를 보여주는 예시)

remove를 사용할 때는 자식 엘리먼트인 div1만 참조해서 사용하고, removeChild를 사용할 때는 자식 엘리먼트인 div2와 그의 부모 엘리먼트인 body까지 참조하는 것을 알 수 있다.

✷ 삭제하려는 엘리먼트의 위치를 알고 있는 경우에 사용하는 방법

‣remove

```js
const footer = document.querySelector("#footer");
const tweetDiv = document.createElement("div");

container.append(tweetDiv);
tweetDiv.remove(); // 이렇게 append 했던 엘리먼트를 삭제할 수 있다.
```

✷ 자식 엘리먼트를 지정해서 삭제하는 방법

‣removeChild

모든 자식 엘리먼트를 삭제하기 위해, 반복문(while, for, etc.)을 활용할 수 있다.

ex)

```js
const container = document.querySelector("#container");
while (container.firstChild) {
  // container의 첫 번째 자식 엘리먼트가 존재하면
  container.removeChild(container.firstChild); // 첫 번째 자식 엘리먼트를 제거한다.
}
```

⇒ 자식 엘리먼트가 남아있지 않을 때까지, 첫 번째 자식 엘리먼트를 삭제하는 코드이다.

하지만 이 방법을 사용하면 모든 제목까지 전부 지워지게 된다. 이것을 방지하기 위한 방법으로

```js
const container = document.querySelector("#container");
while (container.children.length > 1) {
  // container의 자식 엘리먼트가 1개만 남을 때까지
  container.removeChild(container.lastChild); // 마지막 자식 엘리먼트를 제거한다.
}
```

아니면

✷ 직접 클래스 이름이 tweet인 엘리먼트만 찾아서 지우는 방법
(지우고 싶은 엘리먼트들에 달린 클래스 이름을 찾아 지운다)

```js
const tweets = document.querySelectorAll(".tweet"); // 클래스 이름을 찾는다
tweets.forEach(function (tweet) {
  tweet.remove(); // 함수 안에서 해당하는 클래스 이름을 찾아 지운다.
});
```

라고 쓰거나

```js
for (let tweet of tweets) {
  tweet.remove();
}
```

라고 쓰거나.

✷ 위의 예시에서 forEach는 되는데 reduce는 안 되는 이유

: 우선 위에서 쓰인 forEach()는 Array.prototype.forEach(). 즉 주어진 함수를 배열 요소 각각에 대해 실행한다.

앞에서도 잠깐 언급했지만, Nodelist는 배열이 아니라 노드의 콜렉션이기 때문에 배열 메소드들을 사용할 수 없다.

Nodelist 사용 가능한 메소드들은 Nodelist.item(), Nodelist.entries(), Nodelist.forEach(), Nodelist.keys(), Nodelist.values() 등이 있다.

즉 배열 메소드를 사용할 수 없기 때문에 reduce는 사용 불가이지만 forEach는 Nodelist의 메소드이기도 하기 때문에 사용이 가능하다.

✷ 여러 개의 자식 엘리먼트를 지우는 방법

‣ innerHTML

```js
document.querySelector("#footer").innerHTML = "";
// id가 footer인 엘리먼트 아래의 모든 엘리먼트들을 지운다.
```

하지만 이 방법은 보안상의 문제가 있다.

✷ offsetWidth와 offsetHeight

margin을 제외한 padding값, border값까지 계산한 값

```js
document.querySelector(".classNameSomething").offsetWidth;
document.querySelector(".classNameSomething").offsetHeight;
```

✷ offsetTop

부모요소의 상단으로부터 떨어진 top값을 계산한 값. 부모요소로부터의 떨어진 값을 계산하는 상대적인 값이다.

따라서 요소의 절대적인 값을 계산하기 위해서는 부모의 top값도 함께 구해 더해주어야 한다.

기본 구문

```js
document.querySelector(".classNameSomething").offsetTop;
```

ex)

```js
function getSomething(element) {
  let something = element.offsetTop;
  if (element.offseetParent) {
    something += element.offsetParent.offsetTop;
  }
  return something;
}
```

✷ 함수를 쪼개는게 좋은 이유

① 어떤 함수가 무슨 역할을 하는 지 분명히 알 수 있음

② 재사용이 가능하다 ⇒ 하나의 함수는 하나의 동작만 해야하고 부가적인 영향을 끼치지 않는다(순수함수)

③일관된 코드 작성 가능
