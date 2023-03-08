---
layout: single
title: "jekyll blog 글자 및 형광펜 색상 변경하기"
categories: Information
author_profile: false
---

jekyll blog 글자, 형광펜 색상 변경하는 방법

## 개요

블로그를 쓰다보니 글자 색상을 바꾸어야할 때도 있고, 형광펜의 기본 색상 외에도 다른 색상을 써야할 때가 있는데 어떻게 해야할 지 잘 몰라 찾아보고 정리해보게 되었다.

## 글자 색상

font 태그를 사용하여 color 속성을 넣을 수 있다.

직접 색상명을 넣을 수도 있고, hex code를 넣을 수도 있다.

<font color="blue">파랑</font>

<font color="1E90FF">연파랑</font>

```
<font color="blue">파랑</font>
<font color="1E90FF">연파랑</font>
```

## 형광펜 색상

실제 하이라이트의 기본 색상은 노랑색이다.

만약 색상을 바꾸고 싶다면 mark 태그 안에 style="background-color: blue" 등의 방법으로 바꿀 수 있다.

그 중 내가 가장 많이 쓰고, 선호하는 색상의 예시를 적어본다.

<mark style='background-color: #ffdce0'>연빨강</mark>

```
<mark style='background-color: #ffdce0'>연빨강</mark>
```

<mark style='background-color: #fff5b1'>연노랑</mark>

```
<mark style='background-color: #fff5b1'>연노랑</mark>
```

<mark style='background-color: #dcffe4'>연초록</mark>

```
<mark style='background-color: #dcffe4'>연초록</mark>
```

<mark style="background-color: #F6B4C1">분홍색</mark>

```
<mark style="background-color: #F6B4C1">분홍색</mark>
```
