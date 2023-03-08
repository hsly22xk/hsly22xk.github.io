---
layout: single
title: "D+9 CSS"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

CSS의 전반적인 설명(1).

## 1. CSS

Cascading Style Sheets의 약자로 HTML과 같은 마크업 언어가 표현되는 방법을 결정한다.

CSS는 구조의 외부와 내부를 꾸미는 역할을 담당한다.

같은 HTML 구조를 가지고 있는 문서에, 각기 다른 CSS파일을 적용하면 전혀 다른 웹사이트처럼 보이게 할 수있다.

## 2. CSS 문법 구조

```css
body {
  color : blue;
  font-size : 20px:
}
```

body는 선택자(selector). 셀렉터로 태그 이름이나 id, class(특정 요소)를 선택한다.

특정 요소를 선택한 후 { } 안에서 이 요소에 적용할 내용들을 작성한다. color와 font-size가 여기서 쓰인 그 예이다.

{ } 안에 있는

```
color : blue;
font-size : 20px;
```

는 선언(declaration). 여기서 색깔은 파란색, 폰트 크기는 20으로 설정하여 스타일을 표현했다.

{ }안에 있는 선언들은 선언 블록(declaration block)

color, font-size는 속성명(property), blue와 20px는 속성값(value)

;(세미콜론)은 선언 구분자. 속성의 값과 끝에는 ;을 붙여 속성끼리 구분한다.

## ✷ 선택자, 속성, 값

querySelector를 알아보다가 자꾸 선택자, 선택자 하는데 그게 대체 뭔지 제대로 몰랐다.

**선택자는 선택을 해주는 요소다. 이를 통해 특정 요소를 대상으로 스타일을 적용할 수 있다.**

**속성은 좀 더 구체화된 명령어라고 생각하면 되겠다. 요소의 시작태그 안에 사용되어지며 다양한 효과를 부여한다.**

**값은 속성과 관련된 값을 말한다.**

## ✷ document.querySelector(CSS elements);

특정 name,id,class를 제한하지 않고 css선택자를 사용하여 요소를 찾는다.

같은 id 또는 class 일 경우 스크립트의 최상단 요소만 로직에 포함한다

## id, class

id와 class를 사용하면 특정한 <p>요소에만 스타일을 적용할 수 있다. 속성에 따라 스타일을 지정한다.

① class

스타일의 분류에 사용됨. 자주 사용되는 스타일에 적용하는 것.

한 컨텐츠를 여러 번 반복하는 경우 class를 이용하여 같은 css를 적용시킨다.

→ 빨간색이나 파란색 등 색상을 미리 지정하고 HTML에 적용시키는 방법
css에서 정의하는 방법은

```css
.class name {
  속성명: 속성값;
  속성명: 속성값;
}
// (class 앞에 . 붙이는거 중요함!)으로 적용한다.
```

하나의 class를 여러 tag에 지정시킬 수 있다.

② id

class와 다른 형태이다.
css에서의 정의 방법은 **#id name{ 속성명 : 속성값; 속성명 : 속성값; }** 으로 적용한다.

id를 사용 할 때 중요한 것은 class와 다르게 한 페이지에서 한 번만 사용이 가능하다. ⇒ 하나의 id당 하나의 tag에만 지정시킬 수 있다.

id는 페이지 내에서 특정 위치나 태그를 지정하는 것이기 때문에 오직 페이지 내에서 한 번만 사용할 수 있다.

로고나 상단 메뉴, 하단 정보 등의 고유의 컨텐츠에 스타일을 정의할 때 id를 쓴다.

⇒ 반복적으로 사용되는 컨텐츠는 class를 이용하여 정의하고, 그 내부에 스타일을 정의할 때 id를 쓰는 것이 효과적이다.

⇒ id의 속성이 class의 속성보다 우선순위가 높아 id의 속성은 해당 요소에 부여된 class의 속성과 관계없이 작동한다.

## 3. CSS box model

