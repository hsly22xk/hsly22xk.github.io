---
layout: single
title: "D+8 HTML"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

html의 전반적인 설명글.

```
‣ HTML: 웹 페이지의 구조를 담당하는 마크업 언어(Structure), 웹페이지의 구조를 표현하는 언어
‣ CSS: 디자인 요소를 시각화하는 스타일시트 언어(Presentation)
‣ JAVASCRIPT: 단순한 웹페이지를 프로그램으로 만들어 유저와 상호작용할 수 있게 해주는 프로그래밍 언어(Interaction)
```

ex)

집을 짓는다고 가정할 때, 집 구조에 대해 러프하게 작성해놓는 것은 HTML 문서를 작성하는 것과 같다.

집 구조를 그려놓은 하나의 문서를 보고 문서의 제목, 지붕과 창문의 위치, 문의 위치 등을 명확하게 표시를 하고, 지붕의 색깔과 저택의 외관 색깔, 집을 지을 때 쓸 수 있는 재료 등의 정보를 간단히 적어두는 것은 CSS문서 작성과 같다.

앞서 작성해놓은 HTML 문서를 보고 지붕, 창문, 문의 색깔과 사용할 재질에 대한 정보를 간단히 적어둔다.

집 안에 전등이 없다면 매우 어두울 것이기 때문에 밤이 되면 켜지고, 아침이 되면 다시 꺼지는 전등도 달아놓을 것이다.

이는 JAVASCRIPT와 같다.

앞서 써놓은 알고리즘을 js 언어로 옮겨놓으면

```javascript
if (isNight === true) {
  light.isOn();
} else {
  light.isOff();
}
```

(실제 집이 구조, 색깔, 재료, 전등으로만 구성하지는 않지만 HTML, CSS, JAVASCRIPT를 쉽게 이해하기 위해서 간단하게 쓴다)

## 1. HTML

HyperText Markup Language의 약자. 홈페이지의 틀을 만드는 마크업 언어.

‣ HTML은 Tag들의 집합이다.

```
Tag: <>로 묶인 HTML의 기본 구성 요소
요소: HTML에서 시작과 종료 태그로 쓰인 모든 명령어들. 태그명령어들 종류.
```

‣ HTML은 Tree Structure로 쓴다.

![](https://blog.kakaocdn.net/dn/xbVoK/btrhFSrkDbB/OLIyyuBT7IWC98TRukTKr0/img.png)

```
• HTML 문서 시작 // 선언

• html // 가장 상위의 태그, 부모

◦ head //html의 자식
    ◦ title: Page title // 텍스트만 포함할 수 있으며 태그를 포함하더라도 무시함

◦ body // html의 자식
    ◦ h1 //body의 자식
    ◦ div //body의 자식
      ◦ span // div의 자식
```

위에 쓴 트리 구조의 예시를 바탕으로 html문서를 하나 작성해보자.

```html
<!DOCTYPE html> // HTML 문서라는 것을 명시. 선언한 것.
<html> // html시작 태그, 문서가 시작되었음을 의미(opening tag)
  <head> //head의 태그는 문서의 메타데이터(기계가 읽을 수 있는 문서 정보, 사람이 읽을 수 있는 정보 아님)선언
    <title>Page title</title>
     // 브라우저의 제목 표시줄이나 페이지 탭에 보이는 문서 제목(오프닝, 클로징 태그 함께 씀)
  </head> //<head>태그가 끝났다는 표시. </ >로 쓴다 (closing tag)
  <body> //body의 태그는 문서의 내용을 담는 곳
    <h1>Hello Everybody</h1> //제목을 의미, 크기에 따라 h1부터 h6까지 있음(사람에게 보이는 제목 정보)
    <div>Contents here</div> //content division, 줄바꿈됨
      <span>Here, too!</span> //줄바꿈이 없는 content 컨테이너
    </div> // <div> 태그가 끝났음을 의미
  </body> // <body>태그가 끝났음을 의미
</html> // <html>태그가 끝났음을 의미
```

‣ 위의 예시에서는 html문서에 닫는 태그가 있었지만, 간혹 없는 경우가 있다.

태그 내부에 내용이 없을 때(<tag></tag>와 같이 표현되는 경우), self-closing tag를 사용할 수 있다.

```html
<img src="apple-logo.png"></img>
<img src="apple-logo.png" />
```

<img> 태그의 src라는 속성이 담겨져 있고 속성에 대한 값이 이미지 소스의 URL을 명시

✷ vs code에서 html형식으로 파일 형식을 바꾸고 html: 5를 치면 html 문서 형식이 그대로 나온다.

✷ vs code에서 html형식으로 파일 형식을 바꾸고 ! 를 치면 html 문서 형식이 그대로 나오는데, 이를 에밋이라고 한다.(플러그인의 한 종류)

✅ html에서 가장 많이 사용되는 태그들

① <div> // division, 영역을 설정할 때 필요, 박스 형태로 영역이 설정됨, 줄바꿈 가능, width와 height의 크기 설정 가능

② <span> // span , 영역을 설정할 때 필요, 줄 단위로 영역이 설정됨, 줄바꿈 불가능, width와 height의 크기 설정 불가능

ex)

