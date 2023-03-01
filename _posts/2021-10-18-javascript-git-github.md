---
layout: single
title: "D+14 git & github"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

git, github 관련 내용 정리.

## 1. 버전 관리 시스템(Version Control System)

이전에 작성한 내용을 보존해주는 시스템.

✷ 버전 관리 시스템의 필요성(버전 관리를 함으로서 얻을 수 있는 것)

① 코드를 수정한 뒤 에디터를 종료했다면 다시 실행한 텍스트 에디터에서 이전 코드로 돌아갈 수 없기 때문에 이전에 작성한 내용을 보존할 필요가 있다. 즉, 파일이 변경되면 변경 이력을 저장하고 이전 버전으로 돌아갈 수 있다.

⇒ 특정 시점에 Tag(꼬리표)를 달아 버전을 표시해주고, Branch(브랜치) 등으로 동시에 여러 버전을 개발할 수 있게 해준다(버전 관리).

② 변경 사항을 저장할 때는 어떤 사항이 변경되었는지 코멘트를 꼭 작성을 해야 하기 때문에 누가 어떤 파일을 추가, 수정, 삭제했는지도 확인이 가능하다(변경점 관리).

③ Git으로 관리되는 파일은 Github, GitLab, Bitbucket 등의 여러 가지 원격 저장소를 이용해서 백업과 협업을 할 수 있다.

⇒ 무언가 잘못 되었을 때 다시 특정 시점으로 돌아가게 해주고, 사고로 내용이 날아간 경우에도 복구할 수 있게 해준다(백업&복구).

⇒ 같이 일하는 사람들에게 수정사항을 쉽게 공유(협업)

## 2. Git과 Github

① Git: 개발자의 코드를 효율적으로 관리하기 위해서 개발된 분산형 버전 관리 시스템. 소스 코드 기록을 관리, 추적할 수 있는 버전 관리 시스템.

버전 관리 시스템은 하나하나 날짜별로 어떤 파일이 어떻게 변경되었는지 확인이 가능하다.

‣ 스냅샷: 특정 시점에 생성된 백업 복사본

‣ commit: 스냅샷을 만들어주는 작업. 파일 및 폴더의 추가/변경 사항을 저장소에 기록함.

⇒ 커밋 버튼을 누르면 이전 커밋 상태부터 현재 상태까지의 변경 이력이 기록된 커밋(혹은 리비전)이 만들어진다.

커밋은 시간순으로 저장된다. 최근 커밋부터 거슬러 올라가면 과거 변경 이력과 내용을 알 수 있다.

- 버그 수정, 기능 추가 등 의미 있는 업데이트를 작업 별로 구분해서 각각 커밋하면 나중에 이력을 보고 특정 변경 내용을 찾기 쉽다.

⇒ commit을 통해 변경 사항에 대한 스냅샷이 만들어지고 이전의 기록들에 대한 추적이 가능하다면 버전 관리뿐만 아니라 회사에서 협업을 할 때도 굉장히 유용하다.

⇒ Git에서는 소스 코드 변경 이력을 쉽게 확인할 수 있고, 특정 시점에 저장된 버전과 비교하거나 특정 시점으로 되돌아갈 수도 있다.

② Github: Git Repository를 관리할 수 있는 클라우드 기반 시스템. 내 컴퓨터에서 Git으로 관리하는 프로젝트를 올려둘 수 있는 사이트

⇒ Git으로 버전을 관리하는 폴더에 대해서 Github을 통해 여러 사람들이 공유하고 접근할 수 있는 것. 즉, 개발자의 SNS.

Github에서 Code Review 등을 통해 협업이 가능하고, 수많은 오픈 소스(소스 코드가 공개된 소프트웨어) 프로젝트들이 GitHub로부터 호스팅 되고 있어 누구든 자유롭게 기여(attribute, 기능을 추가하고 개선하는 것)가능.

## 3. Git 버전의 관리 기능 활용하기

‣ Git Repository: Git으로 관리되는 폴더. 파일이나 폴더를 저장해두는 곳.

- Remote Repository(원격 저장소): 작업한 코드를 업로드하여 여러 사람과 함께 공유할 때 쓰는 폴더.

- Local Repository(로컬 저장소): 내가 작업할 때 쓰는 폴더. 내 PC에 파일이 저장되는 개인 전용 저장소.

다른 사람의 Remote Repository에 올려놓은 소스코드를 나의 Local Repository로 가져올 수 있음.