![](https://blog.kakaocdn.net/dn/J3GLI/btrhdWaK9lo/IlsHPTki10nyYS605soGp0/img.png)

모든 HTML 요소는 박스(box) 모양으로 구성되며, 이것을 박스 모델(box model)이라고 부른다.

박스 모델은 HTML 요소를 패딩(padding), 테두리(border), 마진(margin), 그리고 내용(content)으로 구분한다.

```
① 내용(content) : 텍스트나 이미지가 들어있는 박스의 실질적인 내용 부분
② 패딩(padding) : 내용과 테두리 사이의 간격입니다. 패딩은 눈에 보이지 않음
③ 테두리(border) : 내용과 패딩 주변을 감싸는 테두리.
⇒ 각 영역이 차지하는 크기를 파악하기 위해 레이아웃을 만들면서 그 크기를 시각적으로 확인할 수 있도록 만듦.

④ 마진(margin) : 테두리와 이웃하는 요소 사이의 간격. 마진은 눈에 보이지 않음
```

## CSS속성들

> width → 가로 길이
>
> height → 세로 길이

> 값의 단위
>
> auto: 기본값, 브라우저가 계산한 너비
>
> px: 픽셀
>
> % : 부모 요소에 상대적인 너비
>
> initial: 기본값으로 초기화
>
> inherit: 부모 요소로부터 상속 받은 값

✅ block과 inline, 그리고 inline-block

‣ block: 줄바꿈이 되는 박스. 즉 줄바꿈이 되고 크기 지정을 할 수 있다. 대표적인 요소(element)는 <div>와 <p>

⇒ 기본적으로 갖는 너비(width)는 100%, width와 height속성 지정 가능.

‣ inline: 옆으로 붙는 박스. 즉 줄바꿈이 되지 않고 크기 지정을 할 수 없다. 대표적인 요소(element)는 <span>

⇒ 기본적으로 갖는 너비(width)는 글자가 차지하는 크기만큼.

⇒ <span>태그의 경우 width와 height속성이 지정되지 않음.

그런 경우에 display: inline-block; 을 사용하면 width와 height의 속성을 지정할 수 있음.

ex)

```html
span { background: yellow; display: inline-block; width: 100px; height: 100px; }
```

inline-block속성을 이용하여 밑에 width와 height 속성을 지정할 수 있음.

display속성: 요소를 어떻게 보여줄 지 결정함.

‣ inline-block: 줄바꿈이 되지 않으면서 블록 박스의 특징을 가짐.

⇒ inline 박스처럼 다른 요소의 옆으로 붙으면서, 자체적으로 고유의 크기를 가진다.

⇒ 기본적으로 갖는 너비(width)는 글자가 차지하는 크기만큼.

> margin: 바깥쪽 여백 ⇒ 바깥쪽 여백에는 음수값을 지정할 수 있다.
>
> padding: 안쪽 여백

ex)

```
margin:10px → 상하좌우 모두 10px 여백
margin:20px 10px → 상하 20px , 좌우 10px 여백
```

(상하와 좌우의 여백이 각각 같다면 네 개를 전부 따로 쓸 필요는 없다)

```
margin:40px 30px 20px 10px → 위 40px, 오른쪽 20px, 아래 20px, 왼쪽10px 여백
margin:40px 30px 10px → 위 40px, 좌우 30px, 아래 10px 여백
```

```
margin-top → 위 여백 지정
margin-bottom → 아래 여백 지정
margin-left → 왼쪽 여백 지정
margin-right → 오른쪽 여백 지정
```

✷ 박스의 height 속성에 콘텐츠가 차지하는 공간보다 작은 값을 지정하면 콘텐츠가 박스 바깥으로 빠져나오게 된다.

즉, 박스 크기보다 콘텐츠 크기가 더 크면 내용이 박스 바깥으로 빠져나오게 된다.

콘텐츠가 박스를 뚫고 나가는 경우에는 박스 크기에 맞게 콘텐츠를 더 이상 표시하지 않거나,

