---
layout: single
title: "jekyll blog 유튜브 영상 삽입하기"
categories: Information
author_profile: false
---

깃헙 블로그에 유튜브 영상 삽입하기.

## 개요

블로그 글을 정리하다보니 단순 블로그 링크나 이미지 삽입 뿐만 아니라 참고 영상 등으로 유튜브 영상을 삽입해야 할 경우가 있었다.

그런 경우를 위해 어떻게 유튜브 영상을 간단하게 삽입할 수 있는지에 대해 정리하여 적어보았다.

## 방법(1)

[mmistakes github blog link](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#youtube)

<img width="580" alt="스크린샷 2023-03-11 오전 12 02 49" src="https://user-images.githubusercontent.com/91467260/224349873-43f8666a-4517-4528-a4c9-8d68a40d9dbb.png">

해당 명령어를 블로그 글 안에 넣어주면 된다.

id의 경우

![스크린샷 2023-03-10 오후 11 56 31](https://user-images.githubusercontent.com/91467260/224348669-99d27736-8b2d-420f-beed-711eeee2ca2e.png)

사진에 나와있는, v= 뒤에 나와있는 부분을 넣어주면 된다.

## 방법(2)

간혹 id를 넣어줄 때 제대로 영상이 들어가지 않는 경우가 있다. 그럴 때는

![스크린샷 2023-03-11 오전 12 00 15](https://user-images.githubusercontent.com/91467260/224349241-7deab23e-2658-48a0-9673-da5fef3a01ee.png)
![스크린샷 2023-03-11 오전 12 00 33](https://user-images.githubusercontent.com/91467260/224349383-0b056960-c4c2-4b12-9fdc-6e04e53ca25c.png)

embed/ 뒤에 있는 id를 넣어주면 된다.

## 방법(3)

퍼가기에 있는 iframe 코드를 복붙해주어도 영상이 나온다.

## 결과

<iframe width="560" height="315" src="https://www.youtube.com/embed/1YAWshEGU6g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