- Fork: 프로젝트에 자유롭게 기여하기 위해 원격 저장소를 내 원격 저장소로 가져오는 작업의 과정.

- Clone: Fork 후 나의 Remote Repository에 코드를 옮겨온 상태에서 코드를 수정하기 위해 내 컴퓨터로 가져오는 작업.

- Push: 내 컴퓨터에서 소스코드 변경 작업 완료 후 변경 내용을 commit 하여 저장하고 Remote Repository에 반대로 올려주는 작업.

- 반대로 Remote Repository에서의 변경사항을 Local Repository로 가져오는 Pull 작업도 있다.

- Pull request: 내가 제안한 코드 변경사항에 대한 반영 여부 요청.

즉, 내가 Remote Repository에 Push 해 놓은 변경 사항에 대해서 함께 작업하는 다른 사람들에게 알리는 것.

![](https://blog.kakaocdn.net/dn/GuX3f/btrhWJ8hASL/1Myfkda8VS9Z9YMMfftK6k/img.png)

② 이 코드를 수정하기 위해서는 내 컴퓨터로 가져오는 작업을 한다. 내 컴퓨터에서 작업을 하기 위해서 clone을 한다.

- git clone: 명령어 뒤에 Repository 주소를 입력하면 해당 Repository를 내 컴퓨터(Local Repository)로 가져와서 작업할 수 있다.

③ 내 컴퓨터의 작업 공간(work space)에서 작업에 들어간 파일들을 git의 관리 하에 있는 상태로 올려줄 수 있는데, 이 영역을 staging area라고 한다.

staging area에 들어오지 않은 파일은 unstaged 혹은 untracked file이라고 말하며 staging area에 있는 파일들은 staged 된 파일이다.

✷ staging area가 정확하게 뭔지 이해가 안간다면 이렇게 생각하면 된다.

우리가 이사갈 때는 무빙 박스에 담고, 무엇이 들었는지 박스 겉면에 라벨링해준다.

이 무빙박스가 commit을 만들 수 있는 staging area, 라벨링 해주는 것이 commit이라고 생각하면 편하다.

④ staging area으로 파일들을 옮겨준다. staging area에 들어온 파일들은 commit이 가능하다.

commit을 하기 위해서 먼저 현재 Local Repository에 변경된 파일들이 어떤 것이 있는지 확인해 보려고 한다.

git status 명령어로 staging area와 untracked files(git의 트래킹 되고 있지 않은 파일들 / 관리되지 않는 파일들)목록에 어떤 게 있는지 확인할 수 있다.

여기서 알아둘 수 있는 명령어는

git add 파일명: 파일을 commit 할 수 있는 상태로 만들어 줌.

즉, git의 관리 하에 있는 staging area 로 파일들을 추가하는 명령어.

git add . : staging area에 unstaged 상태인 모든 파일을 한번에 추가할 수 있지만 이 명령어를 사용할 때는 올리지 말아야 할 파일까지 모두 add될 수 있기 때문에 주의할 것.

git restore 파일명: 변경사항을 폐기(discard changes) 하는 명령어.

처음 clone으로 받아왔던 코드 상태로 되돌리기 위한 명령어.

즉, commit 되지 않은 Local Repository의 변경사항을 폐기할 수 있다.

이처럼 git status 를 통해 어떤 파일이 어떤 상태에 있는지, 해당 파일에 대해 어떤 행동을 할 수 있는지 알 수 있다.

⑤ commit을 하고 나면 내 remote repository에 push 해서 commit 기록을 remote 에도 남겨줄 수 있다.

git commit -m '메시지 내용': commit 메시지를 작성하기 위해 -m 옵션을 통한 코멘트 작성.

- Commit 기록은 날짜, commit한 사람, commit 메시지가 모두 기록됨.

- 새로고침했더니 에러가 나서 방금 commit한 기록을 취소하고 에러를 수정하고 싶을 때,

아직 Remote Repository에 업로드 되지 않고 Local Repository에만 commit 해 놓은 기록이라면 reset 명령어를 통해서 commit 을 취소할 수 있다.

git reset HEAD^: 가장 최신의 commit 을 취소할 수 있다.

⑥ push를 완료한 후 이제 remote의 원래 레파지토리에 pull request(PR)를 보내면 Remote Repository로 내가 수정한 코드를 업로드할 수 있다.

git push origin branch: 내 Local Repository의 commit 기록들을 Remote Repository로 업로드하기 위해 사용하는 명령어.

- git push origin main, git push pair dev 등 git push 뒤에 따라오는 명령어는 상황에 따라 변경할 수 있다.

✷ origin과 upstream & downstream

‣ origin: 깃허브에 존재하는 repository, remote를 뜻하는 단어. 다만 remote에 origin이라는 이름을 붙인 것 뿐이다.

‣ upstream & downstream: 사실 어떤 것이 upstream이고, 어떤 것이 downstream이라고 확정지을 수 없었다.

쉽게 얘기하자면 pull 하는 주최가 downstream, 당하는 쪽이 upstream 이다. 만약 내 레포에서 다른 레포를 풀 해서 작업하고 있다면 다른 레포가 업스트림이 된다.

otherRepository(upstream) -> (git pull) myRepository(downstream)

‣ origin과 upstream의 차이점

보통 다른 repository를 fork해서 내 repository를 만들어놓고 내 repository를 clone, pull하여 작업한다.

이 때 가장 근본이 되는 repository를 upstream, 내가 fork해서 가져온 repository를 origin이라고 부른다.

그러므로 내가 로컬에 클론 해 놓고 작업할 때, origin/master에서 가져올지, upstream/master에서 가져와야 할지 생각해서 가져와야한다.

otherRepository(upstream) -> (fork) myRepository(origin)

otherRepository(upstream) -> (git pull) myRepository(local)

myRepository(origin) -> (git pull) myRepository(local)

✷ git branch 브랜치이름: 새로운 브랜치 작성 명령어

옵션을 지정하지 않고 branch 명령어를 실행하면 브랜치 목록 전체를 확인할 수 있다.

- branch: 프로그램 소스 버전을 관리하기 위한 개념, 간단히 말하면 복사본.

원본에서 가지치기해서 복사한 소스를 가지고 별도의 버전을 새로 생성하는 것.

- git branch -m 브랜치명 새로운 브랜치명: 마스터 브랜치명을 바꿀 때 사용하는 명령어.

git checkout: git을 사용할 때 커밋되지 않았거나 저장되지 않은 변경 사항이 나타나는 경우가 많다.

이 때 현재 로컬에서 작업한 사항이 없어서 전부 날려서 해결하고 싶은 때 사용하는 방법 중 하나. 모든 변경 사항을 취소.

git merge: 다른 브랜치를 현재 Checkout된 브랜치에 Merge(병합)하는 명령.

⑦ git log: 남긴 commit들이 잘 기록되었는지 확인하는 명령어.

현재까지 commit된 로그들은 터미널 창에서 확인 가능. 이 터미널 창을 종료하려면 q 입력.

- git diff 파일명: 파일 내에서 실제로 내가 무엇을 변경했는지 알려줌.

## 4. Git의 세 가지 영역 및 상태

![](https://blog.kakaocdn.net/dn/bpV4Gz/btrhUW8kXEX/n9npSIFAkiY1fFquW7gyAk/img.png)

Tracked area에 들어온 파일들만 Git의 관리를 받을 수 있으며, Tracked area 내부에서도 세 가지 상태로 나누어진다.

①Unmodified : 기존에 Commit했던 파일을 수정하지 않은 상태

②Modified : 기존에 Commit했던 파일을 수정한 상태(변경사항이 있는 것)

③Staged : commit이 가능한 상태. 수정한 파일을 commit 하기 위해서는 staged area에 add 하는 작업 필요.

- track: 추적, 즉 파일을 관리한다는 의미로 쓰인다.

Changes to be committed(커밋할 준비가 되어있는 파일들)라고 적혀 있는 초록색 파일은 staged 상태의 파일,

Changeds not staged for commit(커밋할 준비가 되어있지 않은 파일들)이라고 적혀 있는 빨간색 파일은 Modified 상태의 파일이다.

그래서 add 명령어를 통해 tracked area에 들어간 파일을 수정하게 되면 다시 modified 상태가 되기 때문에 다시 add하는 작업을 통해 파일을 staged 해 주는 작업이 필요하다.

## 5. 터미널로 macOS에서 git 설치하기와 git 환경설정

① 터미널로 git 설치하기

리눅스나 우분투라면 apt를 사용하여 설치해야 하지만, 맥은 그런 거 필요 없다.

터미널을 켜고 git 명령어 하나만 쳐주면 바로 설치 가능하다.

brew install git으로도 가능하다.

② git 환경설정

```
git config --global user.name "" // 깃에서 쓸 유저네임을 입력한다.
git config --global user.email "" // 깃에서 쓸 이메일을 입력한다.
git config --global core.editor nano

// Git에서 커밋 메시지를 기록할 때, 특히 merge commit 확인 메시지가 나올 때 쓸 에디터.

기본적으로는 vi가 나오지만 nano가 익숙하기 때문에 nano로 설정했다.

git config --list // 내가 설정해놓은 리스트를 나오게 하는 명령어
```

## 6. SSH 등록

① SSH(Secure SHell): 보안이 강화된 shell 접속.

CLI 환경에서 다른 PC에 접속하거나 요청할 때 사용, 비대칭키를 이용해 사용자 인증.

② SSH키 생성

ssh 키는 비대칭키로 구성되며, 이것은 두 개의 키가 서로 대칭이 되지 않는 형태로 존재한다.

```
ssh-keygen
```

명령어를 프롬프트에 입력하고, ssh 키 페어(쌍)를 생성한다.

명령어 입력 후 Enter키 3번이면, ssh 키 페어가 생성된다.

처음에 Enter file in which to~~~ 라고 나오는 문장에서 엔터 키 한 번,

바로 다음 문장에서 또 한 번, 마지막으로 그다음 문장에서 한 번.

\*ssh-keygen 명령어는 경로 ~/.ssh./ 에 두 파일 id_rsa 와 id_rsa.pub 를 생성한다.

이 두 파일은 ssh 키 페어라고 한다.

이 중 id_rsa.pub는 누구에게나 공개해도 되는 공개키(Public Key), id_rsa는 공개되면 안 되고 나만 보관하고 있어야 하는 키라고 하여 개인키(Private Key) 또는 비밀키(Secret Key)라고 함.

③ 공개 키 복사 후 깃헙에 등록하기

```
cat ~/.ssh/id_rsa.pub
```

명령어를 프롬프트에 입력하여 공개키를 복사한다.

명령어를 입력하는 순간 ssh-rsa부터 뭔가 엄청 길게 나오는 문장들이 있는데, 당황하지 말고 처음부터 문장 끝까지 잡아 복사하면 된다.

복사한 키는 메모장 같은 곳에 복사해두는 편이 좋다.

이제 Github 사이트에 들어가 로그인한 후, 우측 프로필을 클릭하고 Settings에 들어간다.

SSH and GPG keys를 클릭한다. 밑으로 내리다 보면 있다. 화면 우측의 초록색으로 된 New SSH key를 누른다.

Title에는 아무 제목이나 써두고, Key라고 쓰여있는 부분에 복사해뒀던 키를 붙여넣기 하여 Add SSH key를 누른다.

④ SSH를 이용한 git clone

SSH 공개 키를 복사해서 깃헙에 등록한 이유는 원하는 레포지토리에서 clone 하기 위해서이다.

원하는 레포지토리에 들어가서 우측에 Code를 클릭하고 SSH를 누른다. 나오는 링크를 복사한다.

git clone 복사한 링크를 입력하고 ls로 정상 작동되었는지 확인한다.

✷ 내가 만든 git project 다른 사람과 함께 작업하기

```
1. 내 컴퓨터에서 생성한 디렉토리를 init 명령어를 통해 Git의 관리 하에 들어가게 만들어 준다.

① 내 컴퓨터에 새로운 디렉토리(편의상 a)를 생성한다.
② 새로운 디렉토리는 내 컴퓨터에만 존재하기 때문에 버전 관리를 위해 먼저 git repository로 변환시켜준다.
    git init: 내 컴퓨터에서 내가 직접 만든 디렉토리를 git 관리하에 들어가게 만들어주는 명령어.
기존 프로젝트를 git repository로 변환, 새로운 repository를 초기화하는 데 사용할 수 있다.

이렇게 local repository 생성.

2. 내 컴퓨터의 Git 디렉토리를 Remote Repository와 연결시켜 준다.

① 변환한 local repository를 github에서 원격으로 관리해준다.
② 그러기 위해서 local repository와 remote repository를 연결하는 작업을 한다.
     git remote add repository주소
③ 내 Github에 a Repository를 하나 만들고
    그 Repository 주소를 git remote add origin 명령어 뒤에 입력한다.
    명령어를 입력했을 때 터미널창에 나타나는 변화는 없다.

3. pair의 변경 사항과 나의 변경 사항을 Remote Repository를 통해서 공유한다.

① Remote Reopository를 연결함으로서 Github Repository를 함께 공유할 수 있다.
② remote add 상대방의 repository 주소를 입력하여 상대방의 repository(편의상 이름은 b)와 연결한다.
    명령어를 입력했을 때 터미널창에 나타나는 변화는 없다.
③ git remote -v 명령어를 통해 현재의 Local Repository와 연결된 모든 Remote Repository 목록을 확인한다.

4. 페어가 작업한 코드 작업 내용 확인하기 & 충돌(conflict) 확인하기

① git pull b master: 상대방의 Remote Repository에 있는 작업 내용을 받아온다. 받아오는 내용은 자동 병합(merge)된다.
② 페어의 작업 내용을 받아오는 와중에 만일 페어와 내가 동일한 라인을 수정한 파일이 있다면 자동 병합에 실패하고 충돌이 발생한다.

‣ git status 명령어를 통해 어떤 파일이 충돌하고 있는지 확인할 수 있다.

: 충돌이 발생한 파일을 열어 보면 어떤 부분에서 충돌이 발생한 것인지 확인할 수 있다.

또한 충돌이 일어난 부분은 하나 하나 직접 확인 후 수정 필요

‣ Accept Current Change를 클릭해서 내가 수정한 내용으로 파일에 반영할 수 있다.

‣ Accept Incoming Change를 클릭해서 Remote Repository의 내용으로 파일에 반영할 수 있다.

‣Accept Both Changes는 변경 사항 모두를 반영한다.

\*Compare Change: 충돌 난 부분을 좀 더 보기 쉽게 보여준다.

‣ 직접 파일을 수정해서 반영한다.

5. 수정 후 병합 커밋(merge commit) 생성

① Remote Repository에 업로드 하기 위해서 staging area에 파일을 추가한다.

② Merge commit은 자동으로 Commit 메시지가 생성되고, 내용을 수정할 수도 있다
(git commit -m "메시지내용").

③ git commit 명령어로 자동으로 생성된 commit 메시지를 남길 수 있다.

④ Remote Repository에 Push 한다면 Merge branch ‘master’ of 라는 commit 메시지가 기록된다.

⑤ Remote Repository로 push 완료.
```

✅ 간단하게 순서 써보기

해당하는 파일 위치에 정확히 들어가서 git init → git clone → git remote add pair master → git remote -v → 코드 수정 → git add . → git status → git commit -m '커밋 메시지 내용' → git log -> q → git push origin master → (상대방 쪽에서 하는)git pull pair master

(상대방이 먼저 코드를 수정하면 내가 git pull pair master)

✅ conflict가 일어나는 상황

내가 git pull 하기 전에 어떠한 코드를 수정하고 git add . → git commit -m '커밋 메시지 내용' 까지 한 상태(git push는 하기 전).

상배방이 동일한 라인의 코드를 수정하여 git push까지 전부 끝난 상태에서 확인 요청이 들어오고, 내가 git pull pair master로 당겨 오면 conflict 발생.

제대로 상황 발생 되지 않을 시 git stash → git pull pair master하면 conflict 발생.

![](https://blog.kakaocdn.net/dn/bsM8hw/btrlGcZ24Rk/YLoYMXM6JwetLcHYq4rTQ1/img.png)
![](https://blog.kakaocdn.net/dn/bC3sWB/btrlEI6DAuZ/EkXSd3JkK2YDCP28NPUY9k/img.png)

vs code로 들어가서 conflict 수정 후 저장, 터미널에서

git add . → git status → git commit -m '커밋 메시지 내용' → git log -> q → git push origin master

까지 해준 상태에서 상대방이 git pull pair master를 하면 정상적으로 코드 병합 완료.

[(참고링크)](https://goddaehee.tistory.com/253)

✅git repository 삭제하는 방법

```
① 내 github에 들어간다.
② 삭제하고 싶은 repository를 클릭한다.
③ 톱니바퀴 모양의 settings를 클릭한다.
④ 제일 밑으로 내려서 Danger Zone까지 내려간다.
⑤ Danger Zone의 Delete this repository를 클릭한다.
⑥ Please type (삭제 하고 싶은 repository) to confirm.
이라는 멘트가 나오는데 진하게 쓴 글씨를 복붙하여 써넣는다.
⑦  다시 한 번 본인확인을 위한 github 계정 비밀번호를 입력하고 confirm을 누른다.
⑧ 삭제하고 싶은 repository가 삭제되었다.
```