혹은 박스 안에 스크롤을 추가하여 콘텐츠를 확인할 수 있게 만든다.

그 점을 방지하기 위해 우리는 overflow속성을 사용한다.

```
overflow: auto;
```

overflow에서 auto속성은 콘텐츠가 넘치는 경우 스크롤을 생성하도록 만든다.

```
overflow: hidden;
```

콘텐츠가 넘치는 경우 보여주고 싶지 않을 때 hidden을 사용한다.

```
overflow-x, overflow-y
```

overflow 속성은 x축과 y축을 지정해 가로 방향으로 스크롤하거나 세로 방향으로 스크롤 할 수 있게끔 지정할 수 있다.

이 두 속성을 이용하면 두 방향을 모두 지정할 수 있다.

## 박스 측정 기준

html 예시

```html
<div id="container">
  <div id="inner">inner box</div>
</div>
```

css 예시

```css
#container {
  width: 300px;
  padding: 10px;
  background-color: lightpink;
  border: 10px solid blue;
}

#inner {
  width: 100%;
  height: 200px;
  border: 2px solid red;
  background-color: lavender;
  padding: 30px;
}
```

container박스와 inner박스의 width를 똑같이 잡고, inner박스의 높이를 200px로 잡았으니 inner박스는 container박스에 들어갈까?

결론부터 말하자면 아니다. 브라우저에서의 실행은 다음과 같이 나온다.

```
#container                 #inner

300px(콘텐츠 영역)            300px(300px의 100%)

+ 10px(padding-left)       + 30px(padding-left)

+ 10px(padding-right)      + 30px(padding-right)

+ 2px(boder-left)          + 2px(boder-left)

+ 2px(boder-right)         + 2px(boder-right)
```

즉, container의 너비는 300px이 아닌 padding과 boder-width가 합쳐진 324px로 나오고 inner의 100% 또한 300px이 아닌 padding과 boder-width가 합쳐진 364px이 나온다.

CSS에서 width속성을 100%로 주게 되면 부모의 width만큼 너비가 설정된다.

하지만 content-box일 때 너비 100%에 이어 padding과 boder까지 주게 되어 부모 영역을 초과해서 너비가 정해진다.

따라서 위의 CSS예시에서 <mark>width와 height 외에 boder와 margin값을 따로 추가했기 때문에 원래 지정해주려던 영역보다 더 커졌다.</mark>

이러한 경우를 방지하기 위해 우리가 사용할 수 있는 박스 계산법이 있다.

여백과 테두리 두께를 포함한 박스 계산법이다.

```css
* {
  box-sizing: boder-box;
}
```

[(boder-box에 대한 예시)](https://www.codingfactory.net/10630)

여기서 \* 은 모든 요소를 선택하는 선택자(selector)이다.

모든 요소를 선택하여 box-sizing속성을 넣고, boder-box값을 추가하면 된다.

⇒ 지정한 width와 height만큼 영역크기를 맞춰주고 싶다면 boder-box를 사용한다.

## border

테두리를 지정하는 속성. boder 속성 하나만으로 여러 속성을 한번에 쓸 수 있다.

1)속성

boder-width → 테두리의 두께. px단위 사용

boder-style → 테두리의 스타일

‣ style값

```
solid: 실선
dotted: 점선
dashed: 조금 긴 점선
boder-coloer → 테두리의 색상. color값과 동일함
```

‣ 특정 테두리의 방향만 따로 설정

```
boder-top
boder-bottom
boder-left
boder-right
```

‣ 특정 방향만 두께, 스타일, 색깔을 따로 지정할 수 있다.

```css
boder-top-color: black;
```

✷ boder 속성으로 한꺼번에 지정하기 예제

```css
#box {
  boder: boder-width boder style boder-color;
}
```

boder-raidus → 테두리를 둥글게 만들어주는 속성. px와 % 단위 사용. boder 속성 없이 사용 가능.

