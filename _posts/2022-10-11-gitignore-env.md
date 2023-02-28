---
layout: single
title: "[Git] .gitignore에 .env 파일을 추가해도 그대로 올라가는 경우"
categories: Git
tag: [기록, git, 깃]
author_profile: false
---

.gitignore에 .env 파일을 추가하는데 그대로 git에 올라가는 경우

## 개요

보통은 .gitignore 파일에 .env 파일을 작성해두면 환경변수가 깃에 올라가지 않지만, 그렇지 않을 때가 있다.

그런 경우를 위해 어떻게 할 수 있는지 작성해보았다.

## 첫번째

[reference(1)](https://velog.io/@hoje15v/.gitignore%EC%97%90-.env-%ED%8C%8C%EC%9D%BC-%EC%98%AC%EB%A0%A4%EB%8F%84-git%EC%97%90-%EC%98%AC%EB%9D%BC%EA%B0%88-%EB%95%8C)

[reference(2)](https://stackoverflow.com/questions/38983153/git-ignore-env-files-not-working)

```
git rm --cached -r .env
git add .
git commit -m "remove .env file from git"
git push
```

## 두번째

[(reference-from inflearn)](https://www.inflearn.com/questions/371108)

```
① .gitignore에서 .env라는 코드를 삭제 (이때부터 .env파일 git으로 추적 다시 시작)
② .env 파일 삭제
③ 커밋 및 푸시 (이러면 원격 저장소에 .env가 사라지겠죠)
④ .env 파일 되살리기
⑤ 다시 .gitignore에 .env 라는 코드 추가
```
