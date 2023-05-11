---
layout: single
title: "깃헙 블로그 포스팅이 되지 않을 때 해결 방법"
categories: Information
author_profile: false
---

블로그 포스팅이 올라가지 않을 때 해결 방법.

## 개요

깃헙 블로그를 새로 만들어 기존 블로그 글들을 옮기고, 새로운 포스팅을 올리던 중 build가 제대로 되고 있음에도 불구하고 포스팅은 제대로 올라가지 않았다.

pull request나 deploy 과정에서 뭔가 잘못되었을까 싶어 살펴보았지만 제대로 동작하고 있었다.

## 해결방법

### 1. 기본 항목들이 지켜졌는지 살펴보기.

기본 항목들이라 함은, 다음을 의미한다.

- [x] YEAR-MONTH-DAY-title.md 파일 형식과 포스팅 날짜를 확인한다.

ex) 2023-04-26-글제목.md

- [x] \_post 폴더에 맞게 위치했는지 확인한다(포스팅 파일이 들어갈 폴더 안에 해당 파일이 있는지 확인한다).

- [x] 해당 카테고리가 존재하는지, 카테고리에 맞게 작성했는지 확인한다.

### 2. 하기 항목들을 하나씩 해보기.

- [x] \_config.yml 파일 내 timezone 옵션을

```
timezone: Asia/Seoul
```

으로 변경해준다.

- [x] \_config.yml 파일 안에 있는 masthead_title 바로 아래 줄에

```
future: true
```

코드를 추가하여 push-pull request-merge한다(이 방법으로 해결했다).

- [ ] 포스팅 파일에 published: true 옵션을 명시한다.

- [ ] index.html 파일에 공백 등을 추가하여 변경 사항을 만들고, push 해본다.

- [ ] jekyll build --verbose 명령어를 통해 skipping 된 것이 있는 지 확인해본다.

### 3. 옵션에 대한 설명

#### ① timezone: Asia/Seoul

jekyll blog의 timezone 옵션의 기본값은 null이다.

이 timezone을 한국 시간으로 맞춰 놓아 해결할 수 있었다고 했다. 하지만 나는 이미 해당 옵션을 사용 중이었고, 포스팅이 잘 되다가 되지 않았다.

#### ② future: true

해당 옵션은 미래의 포스팅을 보이게 해준다.

지킬의 timezone 설정과 로컬의 timezone 설정이 맞지 않는 등 모종의 이유로 인해 포스팅 시간이 지킬 기준의 '미래의 포스팅' 이 된다면 보이지 않게 된다.

(그 이유로 인해 항상 업로드 날짜를 현재 날짜의 전일로 기재하여 업로드 하는 것인데, 잘 되다가 안되는 이유까지는 알아내지 못했다ㅠㅠ)

그래서 업로드가 되지 않는 이유일까 싶어 미래의 포스팅이 보일 수 있도록 해주었다. 해당 방법으로 해결할 수 있었다.

#### ③ published: true

말 그대로 포스팅의 공개/비공개 여부 설정이다.

원래는 따로 옵션을 설정하지 않으면(기재하지 않으면) 공개가 기본 옵션인데, future 옵션이 되지 않을 경우를 대비하여 작성해보았다.

#### ④ 변경 사항을 만들어 push 하기

이미 첫번째 방법으로 해결을 해서 시도해보지는 않았지만, 이 방법은 어떻게든 변경사항을 만들어 staging area에 올린 다음 push하는 방법이다.

구글링을 통해 해당 방법으로 해결한 사람들이 있다고 하여 올려보았다.

### 4. 마무리 및 참고 자료

이런 이유에서인가, 하는 추측은 있지만 정확히 왜 되지 않는지에 대한 이유는 알아내지 못해서 조금 아쉽다.

오랜만에 블로그에 글을 작성하려다 발견된 문제에 대해 해결할 수 있었고, 그 과정을 글로 올릴 수 있어 기분이 좋다.

- [github-pages-are-not-updating](https://stackoverflow.com/questions/20422279/github-pages-are-not-updating)
- [지킬 블로그 문서](https://jekyllrb-ko.github.io/docs/configuration/default/)