```html
<div>div태그는 한 줄을 차지한다</div>
<div>division</div>

<span>span태그는 컨텐츠 크기만큼 공간을 차지한다</span>
<span>span1</span>
<span>span2</span>
<span>span3</span>

<div>division2</div>
```

이 내용을 <body>tag 안에 넣어주었다면 홈페이지에서 어떤 식으로 보일까?

(배경색은 이해를 돕기 위해 임의로 넣은 색)

> <mark>div태그는 한 줄을 차지한다</mark>
>
> <mark>division</mark>
>
> span태그는 컨텐츠 크기만큼 공간을 차지한다 span1 span2 span3
>
> <mark>division2</mark>

div를 넣은 부분은 줄바꿈이 되어 한 줄씩 차지하여 박스 형태로 나왔다. 마지막에 쓴 division2도 줄바꿈이 되어 나왔다.

반면 span을 넣은 부분은 줄바꿈이 되지 않고 한 줄로 그대로 쓰였다(=== 줄 단위로 영역이 설정되었다)

물론 CSS로 div와 span 상관없이 줄바꿈의 형태를 바꿀 수 있지만 이것이 html에서의 기본값이다.

<mark>div는 전체적인 레이아웃을 잡을 때, span은 텍스트 스타일 등 특정 부분에 스타일을 지정하고자 할 때 사용한다.</mark>

## <span> 스타일 속성 잡는 방법

> html 파일 안에 직접 적용하기
>
> 이는 다른 css 속성보다 먼저 적용된다.

```html
<span style="background-color: red; font-size: 10px"></span>
```

> <style>태그로 지정하기(internal)

```html
<head>
  <style>
    p {
      font-size: 2em;
      background-color: beige;
      border: 1px solid black;
    }
  </style>
</head>
```

구조와 스타일이 섞이게 되므로 유지보수가 어렵다.

별도로 css파일을 관리하지 않아도 되며 별도로 브라우저가 css파일 연결 요청을 보낼 필요가 없다.

하지만 그다지 선호하지 않는 방식.

> 외부 css 파일로 지정하는 방식(external)

```html
<html>
  <head>
    <link rel="stylesheet" href="style.css"
  </head>
  <body>
    <div>
      <p>
        <ul>
          <li></li>
          <li></li>
          <li></li>
        </ul>
      </p>
    </div>
  </body>
```

href="style.css"형식으로 외부 css파일을 지정하는 방식이고, 가급적 이 방법을 사용하며 선호한다.

현업에서는 여러 개의 css 파일로 분리하고 이를 합쳐 서비스에 이용하기도 한다.

위에서 봤던 internal코드와 같은 css를 쓰고, style.css와 같은 별도의 파일을 생성한다.

이후 html에서 <link>태그를 걸어주면 된다.

