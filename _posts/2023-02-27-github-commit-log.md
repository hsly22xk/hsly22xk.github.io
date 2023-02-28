---
layout: single
title: "깃헙 블로그 커밋 기록 남기기"
categories: Github-Blog
tag: [기록, 깃헙블로그, 커밋기록남기기, 잔디심기]
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar:
  nav: "docs"
---

깃헙 블로그 생성 후 커밋 기록 남기기(잔디심기) 내용 정리글입니다.

## 개요

깃헙 블로그를 만들고 커밋 기록 남기기, 일명 잔디심기가 되지 않는다는 것을 알게 되었습니다.

테디노트님의 라이브 강의를 듣던 중 나왔던 질문이었지만, 시간 관계상 자세한 설명을 듣지 못하여 유튜브 영상을 보고 직접 해본 후 정리한 내용입니다.

## branch 생성 및 전환

```
git checkout -b branch name
git switch -c branch name
```

chekcout -b 나 switch -c 명령어를 사용하여 브랜치를 새로 만들고 전환해준다.

-b 혹은 -c 옵션을 붙여야 브랜치를 만들고 전환하는 것까지 가능해진다. 단순 브랜치 전환만 하고 싶다면 옵션을 붙이지 않아도 된다.

## git push

블로그 글을 작성하고 저장했다면,

```
git status
git add .
git commit -m "commit message"
git push origin branch name
```

과정을 차례대로 해준다.

여기서 git push를 해줄 때, 내가 만들어준 branch name에 push를 해준다.

## pull request

깃헙에 들어가 pull request를 해준다.

New pull request 버튼을 눌러주면
![스크린샷 2023-02-28 오후 6 04 21](https://user-images.githubusercontent.com/91467260/221805164-eded44c9-b96b-44eb-837b-3751f00c57d3.png)
해당 사진처럼 나오게 되는데, 여기서 주의할 점은 base repository와 head repository 부분이다.

먼저, head repository의 branch가 어디인지를 보아야하고, 그 다음엔 base repository가 내 repository로 되어있는지 봐야한다.

나의 경우 레포지토리를 포크해서 클론해온 상태이기 때문에, 다른 사람 레포지토리 주소로 pr을 넣으면 안된다...(물론 넣는다고해서 바로 merge되진 않지만 그래도 주의할 것!)

제대로 설정되었다면 Create pull request 버튼을 클릭해준다.

## commit and merge

클릭 후, Title을 작성해준 후 comment를 작성해준다(comment 작성은 옵션).

Create pull request - merge까지 해주면 끝!
