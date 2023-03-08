---
layout: single
title: "D+16 CSS 중급"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

CSS의 전반적인 설명(2).

## 1. CSS Selector

‣ 셀렉터: 말 그대로 선택을 해주는 요소를 의미하며, 특정 요소들을 선택하여 스타일을 적용할 수 있다.

ex)

```css
p {
  color: red;
  padding: 6px;
}
```

에서 p는 선택자이다.

h2 {}

div {}

- 전체 셀렉터

- {} // 문서의 모든 요소를 선택할 때 사용

- 태그 셀렉터

section, h1 {} // 문서의 특정태그를 선택자로 태그명을 사용

- id 셀렉터

#only {} // 요소에 id속성, id이름을 생성하고 id이름을 선택자로 사용한다.

- class 셀렉터

.widget {} // 요소에 클래스 속성, 클래스 이름을 생성하고 클래스 이름을 선택자로 사용한다.

.center {} // 클래스 이름은 서로 다른 요소에서 중복 사용할 수 있고 하나의 요소에 2개 이상 적용할 수 있다.

✅ .show#only와 .show #only의 차이

.show#only는 class가 show이면서 id가 only인 엘리먼트(둘 다 가진 엘리먼트)를 가져오는 셀렉터이고,

.show #only는 show class를 가진 엘리먼트 안에 들어있는 only라는 id를 가진 엘리먼트를 찾아오는 셀렉터이다.

✷ vs code에 ! 치면 html 파일 형식 나오는것 → 에밋: 플러그인의 한 종류

① 후손셀렉터와 자식셀렉터의 차이

본인 하위의 값을 선택한다는 점에서 의미는 같지만 약간의 차이가 있다.

우선 제일 상위에 속하는 요소를 부모 요소, 그 하위에 속하는 요소를 자손 요소(자식 요소)라고 한다.

그 자손 요소에서 더 하위에 속하는 요소는 후손 요소(하위 요소)라고 한다.

후손 셀렉터: 지정된 셀렉터의 하위에 위치하는 선택자를 선택한다. header h1{} // 그냥 쭉 이어쓴다.
자식 셀렉터: 지정된 셀렉터의 모든 자식 요소들 중에서도 지정된 자식 선택자만 선택한다.

header > p { } // > 기호를 이용하여 선택한다.

![](https://blog.kakaocdn.net/dn/cws5Fb/btriizS26mZ/KUgocztENvK4cEBNI8SOX1/img.png)

div 태그 닫는 위치에 따라 자식이나 후손이 아닌 형제들이 될 수 있다. 닫는 태그의 위치도 정확하게 알고 써줄 것.

ex)

```html
<div class = 'parent'></div>
<div class = 'child'></div>
<div class = 'greatGrandchild></div>
```

②형제 셀렉터와 인접 형제 셀렉터

- 형제 셀렉터: ~ 기호를 사용함. 지정된 셀렉터의 형제 요소 중 그 셀렉터 뒤에 위치하는 셀렉터 요소를 모두 선택함.

```
section ~ p { }
```

- 인접 형제 셀렉터: 인접 형제 선택자는 + 기호를 사용함. 지정된 셀렉터의 형제 요소중 셀렉터 바로 뒤에 위치하는 셀렉터의 요소를 선택한다. 그 사이에 다른 요소가 존재하면 선택되지 않음.

```
section + p { }
```

③ 가상 클래스 -선택자 뒤에 :가상이벤트를 붙이면 특정 이벤트마다 적용 할 스타일을 설정 할 수 있다.

```
-a: link {} // 방문한 적이 없는 링크
-a: visited {} // 방문한 적 있는 링크
-a: hover {} // 마우스를 롤오버 했을 때(마우스를 위에 올려놓은 상태)
-a: active {} // 마우스를 클릭했을 때
-a: focus {} // 포커스를 가질 때
```

④ 요소 상태 셀렉터

\*라디오 버튼과 체크박스를 생각하면 셀렉터가 체크되거나 사용 가능한 상태라는 말이 조금 이해가 된다.

```
-input:checked + span {} // 셀렉터가 체크된 상태일 때
-input:enabled + span {} // 셀렉터가 사용 가능한 상태일 때
-input:disabled + span {} // 셀렉터가 사용 불가능한 상태일 때
```