총 4개의 모서리를 각각 다른 값으로 줄 수 있으며 값을 띄어쓰면 왼쪽 위부터 시계 방향으로 각각 다른 값을 지정함.

```css
#box {
  boder-radius: 10px;
}

#box {
  boder-radius: 1px 2px 3px 4px;
} //여러 방향을 왼쪽 위부터 시계방향으로 각각 다른 값을 지정한 예시
```

## color

글자의 색상을 지정하는 속성.

```
inherit → 기본값 , 부모의 색상을 가져온다
red 또는 blue → 이미 css로 정의된 색상
#000 또는 #FFFFFF → 16진수의 색상코드
rgb(255,255,255) → rgb 색상
rgba(200,100,150,0.5) → 알파(투명도)가 적용된 rgba 색상
```

## font

글자의 폰트를 정의하는 속성으로, 여러 개의 속성들이 존재한다.

```
font-style -> 기울기 등의 스타일 지정

nomal : 기본값
italic : 기울기

font-weight → 글자 두께

100~900 사이의 숫자를 통해 설정하거나, 지정된 값을 사용한다.
lighter (100)
normal (400)
bold (700)
bolder (900)

font-variant → 글꼴 변형. 즉 소문자를 대문자로 바꾸되 글자 크기를 소문자 크기로 함(한글에선 따로 의미는 없음).
```

```css
body {
  font variant : normal || small-caps || initial || inherit
}

normal : 소문자를 작은 대문자로 바꾸지 않음
small-caps : 소문자를 작은 대문자로 바꿈
initial : 기본값으로 설정
inherit : 부모 요소의 속성값 상속
```

font-size → 글자 크기

px 나 em등을 사용한다. 크기를 나타내는 값에 쓰인다.

line-height → 줄 간격(행간)

letter-sapcing →자간(글자 사이의 간격)
font-family → 글꼴

font 태그의 face 속성과 같다.
통상적으로 구글폰트에서 가져와서 head내부에 link태그로 External방식으로 적용시킨다.

✷ font 속성에 한번에 정의하는 예제

font : font-style font-variant font-wight font-size/line-height font-family

## 절대단위와 상대단위

① 절대 단위

고정된 값을 출력하며 절대 크기가 변하지 않는다.

크기가 가변적인 웹사이트가 아닌 경우에는 유용하지만, 반응형 사이트에서는 복잡하다.

px, pt 등

② 상대 단위

부모 요소나 다른 요소의 크기에 영향을 받아 상대적으로 크기가 변한다.

반응형 웹사이트를 만들 때 주로 사용한다.

%, em, rem, ch, vw, vh 등

```
‣ px : pixel, 글꼴의 크기를 고정하는 단위. 브라우저의 기본 글꼴 크기를 크게 바꾸더라도 크기가 고정된다.
‣ em : font-size, 부모 요소의 크기에 영향을 받아 크기가 변하므로 계산이 복잡하다.
‣ rem: 일반적으로 브라우저의 폰트 크기는 1rem이다. 브라우저의 기본 폰트 크기에 따라서만 상대적으로 변한다.
‣ %  : percent, 기본글꼴의 크기에 대하여 상대적인 값을 가짐. 부모 요소의 크기에 영향을 받아 크기가 변함
‣ ex : x-height, 최상위요소인 html요소의 크기에 영향을 받아 크기가 변함
‣ pt : point, 일반 문서(워드 등)에서 많이 사용하는 단위
```

