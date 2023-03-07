---
layout: single
title: "vs code의 code 명령어 영구적용하기"
categories: Information
author_profile: false
---

mac 터미널에서 vs code를 여는 'code .' 명령어 영구적용시키기

## 개요

터미널에서 vs code를 열 때 code . 명령어를 사용하면 바로 vs code로 열 수 있는데, 이게 매번 초기화가 되어 여간 불편한 게 아니다. 그러던 중, 터미널에 영구적으로 적용할 수 있는 방법을 알게 되어 적어보게 되었다.

## 해결 방법

- zsh인지 bash인지 알아야하는데, 대부분 m1 이상의 터미널은 zsh인 것으로 알고 있다.

```
nano ~/.zhsrc
code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
source ~/.zshrc
```

nano 에디터(vim 에디터도 상관없음. 본인에게 편한 에디터)를 열어 코드를 추가한 후, 저장한다.

그리고 변경된 .zshrc 파일을 source 명령어를 통해 한 번 실행시킨다.

## code . 명령어

vs code에 먼저 code 명령어를 입력시켜주어야 하는데, 일단 vs code를 열어준다.

그 다음 command + shift + p로 쉘을 열어 shell command : install 'code' command in PATH를 클릭해주면 vs code가 알아서 해당 명령어를 등록해준다.
