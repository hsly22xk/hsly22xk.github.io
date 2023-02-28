---
layout: single
title: "[Git] 기존 프로젝트 github repository에 연결하기"
categories: Git
tag: [기록, git, 깃]
author_profile: false
---

(how to connect my own project in gihutb repository)

```
기존 프로젝트 폴더 안으로 진입
git init 으로 깃 저장소 초기화
git remote add origin 깃 저장소 주소
git remote -v 로 현재 리모트 주소 확인
git add . 로 새 레포지토리에 파일 업로드를 위해 스테이지에 파일 올리기
git status 로 현재 스테이징된 파일들 확인
git commit -m "커밋 메시지 내용" 으로 커밋
git push origin master 로 레포지토리에 파일 업로드
```

✷ git push -u origin master

: -u 옵션이 붙으면 다음부터는 git pull / push할 때 origin master를 지정하지 않아도

알아서 origin master로 붙어서 가져오라는 의미.