[단위변환 사이트](http://pxtoem.com/)

## text-align

텍스트의 정렬 방향을 지정하는 속성.

```
left → 왼쪽 정렬
right → 오른쪽 정렬
center →가운데 정렬
jutify → 양쪽 정렬
```

## background

태그의 배경을 지정하는 속성으로, 여러 개의 속성들이 존재한다.

font 속성처럼 여러 개의 속성을 background 속성 하나만으로 한번에 쓸 수 있다.

① background-color → 배경 색 : color 값과 동일

✷ background와 background-color의 차이점

backgroud와 background-color 모두 색상을 지정할 수 있지만

background-color는 색깔만 지정할 수 있고

background는 color 이외의 다른 background 옵션들을 지정해 사용할 수 있다.

✷ 불투명속성을 넣어주기 위한 2가지 방법

```css
background-color: rgba(0, 0, 0, 0.8) // rgb가 모두 0이면 검정색, 투명도 80%;; ; ; ; ; ; ; ; ; ; ;
```

r: red[0~255] g: green[0~255] b: blue[0~255] a: (alpha)[0~1]

```css
background-color: #000; // 검정색
opacity: 0.8 // 투명도 80%;; ; ; ; ; ; ; ; ; ; ;
```

opacity값을 통해 투명도 조절이 가능하며, 범위는 [0~1]이다.

background-image → 배경 이미지 : 배경 이미지를 설정하며, 이미지 경로를 지정한다.

ex) background-image:url("이미지 경로 / 이미지 url 주소")

② background-repeat → 배경 이미지 반복 여부

값

```
no-repeat → 반복안함
repeat-x → x축으로 반복
repeat-y → y축으로 반복
repeat → 모든 방향으로 반복
```

③ [background-position](https://developer.mozilla.org/ko/docs/Web/CSS/position) : 배경 이미지 위치

```
숫자값 (x , y)
left
right
center
top
bottom
```

✷ background 속성 한번에 정의 예제

```css
#box {
  background: background-color background-image background-repeat
    background-position;
}
```

## text-decoration

글씨의 색깔, 선 등의 장식을 지정한다.

값

```
text-decoration-line : underline, line-through 등 장식의 종류.
text-decoration-color : 장식의 색.
text-decoration-style : solid, wavy, dashed 등 장식의 스타일.
text-decoration-thickness : 요소를 꾸미는데 사용되는 선의 두께를 설정.
```

ex)

```css
.under {
  text-decoration: underline red;
}

.over {
  text-decoration: wavy overline lime;
}

.line {
  text-decoration: line-through;
}

.plain {
  text-decoration: none;
}

.underover {
  text-decoration: dashed underline overline;
}

.thick {
  text-decoration: solid underline purple 4px;
}

.blink {
  text-decoration: blink;
}
```

## calc() in CSS

[괄호 안의 식을 계산한 결과를 속성값으로 사용하게 해주는 함수.](<https://developer.mozilla.org/ko/docs/Web/CSS/calc()>)

왼쪽에서 오른쪽으로 계산하고, 곱셈 혹은 나눗셈부터 계산한다. 만약 안에 괄호가 있다면 괄호 안부터 계산한다.

‣ calc()의 연산자 : +는 더하기, -는 빼기, \*은 곱하기, / 는 나누기.

더하기와 나누기는 연산자 좌우에 공백이 있어야 하지만, 곱하기와 나누기는 그럴 필요는 없다.

## z-index

[z-index](https://developer.mozilla.org/ko/docs/Web/CSS/z-index)는 레이어의 개념을 가지고 있다. 셀로판지를 여러 장 겹쳐서 하나의 그림을 만들어내는 것과 비슷하다.

⇒ 레이어가 있는데 화면이 평면이지만 층이 쌓인다고 가정했을 때 높이를 준다.

① z-index를 사용하려면 일단 positioning을 해야 한다(position 설정한 값에만 z-index가 적용된다).

non-positioning일 때는 z-index는 작용하지 않으며 늘 밑에 깔려 있게 된다.

② z-index는 양수의 값을 가지면 위로, 음수의 값을 가지면 밑으로 페이지가 위치하게끔 한다.

## CSS gradient

[그라데이션 효과, 토글 버튼 등에서 사용할 수 있다.](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Images/Using_CSS_gradients)

ex)

```css
.className {
  background: linear-gradient(blue, pink);
}
```

[transform in CSS](https://gahyun-web-diary.tistory.com/79)