⑤ 부정 셀렉터-요소:not(selector) { style properties }. 선택자가 아닌 모든 요소에 전부 다 적용한다.

```
-input:not[type="password"]) { }
-div:not(:nth-of-type(2)) { }
```

⑥ 정합성 확인 셀렉터

```
-input[type="text"]:valid { } // 정합성 검증이 성공한 input 요소 또는 form 요소를 선택한다.
-input[type="text"]:invalid { } // 정합성 검증이 실패한 input 요소 또는 form 요소를 선택한다.
```

ex)
![](https://blog.kakaocdn.net/dn/zeBvm/btripGb1PKY/xJaZW5Ecd2plrAulDKrrIK/img.png)

이메일 검사를 한다고 했을 때 제대로 된 이메일 형식을 넣었다면 정합성 검증이 성공한 input요소가 되었고, 제대로 되지 않은 이메일 형식을 넣었다면 검증이 실패한 input요소가 되었다.

![](https://blog.kakaocdn.net/dn/qymkz/btrikMrrQjX/QvgUFvI6XtrP4Jv68QnT2k/img.png)

실제 결과물은 이렇게 나온다.

- 구조 가상 클래스 셀렉터

-p:first-child {} // 셀렉터에 해당하는 모든 요소 중 **<mark>첫번째 자식인 요소만 선택</mark>**

-ul > li:last-child {} // 셀렉터에 해당하는 모든 요소 중 **<mark>마지막 자식인 요소만 선택</mark>**

-ul > li:nth-child(n) {} //셀렉터에 해당하는 모든 요소 중 **<mark>앞에서 n번째 자식인 요소 선택</mark>**

-div:nth-last-child(n) {} // 셀렉터에 해당하는 모든 요소 중 **<mark>뒤에서 n번째 자식인 요소 선택</mark>**

-p:first-of-type {} // 셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 **<mark>처음 등장하는 요소 모두 선택</mark>**

-div:last-of-type {} // 셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 **<mark>마지막에 등장하는 요소 모두 선택</mark>**

-ul:nth-of-type(n) {} // 셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 **<mark>앞에서 n번째에 등장하는 요소 선택</mark>**

-p:nth-last-of-type(n) // 셀렉터에 해당하는 요소의 부모요소의 자식요소 중 **<mark>뒤에서 n번째에 등장하는 요소 선택</mark>**

n은 0부터 시작되는 정수이다.

|  n  |                     2n+1                     | 2n-1 | 3n-2 | 3n+1 | -n+5 |
| :-: | :------------------------------------------: | :--: | :--: | :--: | :--: |
|  0  |                      1                       |  -1  |  -2  |  1   |  5   |
|  1  |                      3                       |  1   |  1   |  4   |  4   |
|  2  |                      5                       |  3   |  4   |  7   |  3   |
|  3  |                      7                       |  5   |  7   |  10  |  2   |
|  4  |                      9                       |  7   |  10  |  13  |  1   |
|  5  |                      11                      |  9   |  13  |  16  |  0   |
|  x  | 자식 엘리먼트 중 홀수번째 자식 엘리먼트 선택 |      |      |      |      |

0과 음수는 생략되기 때문에 2n+1과 2n-1, 3n-2와 3n+1은 결과적으로 같은 수열을 생성한다.

-section > p:nth-child(2n+1) {}

-ul > li:first-child {}

-li:last-child {}

-div > div:nth-child(n) {}

-section > p:nth-last-child(2n+1) {}

## 2. 수직 분할과 수평 분할

① 수직분할: 화면을 수직으로 구분하여 콘텐츠가 가로로 배치될 수 있도록 요소를 배치한다.

② 수평분할: 분할된 각각의 요소를 수평으로 구분하여 내부 콘텐츠가 세로로 배치될 수 있도록 요소를 배치한다.

✷ 수평으로 구분된 요소에 height속성을 추가하면 수평분할을 보다 직관적으로 할 수 있다.

![](https://blog.kakaocdn.net/dn/6lPD2/btrio1tZiK8/tXKE0K7ncy9hFXJFDN9pI0/img.png)
(실제 vs code를 추상화 시킨 그림)

![](https://blog.kakaocdn.net/dn/bxUgyO/btrl01dPvOX/Sro10zY56GROLzfNu4RU3K/img.png)
(vs code clone coding HTML 구조)

![](https://blog.kakaocdn.net/dn/nqU8v/btrl4RH1F9Z/7O3kVdQFNujMdjTWoG1SSK/img.png)

✷ min-height: 최소 높이를 지정함

![](https://blog.kakaocdn.net/dn/ssFz0/btrlZekc3GT/4Y0tKdT91uaTbtvGrnys5K/img.png)

![](https://blog.kakaocdn.net/dn/bA2IwO/btrl0Z76OM8/Bo8wnNqnjMcZq6KCv07Dx1/img.png)

![](https://blog.kakaocdn.net/dn/nM2cb/btrl00eUUU7/hta4qffKZzMgx9TYViDQWk/img.png)

✷ Atomic CSS 방법론: 위의 사진과 같이 클래스 이름과 구현을 1:1로 일치시켜 아주 작은 단위로 CSS를 작성하는 기법

## 3. 레이아웃 리셋

HTML문서는 기본적인 스타일을 가지고 있지만, 때로는 이 기본적인 스타일이 레이아웃을 잡을 때 방해가 되기도 한다.

ex)

> 박스의 시작을 정확히 (0,0)의 위치에서 시작하고 싶은데, <body> 태그가 가진 기본 스타일에 약간의 여백이 있다.
>
> width, height 계산이 여백을 포함하지 않아 계산에 어려움이 있다.(박스 크기 측정 기준(box-sizing))
>
> 브라우저(크롬, 사파리 등)마다 여백이나 글꼴과 같은 기본 스타일이 조금씩 다르다.

같은 식이다.

![](https://blog.kakaocdn.net/dn/b1iVbP/btrisLjDknO/SMI5vWZowfcm2sh9WTHkC1/img.png)
(기본 스타일링을 제거하는 CSS 작성 예시)

![](https://blog.kakaocdn.net/dn/brEVxz/btrl0ahLVhH/jf6N2ojVy8fwnCg1Jrh3WK/img.png)

## 4. Flexbox로 레이아웃 잡기

flexbox로 레이아웃을 구성한다는 것은 박스를 유연하게 늘리거나 줄여 레이아웃을 잡는 방법이다.

① display: flex

부모 박스요소에 display: flex를 적용해, 자식 박스의 방향과 크기를 결정하는 레이아웃 구성방법.

기본값으로 display: flex가 적용된 부모 박스의 자식 요소는 왼쪽부터 차례대로 이어 배치된다.

![](https://blog.kakaocdn.net/dn/biXUi8/btrisLDWsPR/2focHnOYeP5FYsKrx4Ep5K/img.png)
(display: flex를 설명하기 위해 작성한 HTML 문서)

![](https://blog.kakaocdn.net/dn/d9KuFA/btrim6QzXjY/HpLvkugl1ozfIzsLlKq4dK/img.png)
(HTML을 기준으로 만든 display: flex CSS 작성 예시)

![](https://blog.kakaocdn.net/dn/bytbjp/btrio2Nef6b/SzlEL0RoeNsWarAdF7ZWLK/img.png)
(적용 결과)

이처럼 display: flex가 적용된 빨간 박스 내의 자식요소는 왼쪽부터 차례대로 배치된다.

자식 박스에 어떠한 속성도 주지 않으면 왼쪽에서부터 오른쪽으로 콘텐츠의 크기만큼 배치된다.

✷ 주의사항

- display 속성에 flex를 적용하는 것은 부모 요소에 적용한다(display: flex)

- 자식 요소는 flex라는 속성에 값을 적용한다(flex: 0 1 auto)

// 자식요소에 flex 속성을 추가하지 않으면 적용되는 기본값

② flex요소에 방향 지정하기

flexbox는 박스가 수직 분할되는 것이 기본값이지만 방향을 설정해주면 수평으로도 분할할 수 있다.

flex-direction 속성: 부모 박스요소에 적용한다. 자식 박스에 특별한 속성을 주지 않아도 부모 요소에 의해 자식 요소가 영향을 받는다.

✅ 주요 속성

‣ row(기본 속성) : row일 때 주축(main axis)은 가로축이 된다. 왼쪽에서 오른쪽 기준

‣ row-reverse: row와 반대. 오른쪽에서 왼쪽으로.

‣ column: column일 때 주축과 교차축은 서로 바뀐다. 위에서 아래

‣ column-reverse: column과 반대. 아래서 위로.

✷ 교차축(cross axis): 여러 개의 주축과 수직을 이루는 방향이다. 주축이 가로일 때 교차축(cross axis)은 세로가 된다.

![](https://blog.kakaocdn.net/dn/plRBs/btrinrG2i4q/KooFjMRTHOMZlTI9HLlBZk/img.png)
(주축과 교차축을 설명하기 위한 그림. 초록색 네모는 부모 박스 안에 들어있는 자식 박스(아이템)들.)

- 축을 기준으로 정렬할 수 있는 속성들

‣ 콘텐츠 수평 정렬(justify-content): 주축을 기준으로 정렬한다. 부모 박스에 justify-content 속성을 적용하면 자식 박스를 수평으로 정렬할 수 있다.

- 주요 속성

```
flex-start: 아이템들을 시작점으로 정렬한다.
flex-direction이 row(가로 배치)일 때는 왼쪽, column(세로 배치)일 때는 위.
flex-end: 아이템들을 끝점으로 정렬한다.
flex-direction이 row(가로 배치)일 때는 오른쪽, column(세로 배치)일 때는 아래.
center: 아이템들을 가운데로 정렬한다.
space-between: 아이템들의 사이(between)에 균일한 간격을 만들어준다.
```

‣ 콘텐츠 수직 정렬(align-items): 교차축을 기준으로 정렬한다.

부모 박스에 align-items 속성을 적용하면 자식 박스를 수직으로 정렬할 수 있다.

- 주요 속성

```
flex-start: 아이템들을 시작점으로 정렬한다.
flex-direction이 row(가로 배치)일 때는 위, column(세로 배치)일 때는 왼쪽.
flex-end: 아이템들을 끝점으로 정렬한다.
flex-direction이 row(가로 배치)일 때는 아래, column(세로 배치)일 때는 오른쪽.
center: 아이템들을 가운데로 정렬한다.
stretch(기본값): 아이템들이 수직축 방향으로 끝까지 쭉 늘어난다.
```

③ flex의 하위 속성

- flex 속성에 적용되는 세 가지는 기본 크기를 바탕으로 필요에 따라 늘리거나 줄일 수 있는 값이 적용된다.

- grow, shrink 속성은 단위가 없고, 비율에 따라 결과가 달라진다.

✷ 기본값 세 가지

```
flex-grow: 0;
flex-shrink: 1;
flex-basis: auto;
```

‣ flex-grow(팽창 지수): 자식 박스가 얼만큼 늘어날 수 있을지 알아본다.

![](https://blog.kakaocdn.net/dn/u8CMg/btrijSZcLNk/ciH6KFFHZJQzkvIcMnpnh1/img.png)
![](https://blog.kakaocdn.net/dn/bBiZzc/btrioGwtWLg/waYRbxNt14Jm3YvcI9Mrx1/img.png)
![](https://blog.kakaocdn.net/dn/bp8ROx/btrikMLStK8/asqFkwjHhgKue8kUoGbSs1/img.png)

위의 경우에는 target클래스만 가졌을 때 flex-grow속성을 1로 했다면, 이제 box클래스도 똑같이 flex-grow속성을 1로 주었다.

box 클래스의 flex-grow는 기본값인 0이다.

만약 box 클래스의 flex-grow 속성에 값을 1로 설정하면 모든 박스가 늘어나려고(grow) 한다.

결과적으로 모든 박스가 동일한 비율로 가로 길이가 늘어난다(총 grow 값 1+1+1, 각 박스는 1/3씩 크기를 가짐).

⇒ 모든 자식 박스의 flex-grow 속성이 0보다 큰 값을 동일하게 가지는 경우, 각 박스의 가로 길이는 동일한 비율을 가진다.

‣ flex-shrink(수축 지수): 자식 박스는 얼마나 줄어들 수 있을까?

: shrink는 설정한 비율만큼 박스가 작아진다. 그러나 grow와 shrink를 같이 쓰는 것은 권장하지 않는다.

flex-shrink 속성은 width나 flex-basis 속성에 따른 비율이므로 실제 크기를 예측하기가 어렵기 때문이다.

✷ 비율로 레이아웃을 지정할 경우

flex-grow 속성 또는 flex: 1 auto와 같이 grow 속성에 변화를 주는 방식을 권장한다.

flex-grow 속성으로 비율을 변경하는 경우, flex-shrink 속성은 기본값인 1로 둬도 된다.

‣flex-basis(기본값): 이 박스의 기본 크기는 얼마인가?

: 자식 박스가 grow나 shrink를 통해 늘어나고 줄어들기 전 기본값을 말한다.

flex-grow가 0일 때만 basis 크기를 지정하면 그 크기는 유지된다.

flex-grow 속성의 값이 1 이상인 경우, flex-basis 속성에 적용한 값보다 커질 수도 있다.

✅ 참고

```
width와 flex-basis를 동시에 적용하면 flex-basis가 먼저다.
콘텐츠가 많아 자식 박스가 넘치면 width가 정확한 크기를 보장하지 않는다.
flex-basis를 사용하지 않고 콘텐츠가 많아 자식 박스가 넘치는 경우를 대비해 width 대신 max-width를 쓸 수 있다.
```

## 5. 와이어프레임(Wireframe)

웹 또는 앱을 개발할 때 레이아웃의 뼈대를 그리는 단계.

단순한 선이나, 도형으로 웹이나 앱의 인터페이스를 시각적으로 묘사한 것. 레이아웃과 제품의 구조를 보여주는 용도.

## 목업(Mock-up)

보통 목업이라고 하면 실물 제품을 얘기하는 것이지만, 실제 실물이 없는 웹이나 앱에서는 실제로 작동하는 모습과 동일하게 HTML 문서를 작성한다.

예를 들어, 트윗 작성자, 트윗 내용, 작성한 날짜 등을 HTML 문서 내에 하드코딩하는 방식이다.

✷ 하드코딩

실제로는 변수와 함수를 사용하여 간단하게 작업할 수 있지만, 아직 div태그 내에서 함수를 전달하는 방식을 배우지 않았기 때문에 하나하나 클래스명과 해당하는 내용을 전부 써주어야한다. 일일이 모든 것을 다 적는다는 의미로 받아들였다.

![](https://blog.kakaocdn.net/dn/cyJ0Jz/btrl3KJso5m/fz7zFNiXtGW0sbkoDEJhd0/img.png)

## 7. HTML로 웹 앱의 구조잡기

- 마크업 언어: 태그 등을 사용하여 문서나 데이터의 구조를 명기하는 언어

① 큰 틀에서 영역 나누기

페이지를 보고, 어떤 영역으로 나눌 수 있는지 알아본다.

② 각 영역을 태그로 나누기

영역을 나누었다면, 그 영역의 태그의 구성요소를 알아본다.

여러 태그들을 하나의 태그로 감싸주어야 한다.

③ id 및 class를 목적에 맞게 사용하기

id: 전체 문서를 통틀어 단 하나, 고유한 이름을 붙일 때

class: 반복되는 영역을 유형별로 분류할 때

HTML문서에서는

```html
<div id="id">
  <li class="class"></li>
</div>
```

라고 썼지만 selector를 사용해서 쓰면

div#id, li.class라고 간단하게 쓸 수 있다.

id는 이름 앞에 #, class는 이름 앞에 .(dot) 을 붙인다.

⇒ 영역별로 알맞은 태그와 속성 붙이기

id와 class를 언제 쓰는 지 알았으니 이제 페이지의 영역별로 알맞은 태그와 그에 맞는 속성(id, class)을 붙여야 한다.

## display: grid;

flex와 같지만 쓰는 방식이 조금 다르다.

예를 들어

[grid-row](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row)

[grid-column](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column)

```css
.section1 {
  display: grid;
  grid-gap: 1em;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
}

.section1 > div {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
```

라고 쓰면

![](https://blog.kakaocdn.net/dn/bDJXRg/btrlQ1E8lNg/5fAOxHdKBCgNs0mo43jwD0/img.png)

이렇게 나타낼 수 있을 것 같다.

flex는 grow, shrink, basis에 따라 나누지만, grid는 오로지 column과 row에 따라 숫자를 나누게 된다.

```css
grid-template-columns: 1fr 1fr;
```

에서 1fr이라 함은 flex의 grow와 같다고 볼 수 있겠다.

1/2씩 나눠가진다, fr은 단위의 이름이라고 생각하면 쉬울 것 같다.

[grid-template-columns](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns)

[grid-template-rows](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows)