([참고링크])(https://0ver-grow.tistory.com/138)

## <span> text-align 스타일 잡는 방법

```css
.(span태그 class이름) {
  float: right;
}
```

```html
<span style="display: inline-block; width: 95%; text-align: right;"></span>
```

<span>은 스타일 속성을 직접 줄 수 없으므로 html파일 안의 span태그 안에 스타일을 사용하여 줄 수 있다.

아니면 class이름을 부여하여 float을 사용하여 정렬할 수 있다.

background나 font속성 등을 줄 때에는 style속성을 사용하여 줄 수 있다.

([참고링크])(https://coding-factory.tistory.com/189)

## img 태그

image, src 특성에 지정한 이미지로 나타나는 시각적 제출 버튼. 이미지 삽입 태그.

이미지의 src를 누락한 경우 alt 특성의 텍스트를 대신 보여주며, <img>tag에는 closing tag가 없음.

인터넷에서의 이미지를 넣어주려면 해당 경로 링크를, 저장되어있는 이미지를 넣어주려면 이미지 파일 경로를 넣어준다.

```html
<img src="C:\Documents and Settings\USER\My Documents\My Pictures\1.png" />
```

## 이미지에 링크 걸기

[<a>태그로 <img>태그를 감싸주면 된다.](https://velog.io/@muchogusto/a-href-%EB%AC%B4%EC%97%87%EC%9D%84-%EC%9D%98%EB%AF%B8)

```html
<a href="https://www.abcd.com" target="_blank"
  ><img src="C:\Documents and Settings\USER\My Documents\My Pictures\1.png"
/></a>
```

## a 태그

하이퍼링크를 걸어줄 수 있는 태그

```html
<a href="https://www.abcd.com" target="_blank">Go abcd</a>
```

여기서 target="\_blank"는 현재 창이 아닌 새 탭으로 사이트를 열리게 하는 속성이다.

## <ul>, <ol>, <li>

> <ul>태그는 순서가 필요없는 목록을 만듦(unordered list)
>
> <ol>태그는 숫자나 알파벳 등 순서가 필요한 목록을 만듦(ordered list)
>
> <li>태그는 <ol>과 <ul>의 항목을 나열할 때 사용함(list item)

```html
<ul>
  <li>Apple 1</li>
  <li>Apple 2</li>
  <li>Apple 3 has nested list</li>
</ul>
<ul>
  <li>Apple 3-1</li>
</ul>
```

첫 번째 <ul>tag에 있었던 리스트 아이템(<li>)인 Apple 1, Apple 2, Apple 3 has nested list가 나왔다.

```
• Apple 1
• Apple 2
• Apple 3 has nested list

    // 두 번째 <ul>tag에 있었던 리스트 아이템인 Apple 3 has nested list의 아이템 Apple 3-1이 나왔다.
    ◦ Apple 3-1
```

대부분 홈페이지의 메뉴에서 많이 쓰인다. 어떤 종류의 리스트라도 이것들을 사용한다.

반대로 순서가 필요하다면 <ul>tag를 써주었던 부분을 전부 <ol>tag로 바꿔주면 된다.

```
1. Apple 1
2. Apple 2
3. Apple 3 has nested list
   1. Apple 3-1
```

앞에 넘버링이 붙어서 나온다.

## input 태그

text, radio, checkbox 등을 사용한다.

> text: 디폴트 값. 한 줄의 텍스트 필드. 새 줄 문자는 입력값으로부터 자동 제거됨
>
> radio: 같은 name값을 가진 여러 개의 선택 중 하나의 값을 선택하게 하는 라디오 버튼
>
> checkbox: 단일 값을 선택하거나 선택 해제 할 수 있는 체크박스

ex)

```html
<div>ID <input type="text" placeholder="type here" /></div>
<div>Password <input type="password" /></div>
<div><input type="checkbox" /> ID 기억하기</div>
<div><input type="checkbox" /> 보안으로 접속하기</div>
```

```html
<input type="radio" name="option">a</input>
<input type="radio" name="option">b</input>
```

## textarea 태그

여러 줄의 긴 문장을 입력할 수 있는 양식의 태그.

## button 태그

기본 행동을 가지지 않으며 value을 레이블로 사용하는 푸시 버튼

```html
<div>
  <button>LogIn</button> // 태그 사이에 넣고 싶은 텍스트를 넣어 버튼 이름을 만듦
</div>
```

이렇게 하면 로그인 버튼이 생긴다. 다만 실질적인 기능을 하는 것이 아닌 단순 폼을 만들어주었다.

## p 태그

paragraph(문단)의 약자로, 하나의 문단을 표현하기 위하여 사용한다.

## <h1>, <h2>, <h3>, <h4>, <h5>, <h6>의 차이

```html
<!DOCTYPE html>
<html lan="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE-Edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Heading1</h1>
    <h2>Heading2</h2>
    <h3>Heading3</h3>
    <h4>Heading4</h4>
    <h5>Heading5</h5>
    <h6>Heading6</h6>
  </body>
</html>
```

![](https://blog.kakaocdn.net/dn/mt7Yo/btrkAuPhzNE/OkxaPnOu9JkgzmuKxBdyh1/img.png)

숫자가 붙어있으니 당연하게도 순서에 맞게 써주어야 한다.

문서의 구조와 밀접한 관계가 있으며 크기와 글자의 굵기 등에도 관계가 있음.

## HTML5 semantic tag(시멘틱 태그)

일반적으로 semantic의 뜻은 "의미의, 의미론적인" 이다.

⇒ semantic tag: 개발자와 브라우저에게 의미있는 태그.

예를 들어, div나 span은 non-semantic 태그라고 할 수 있고, table, article 등의 tag는 semantic 태그라고 볼 수 있다.

div나 span태그만 보고 이게 어떤 내용이 들어가는 지 알 수 없다.

하지만 table을 보면 표가 들어간다는 것을 알 수 있고, article을 보면 어떠한 형태의 글이 들어갈 것이라는 걸 알 수 있다.

✷ HTML5에서의 시멘틱 요소

|    태그    |                                                                                                                                            설명                                                                                                                                             |
| :--------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  article   |                                                                                               해당 문서나 페이지 또는 사이트와는 완전히 독립적으로 구성할 수 있는 요소를 정의할 때 사용한다.                                                                                                |
|   aside    |                                                                                                           페이지 콘텐츠를 제외한 콘텐츠를 정의한다. 링크, 광고, 사이드바 표시 등.                                                                                                           |
|  details   |                                                                                                                   사용자가 보거나 숨길 수있는 추가 세부 정보를 정의한다.                                                                                                                    |
|  summary   |                                                                                                                       details요소를 위해 눈에 보이는 제목을 정의한다.                                                                                                                       |
|   figure   |                                                                                                    일러스트레이션, 다이어그램, 사진, 코드 목록 등과 같은 자체 포함 된 콘텐츠를 지정한다.                                                                                                    |
| figcaption |                                                                                                                             figure 요소에 대한 캡션을 정의한다.                                                                                                                             |
|   footer   |                                                                          문서 또는 섹션의 바닥글을 지정한다. 주로 저작권, 연락처 정보 등 내용이 삽입되며 <header>, <section>, <article> 등 다른 레이아웃 사용가능.                                                                          |
|   header   | 문서나 섹션의 머릿글을 지정한다. 사이트 맨 위쪽이나 왼쪽에 사용하며 헤더 안에 <form> 태그를 이용, 검색창을 넣거나 <nav>태그를 이용해 사이트메뉴를 넣는다.즉, 도입부에 해당하는 콘텐츠나 네비게이션 링크의 집합 등과 같은 정보를 포함, HTML 문서는 여러 개의 <header> 요소를 포함할 수 있다. |
|  section   |                                  <header>, <footer>와 함께 문서의 구역을 정의한다. 웹 페이지의 큰 의미 단위가 될 수 있는 어떤 것이든 묶어서 하나의 구역을 구분하는데 사용한다. <section>안에 <section>을 넣을 수도 있고, <article>을 이용해 내용을 넣는다.                                  |
|    nav     |                                                                                     네비게이션 링크를 정의한다. 같은 사이트 내의 링크나 다른 사이트로의 링크들의 모음이다. 문서의 주요 내용을 지정한다.                                                                                     |
|    main    |                                                                                                                                문서의 주요 내용을 지정한다.                                                                                                                                 |
|    mark    |                                                                                                             강조표시된 텍스트를 정의한다. 형광펜을 칠한 것처럼 노랗게 칠해진다.                                                                                                             |
|    time    |                                                                                                                                   날짜 / 시간을 정의한다.                                                                                                                                   |
|     hn     |                          각 웹 콘텐츠 영역에서 제목을 표시할 때 사용하는 태그. <h1>은 페이지 당 단 한 번만 사용하는 것이 권장된다. 웹표준에서는 <hn>을 사용해 제목을 표시해야 하며, 단순 크기를 키우거나 굵게 표시하고 싶다는 이유로 이 태그를 쓰는 것은 금지된다.                          |
|   hgroup   |                                                                                                            의미는 없지만 제목과 부제목을 묶는 용도. 가독성 향상을 위해 사용한다.                                                                                                            |
|  address   |                                                  웹페이지 저작자의 이름이나 제작자의 웹페이지, 피드백을 위한 이메일주소 등의 연락처 주소를 넣기 위한 태그. 하지만 실제 우편물 주소를 넣는 것은 아니다. - 실제 우편물 주소에는 <p>를 쓴다.                                                   |
