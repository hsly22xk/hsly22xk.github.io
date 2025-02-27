---
layout: single
title: "D+11 CLI"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

CLI 기본 명령어와 관련 내용 정리.

## 1. CLI

Command-Line Interface, 명령어를 입력하여 컴퓨터를 조작하는 방식으로 텍스트 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식.

작업 명령은 사용자가 컴퓨터 키보드 등을 통해 문자열의 형태로 입력하며, 컴퓨터로부터의 출력도 문자열 형태로 주어진다.

① 입력(Input)

화면을 보기 위해 마우스를 사용하고, 메시지를 입력하기 위해 키보드를 사용한다.

화상통화 시 얼굴을 보여주기 위해 내장되어 있는 카메라가 필요하고, 말을 전달하기 위해 마이크를 사용한다.

입력을 담당하는 키보드나 마우스, 컴퓨터에 새로운 명령을 전달하는 카메라와 마이크를 입력소스(Input source)라고 한다.

즉, 입력소스란 컴퓨터를 조작하기 위해 입력하는 것이다.

② 출력(Output)

입력소스에 의해 또는 작성된 프로그램에 의해 모니터에 화면을 나타내거나, 음악을 재생하면 소리를 스피커로 전달하여 사용자가 인식할 수 있도록 하는 일.

출력 소스(Output source)란 모니터로 화면을 나타내거나 스피커로 소리를 전달하는 것을 출력하는 것이다.

모니터나 스피커 외에도 스마트 홈을 연결하여 전등이나 공기청정기를 조작하는 경우 전등과 공기청정기도 출력소스라고 말할 수 있다.

- 컴퓨터를 조작하기 위한 입력과 출력을 간단하게 I/O(Input/Output)라고 표기한다.

## 2. 터미널의 프롬프트와 기본적인 명령어

프롬프트: 키보드의 입력을 확인하고 편집할 수 있는 한 줄의 공간

① pwd(print working directory): 현재 위치 확인하기

프롬프트에 pwd를 입력하고 Enter를 누르면 현재 경로가 나타난다.

CLI에서 폴더를 열거나 닫으면서 이동하다 보면 현재 위치가 헷갈릴 수 있다.

그럴 때 pwd를 사용하면 컴퓨터는 현재 작업 중인 폴더의 위치를 출력한다.

- 디렉토리(directory)를 폴더라고도 한다.

- 명령어를 입력한 후 항상 엔터를 쳐야 실행이 된다.

② mkdir(make directories): 새 폴더 생성하기

컴퓨터에 새 폴더를 만들라는 명령을 전달한다.

mkdir을 프롬프트에 치고 스페이스 바를 눌러 띄어쓰기를 해준 후 폴더 이름을 입력한다.

컴퓨터는 명령어와 폴더의 이름을 띄어쓰기로 구분한다.

✅ <mark>폴더 또는 파일의 이름에 공백(띄어쓰기)이나 특수문자가 있으면 백슬래시(\)를 이용해 적용한다.</mark>

③ ls(list): 특정 폴더에 포함된 파일이나 하위 폴더의 리스트를 출력

mkdir 명령어를 사용해 생성된 폴더를 확인하기 위해서

현재 폴더에 포함된 파일이나 폴더의 이름을 출력하는 명령어가 필요하다.

✅ ls의 옵션

ls -a(all): a는 숨어있는 폴더나 파일을 포함한 모든 항목을 터미널에 출력한다.

ls -l: 폴더나 파일의 포맷을 전부 표현하라는 의미

- CLI에서 특정 명령어의 옵션을 사용하는 경우에는 -를 이용해 옵션을 입력했다고 컴퓨터에 전달함
- 하나의 파일, 폴더는 한 줄에 입력된다.

명령어로 ls -l을 입력하면 가장 왼쪽에 'd' 와 '-' 를 확인할 수 있다.

drwxr-xr-x

-rw-r--r--

r-- : 읽기 권한만 있음
여기서 d로 출력된 경우는 폴더를, -로 출력된 경우는 파일을 나타낸다.

drwxr-xr-x

를 두 분류로 다시 나눠보자.

① [d]

② [rwxr-xr-x]

```
‣ r : read, 읽기 권한. 파일 및 폴더 안에 있는 데이터, 속성, 서브 폴더 등에 접근이 가능하다.
‣ w : write, 쓰기 권한. 파일 및 폴더의 속성과 데이터 변경 가능.
‣ x : execute, 실행 권한. 해당 파일을 실행하여 사용할 수 있음.
‣ - : 권한 없음
```

그럼 ②번을 다시 쪼개서 읽으면?

[rwx] [r-x] [r-x] // []표시는 이해하기 쉽도록 임의로 표시함.

rwx는 해당 파일에 읽기, 쓰기, 실행 권한이 있음을 의미하고 r-x는 읽기, 실행 권한은 있으나 쓰기 권한은 부여되지 않았음을 의미.

그렇다면 왜 r-x를 두 번 쓸까?

제일 앞에 쓴 [rwx]는 파일 및 폴더를 소유하고 있는 유저가 가지는 접근 권한에 대해 설명하고 있다.

즉, 해당 파일을 소유하고 있는 유저는 해당 파일에 대한 읽기, 쓰기, 실행 권한을 가진다.

2번 [r-x]는 그룹을 특정하고, 3번 [r-x]는 다른 유저를 특정하고 있다.

④ open . : 터미널의 현재 위치를 GUI의 탐색기(파인더)로 여는 명령어(open 띄어쓰기 .)

프롬프트에 open . 이라고 치고 엔터를 누르면 폴더의 현재 위치가 바로 나온다.

⑤ cd(change directory): 폴더에 진입하기

mkdir을 이용해 만든 폴더에 진입하기 위해서는 pwd를 이용해 현재 위치를 파악하고, ls를 이용해 파일 이름을 확인한 후, cd를 이용하면 폴더에 진입할 수 있다.

그다음 open . 을 치고 엔터를 누르면 현재 위치인 폴더가 나오게 된다.

- 폴더에 진입할 때 /(슬래쉬)는 생략할 수 있다.

⑥ touch: 새 파일 생성하기

이제 만든 폴더에 파일을 생성해 볼 것이다. touch 파일 이름을 치면 된다.

대표적인 예시로는 텍스트 파일을 만들 수 있다. touch hi.txt

\*mac에서는 text editor로 텍스트 파일이 열린다.

\*파일의 이름은 파일의 확장자를 포함한다.

\*touch 명령어를 사용하여 여러 이름의 파일들을 생성할 수 있다.

⑦ cat: 파일 내용을 터미널에 출력하기

⑥번에서 touch 명령어로 새 텍스트 파일 hi를 생성하였다. 그 파일을 열어 이메일 주소를 적고 저장했다.

그 내용을 터미널에 출력해볼 것이다. cat hi.txt 를 치고 엔터를 누르면 된다.

\*출력 내용 끝에 쓰지 않은 다른 문자가 붙어있다면, 내용을 입력하고 엔터를 누르지 않아 그런 것이다. 내용에는 이상 없음.

✷ cat 명령어 대신 쓰는 명령어들

cat 명령어는 파일의 내용을 터미널에 출력해주지만, 항상 전체 내용을 출력해준다.

그렇기 때문에 파일 내용의 부분만 열람할 수 있게끔 해주는 명령어들이 있다.

```
‣ head: 텍스트로 된 파일의 앞부분을 지정한 만큼 출력하는 명령어.
• head 파일명 // 앞에서부터 10행까지의 내용만 보여준다.
• head -n 100 파일명 // 앞에서부터 100행까지의 내용을 보여준다. -n 뒤에 숫자는 원하는 숫자로.
• head -c 100 // 100바이트 만큼의 내용만 보여준다. -c 뒤에 숫자 또한 원하는 숫자로.
‣ tail: 파일의 마지막 행을 기준으로 지정한 행까지의 파일내용 일부를 출력. 기본적으로 마지막 10줄을 출력한다. 오류나 파일 로그를 실시간으로 확인할 때 매우 유용하게 사용된다.
• tail 파일명 // 기본적인 출력을 해준다.
• tail -n 20 파일명 // 지정한 행까지 출력을 할 경우 -n 옵션을 이용하여 옵션 값을 입력한다. 파일의 특정 행부터 마지막 행까지 출력하고 싶은 경우에는 '+'를 이용
•tail -c 200 // 바이트를 기준으로 출력한다.
•tail -f // 오류나 파일 로그를 실시간으로 모니터링하는 경우 사용한다.

파일의 마지막부터 10줄을 출력하며, 종료되지 않은채 표준입력을 읽어들여 출력해준다.

종료하고 싶을 때는 control + c
‣ more: 파일을 읽어 화면에 화면 단위로 끊어서 출력하는 명령어. 위에서 아래 방향으로만 출력 되기 때문에 지나간 내용을 다시 볼 수 없다.
• more 파일명 // 왼쪽 하단에 화면에 출력된 내용이 전체의 몇 % 인지를 표시. Enter 키를 입력하면 한 줄씩 출력, Space bar를 입력하면 한 화면씩 출력
• more -n 파일명 // n에 입력한 값만큼 끊어서 화면에 출력. Space bar를 입력하면 입력한 값 만큼씩 끊어서 화면에 출력.
• more +n 파일명 // n에 입력한 행부터 화면에 출력
- 확인하고자 하는 파일의 내용이 너무 길 경우 한 화면에 다 출력할 수 없으므로 파이프(|)를 이용해서 more 명령어를 사용한다.

ls -al | more
```

```
‣ less: 파일을 읽어 화면에 출력하는 명령어. 한 번에 보여지는 만큼만 읽어서 출력해서 대용량의 파일을 열어 볼 때 빠르게 사용 할 수 있음.
• less 파일명
• less -?: less에서 사용할 수 있는 명령들에 대한 도움말 출력
• less --help: 해당 명령어의 도움말을 보여주고 실행이 종료
• less -i: 대소문자를 구분하여 탐색
• less --version: version 정보를 출력하고 실행이 종료
• less 행번호 파일명: 지정된 행 다음부터의 내용을 출력
```

- CLI는 텍스트를 기반으로 소통하기 때문에, GUI를 이용한 편집기가 실행되지 않는다.

GUI에서는 파일 "hi.txt"를 찾아 아이콘을 더블클릭하거나, 한 번 클릭하고 Enter를 눌러 텍스트 편집기를 열어 파일의 내용을 확인할 수 있다. 그러나 CLI와 GUI가 편집하는 파일은 같은 파일이다.

GUI와 CLI는 하나의 컴퓨터를 동일하게 조작하지만, 보이는 모습에 차이가 있다.

⑧ rm(remove): 폴더나 파일을 삭제할 때 사용함.

폴더나 파일을 삭제할 때 사용하는 명령어이지만, 실제로 rm만 써서 지울 수 있는 것은 폴더가 아닌 파일이다.

폴더를 삭제하고 싶다면 옵션을 붙인다. rm -rf 폴더명 을 치고 엔터를 누른다.

옵션 r(recursive): 폴더를 지울 때 사용하는 옵션 // 옵션 f(force): 질문을 받지 않고 지울 때 사용함.

\*rm은 CLI 내에서 삭제할 때 사용하는 명령어이므로, 여기서 삭제하면 다시는 복구할 수 없다. 되돌리는 방법은 없다.

⑨ mv(move): 폴더나 파일의 위치를 옮기거나 이름을 변경할 때 사용함.

mv 파일명 폴더명 으로 명령어를 써줄 수 있다.

예를 들어 mkdir 명령어로 bye라는 폴더를 만들고 touch명령어로 bye.txt를 생성하였다.

그 후 bye.txt를 bye폴더에 옮기고 싶다면 mv bye.txt bye/를 써주면 된다.

이제 텍스트 파일의 이름을 변경해주고 싶다. 똑같이 mv명령어를 사용해준다.

mv 원래 파일명 바꾸고 싶은 이름의 파일명

솔직히 헷갈린다. 그냥 예시를 들자.

```
mv bye.txt // 원래 파일명
hi.txt // 바꾸고 싶은 파일 유형
```

(예시를 보여주기 위해서 띄어쓰기를 많이 했지만 사실 띄어쓰기 한 번씩이면 된다.)

⑩ cp(copy): 폴더나 파일 복사하기

cp 원본 파일 이름 복사할 파일 이름

예시를 들자면 이렇다.

```
cp hi.txt bye.txt

⟹ hi.txt의 파일의 내용을 복사하여 bye.txt라는 파일을 생성한 후, 복사한 내용을 붙여 넣었다.
```

이제 폴더를 복사해본다. 반드시 옵션이 붙어야 한다.

cp -rf 원본 폴더 이름 복사할 폴더 이름

```
cp -rf hi bye

⟹ hi라는 폴더의 내용을 복사하여 bye라는 폴더를 생성한 후, 복사한 내용을 붙여 넣었다.
```

\*clear(command + k): 터미널에 여러 복잡하고 많은 내용들을 한 번에 지워주는 명령어

\*만약 cd명령어를 사용해 폴더를 찾는데 이름이 생각이 안날 때는?

⇒cd 기억나는 데까지 폴더 이름 치고 Tab(탭)키 누르기

✷ -r 과 -f 명령어 옵션

앞서 언급했지만 -r은 recursive의 약자로 특정 행동을 순환적으로 반복한다. -f는 force의 약자로 어떤 행위를 강제한다.

즉, -f 명령어를 사용하면 보호되거나 존재하지 않는 파일도 강제로 삭제할 수 있다.

위에서 언급한 -rf 명령어를 사용하면 민감한 정보를 가진 파일도 무차별적으로 삭제함

## 3. 절대 경로와 상대 경로

① 절대 경로: pwd(현재 경로)로 확인할 수 있음

기준점으로부터의 절대적인 위치를 나타낸다. 이때 기준점을 루트폴더( / )라고 한다.

⇒ 즉, 절대 경로란 특정 폴더나 파일이 루트폴더로부터 어떤 폴더로 진입하는 경우 만날 수 있는지 나타낸다.

예를 들자면 이런 것이다.

```
/Users/username/helloworld/hi/
```

루트 폴더에는 제일 앞에 쓰여진 /Users가 들어있고, User안에 username이라는 폴더가 있고,

그 안에 helloworld, 그 안에 hi 폴더가 있는 것을 알 수 있다. 이 과정을 한 줄로 줄여놓은 것을 절대 경로라고 한다.

✷ 루트폴더

앞에서 루트폴더는 절대 경로의 기준점이라고 말했다. 그런데 루트폴더는 Linux의 관리자 영역이다.

Linux 관리자의 가장 큰 특징은, 어떤 일이 있더라도 일반 사용자에게 관리자 권한(루트 권한)을 완전하게 넘기지 않는다.

이 말은, 일반 사용자의 권한으로는 어떤 폴더나 파일도 생성, 변경, 삭제할 수 없다는 것이다.

사용자가 관리자 권한을 필요로 하는 경우는 새로운 프로그램 설치, 프로그램 변경 또는 삭제하는 경우이기 때문에

해당 프로그램 설치, 변경 또는 삭제할 수 있는 관리자 권한만 전달한다.

사용자와 관리자를 명확히 분리하여 사용자의 실수로 발생할 수 있는 시스템 에러로부터 운영체제를 보호한다.

루트폴더는 관리자의 영역이기 때문에 사용자 권한으로는 할 수 있는 일이 없다.

루트폴더로 이동하여 명령어 mkdir을 이용해 폴더 test를 생성하면, "Read-only file system"이라는 에러를 만난다.

\*읽기전용(Read-only): 폴더나 파일을 생성, 변경 또는 삭제할 수 없다는 말이다.

1. whoami: 현재 로그인된 사용자를 확인하는 명령어

이 명령어를 입력하면 macOS를 처음 설정할 때 지정했던 username이 나온다. 이 사용자는 폴더의 형태로 존재한다.

사용자 권한은 이 username 폴더 내에서만 자유롭게 사용할 수 있다.

username에 맞게 폴더를 생성하여 해당 폴더 내에서 권한을 사용하도록 제한한다.

반면에 관리자 권한을 이용하면, 다른 사용자 폴더에도 영향을 끼칠 수 있다. 당연히 시스템 자체에도 접근이 가능하다.

관리자 권한으로 변경한 내용은, 사용자 권한으로 해결할 수 없다.

\*사용자 폴더 경로는 (루트폴더로부터 사용자 폴더까지의 경로)/ 로 표시한다.

2. sudo(superuser do): 관리자 권한을 획득하는 명령어

앞서 언급했지만 일반 사용자의 권한으로 새로운 프로그램을 설치하거나 변경, 삭제하지 못한다.

이 말은 사용자가 새로운 프로그램을 설치하거나 변경, 삭제할 때는 관리자 권한이 필요하다는 것이다.

sudo는 이런 사용자 환경에서 관리자 권한을 획득하는 명령어이며, 기본적인 CLI명령어 앞에 작성한다.

예를 들어 sudo mkdir 이라고 하면 관리자 권한을 일시적으로 획득하여 폴더를 생성한다는 것이다.

일시적으로 획득한 관리자 권한이기 때문에 항상 비밀번호와 함께 사용한다.

비밀번호는 처음 계정 생성 시 지정했던 비밀번호를 말한다.

비밀번호를 입력하면 비밀번호가 화면에 출력되는 것이 보이지는 않지만, 비밀번호가 맞다면 터미널에서 정상 입력되고 있다.

비밀번호를 입력하고 엔터를 누르면 폴더가 정상 생성된다.

이렇게 만들어진 폴더는 관리자 권한으로 생성된 폴더, 즉, 폴더의 소유자는 루트이다.

② 상대 경로: 현재 위치로부터 상대적인 위치를 나타냄

현재 위치한 폴더를 . 으로 나타내고 상위 폴더는 . . 으로 나타낸다.

(\*실제로 색깔이 들어가게 치진 않지만, 강조를 위해 다르게 표기했다)

```
/Users/username/helloworld/hi
```

현재 경로에 포함된 폴더나 파일을 확인하기 위해 ls를 사용할 수 있다.

명령어 ls를 통해 확인되는 폴더나 파일은, 상대 경로로써 ./ 을 붙여 표현할 수 있다.

만약 현재 폴더 아래의 폴더 hi로 진입하려고 한다면, 명령어 cd를 이용할 수 있다.

점(.)은 현재 폴더를, 슬래시(/)는 폴더 내부를 나타낸다. 다음 표현에 포함된 ./는 "현재 폴더 아래의"라는 뜻이다.

즉, ./hi는 현재 폴더 아래의 폴더 hi를 나타낸다. 명령어 cd와 함께 사용한다면, 현재 폴더 아래의 폴더 hi로 진입하라는 뜻.

바로 위에 쓴 두 줄을 예시로 표현하면 cd ./hi 이 된다. 이것으로 현재 폴더의 아래 위치에 있는 hi 폴더에 진입할 수 있다.

이제 hi폴더에서 상위폴더로 다시 진입하고 싶다면?

간단하게 cd ../ 명령어를 치면 hi의 상위폴더로 가게 된다.

✷ 텍스트 에디터 nano

→ nano는 터미널에서 다룰 수 있는 에디터이고, 리눅스 기반 환경에서 기본으로 탑재되어 있는 프로그램이다.

→ 그럼 그냥 vs code로 열면 안 되나? 굳이 nano를 써야 되는 이유는?

물론 vs code를 CLI로 열 수 있는 명령어가 있다(code script.js // script라는 js파일을 vs code로 여는 명령어).

하지만 AWS(Amazon Web Service)와 같은 원격 서버 환경에서 원격으로 텍스트 파일을 편집해야 하는 경우가 있다.

터미널에서 자유자재로 다룰 수 있는 에디터가 하나쯤은 있어야 하고, CLI에서 쉽게 접근할 수 있는 텍스트 에디터는 nano이다.

nano 라는 명령어 하나만으로 nano를 실행할 수 있고, code처럼 nano script.js 라고 명령어를 입력하면 script.js가 nano로 열린다.

![](https://blog.kakaocdn.net/dn/bhoyP5/btrlfA8GILT/bHPi6nNVknvJrkikVuXTp0/img.png)

따로 파일을 열지 않고 터미널에 nano 라고만 입력했을 때 나오는 창이다.

맨 위에 GNU nano 2.0.6 이라고 써진 부분이 파일 이름이 되고,

아무 내용도 없이 커서만 있는 하얀 부분이 실제로 편집할 수 있는 텍스트 부분이고,

제일 밑에 ^x 같은 부분이 nano를 사용할 때 필요한 단축키 모음이라고 보면 된다.

^x 는 맥에서 control + x

- 단축키

^r : 파일 열기(제일 좋은 방법은 처음부터 터미널에서 nano를 치고 파일 이름을 쳐서 불러오는 방법이다)

^x: nano 종료하기

이제 종료하기를 눌렀을 때, 변경사항이 생기면

```
Save modified buffer (ANSWERIG "No" WILL DESTROY CHANGES) ?
```

같은 프롬프트가 뜬다.

변경사항을 저장할건지 안할건지를 물어보는 말인데, 키보드로 y를 누르면 저장, n을 누르면 저장 안함이다.

여기서 control + c 를 누르면 다시 nano로 돌아간다.

## 4. 패키지와 패키지 매니저

패키지 안에는 하나의 프로그램이 정상적으로 설치되고 동작하기 위한 모든 파일이 압축되어 있다.

프로그램의 구성은

```
‣ 프로그램 파일
‣ 프로그램 설치 파일
‣ 프로그램 설치 설명서
‣ 프로그램에 대한 정보를 담은 파일
```

로 구성 되어 있다.

프로그램에 대한 정보를 담은 파일은 프로그램 A를 설치하기 위해 프로그램 B가 필요하다는 정보도 함께 담겨있다.

패키지를 이용해 프로그램을 설치하면 패키지에 포함된 정보를 이용해 프로그램 B를 먼저 설치하고 나서 프로그램 A를 설치한다.

그런데 정작 패키지가 뭔지는 설명을 안해준다. 그럼 찾아봐야지.

```
패키지: 코드의 배포를 위해서 사용되는 코드의 묶음
패키지 매니저는 이러한 패키지의 설치, 변경, 삭제, 업데이트 등 관리를 편리하게 해주는 도구이다.
```

패키지 매니저를 사용하지 않고 프로그램을 독립적으로 설치하는 데에는 큰 단점이 있다.

여러 프로그램을 개별로 설치하기 위해서는 각각의 프로그램이 저장된 위치를 모두 알아야 한다.

모든 프로그램이 여러 군데에 퍼져 있기때문에, 원하는 프로그램을 찾기 위해서 해당 프로그램 저장소 위치를 알아야 한다.

그리고 해당 프로그램의 업데이트 여부를 확인하기 위해서도 주기적으로 저장소를 방문해서 확인해야 한다.

만약 컴퓨터에 설치된 프로그램이 점점 늘어난다면, 모든 프로그램을 업데이트하는 일이 불가능에 가까워진다.

이런 단점을 보완하기 위한 도구가 바로 패키지 매니저다.

사용자가 패키지 매니저를 이용해 필요한 패키지를 설치할 수 있다.

패키지 매니저는 모든 패키지의 저장소 위치를 저장하고 있다.

사용자가 패키지 매니저에게 특정 프로그램의 설치를 요청하면, 패키지 매니저는 패키지가 저장된 위치에서 패키지를 다운로드 받아 설치 프로그램을 실행한다.

패키지 매니저는 설치된 모든 프로그램의 업데이트를 확인하거나, 필요없는 프로그램을 제거하는 데에도 사용할 수 있다.

나는 macOS를 사용하는 중이니 mac에서 맞는 패키지 매니저를 설치하고, 관리하는 명령어를 정리한다.

## 5. homebrew 설치와 명령어

설치 과정

```
① xcode-select --install를 터미널에 입력해본다.

입력했을 때 brew not found(혹은 팝업창이 생성됨)문구가 나오면 설치를 진행하고, xcode-select: error: 라는 문장이 나온다면 이미 설치가 된 것이니 굳이 다시 설치해주지 않아도 된다.

② 이제, [homebrew](https://brew.sh/) 사이트에 들어가보면, Install Homebrew라고 쓰인 곳에 링크가 있다.

이 링크를 복사해서 터미널에 붙여넣기 한다.
(혹은 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)")

③ 붙여넣기 한 후 엔터를 치면, 비밀번호를 물어본다. 계정 생성 시 만들었던 비밀번호를 입력하면 된다.

만약 틀려도 다시 시도하라는 문구가 뜬다. 제대로 비밀번호를 입력하고 엔터를 친다.

④ 그러면 쭉 나오다가 Press RETURN to continue or any other key to abort 라는 문구가 나오면 다시 엔터를 친다.

⑤ 뭔가 쭉쭉 나오다가 Installation successful! 문구가 나오면 설치 성공이다.

⑥ 그 다음 Next step에서 읽다보면 echo 'eval ~~~~~ eval "$(/opt~~~~~~~~~)" 까지 길게 써있는 부분이 있다. 그 부분을 전부 선택해서 복사+붙여넣기.

⑦ 붙여넣기 후 엔터를 누르고 brew help 라고 쳤을 때

Example Usage부터 Further help 내용까지 나오면 설치 성공했다.
⇒ ⑤,⑥,⑦번 과정이 생략되었다. 기다리다보면 설치가 완료되고 which brew, brew help 명령어를 실행했을 때
Example Usage부터 Further help 내용까지 나오는 것을 확인할 수 있었다(2022년 9월 수정)
```

명령어

```
① brew 자체 업데이트: brew update
② 업데이트 필요한 파일 조회: brew outdated
③ 프로그램 업그레이드(업데이트): brew upgrade 프로그램 이름
④ 프로그램 검색: brew search 검색어
⑤ 프로그램 정보 확인: brew info 프로그램 이름
⑥ 프로그램 설치: brew install 프로그램 이름
⑦ 프로그램 삭제: brew uninstall 프로그램 이름
⑧ 설치된 프로그램 보기: brew list
⑨ 버전을 여러개 깔았는데 최신버전 이외의 버전들 전부 삭제: brew cleanup 프로그램 이름
```

## 6. 자바스크립트 런타임

① 런타임: 프로그래밍 언어가 실행되는 환경. 어떤 프로그램이 동작할 때, 프로그램이 동작하는 곳.

우리가 JavaScript를 이용해서 코드를 적었으면 코드가 실행되는데 이 때 실행되는 곳이 런타임.

② node.js: 자바스크립트 런타임. 자바스크립트를 이용해 웹 페이지 뿐만 아니라 서버와 같은 다른 프로그램을 만들 수 있음.

③ node 명령어: 작성한 코드가 어디에서 동작하고 있는지 구분할 수 있음

## 7. nvm과 nvm으로 Node.js깔기

‣ nvm: node version manager, 즉 Node.js의 버전을 관리해주는 패키지 매니저.

굳이 nvm으로 node.js를 깔아주는 이유는 다양한 버전의 Node.js를 쉽게 설치할 수 있고, 별다른 작업 없이도 npm을 sudo 없이 사용할 수 있어서이다.

‣ nvm설치 방법

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

이라는 명령어를 터미널에 입력하고 엔터를 친다.

만약 wget을 설치하지 않았다면 먼저 설치하고 명령어를 입력한다.

앞서 homebrew를 설치했기 때문에 brew install wget으로 간단하게 설치 가능.

입력한 후 Close and reopen your terminal 이라는 문장이 나온다.

nvm은 설치 후 바로 실행되지 않기 때문에 터미널을 껐다 켜준다.

그 다음 nvm --version 명령어를 통해 nvm의 버전을 알아본다. 버전이 나온다면 설치가 잘 되었다.

‣ nvm으로 Node.js 설치하기

다음은 Node.js를 설치해본다. 앞서 언급했듯 nvm으로 다양한 버전의 Node.js를 설치할 수 있다.

```
nvm install v16.11.1
// 글을 쓰는 시점에서의 최신 버전. lts버전과 최신버전은 Node.js 사이트에서 확인해볼 수 있다.
```

치고 엔터를 누르면 설치가 된다.

다시 node -v 명령어를 입력했을 때 버전이 나온다면 Node.js 설치도 끝났다.

\*M1칩을 이용하는 Mac의 경우 15버전 미만의 버전을 사용할 때 제대로 설치되지 않을 수 있으니

15버전 이상의 node.js 사용할 것. 나는 M1 유저라 16.11.1 버전으로 설치함.

## 8. npm과 package.json

‣ node로 js 파일 실행하기: 간단한 함수를 작성하고, 작성한 파일을 node로 열어볼 것이다.

```javascript
① nano node.js 로 새로운 파일 node.js파일을 생성하고 nano로 열어준다.
② function helloWorld () {
    console.log("Hello world!");
  }
  helloWorld();
③ control + x + y
④ node node.js
까지 하면 터미널에 Hello World! 라는 글을 볼 수 있다. 봤다면 성공이다.
```

‣ npm: node package manager,

즉 자바스크립트 프로그래밍 언어를 위한 패키지 관리자다. Node.js의 기본 관리자.

이 npm을 사용하기 위해서 우리는 앞에서 Node.js를 설치해준 것이라 생각하면 되겠다.

‣ package.json: npm모듈을 활용하기 위해 해당 모듈에 대한 정보를 담은 파일. 프로젝트 전반에 관한 정보가 들어있음.

일반적으로 루트폴더에 위치해있으며, 다른 사람에게 프로젝트의 정보를 알려주기 위해 있음.

①프로젝트의 정보: name, version영역

②scripts항목: CLI에서 사용가능한 명령들

③패키지 버전 정보: dependencies / devDependencies 영역

이렇게 세 가지로 프로젝트 정보, scripts항목, 패키지 버전 정보라는 큰 상자가 각각 있다고 생각하면 되겠다.

‣ scripts항목

npm script라고 불리며, CLI에서 사용 가능한 명령들이다.

터미널에서 npm run script이름 으로 실행 가능

|    작업 내용    | 실행 스크립트 |
| :-------------: | :-----------: |
| node.js 앱 실행 | npm run start |
|   테스트 실행   | npm run test  |
|    코드 검사    | npm run lint  |

- npm run submit은 과제 제출을 위한 것으로 내가 공부할 때 과제 제출하는 용도로 썼음.

- 표로 만든 명령어들이 항상 모든 프로젝트에 다 있는 것이 아님.

‣ dependencies: 직접 실행과 관련 있는 dependency

npm install --save-react

--save 옵션과 함께 설치하면, 자동으로 dependencies에 추가됨(save 옵션 생략 가능)

‣ devDependencies: 프로그램 실행과 관계없는 오로지 개발을 위해 필요한 dependency(의존성 모듈)

npm install mocha --save-dev

⇒ npm install을 이용하면, npm에 있는 모듈을 설치할 수 있는데, 이 때 --save-dev 옵션과 함께 설치하면 자동으로 devDependencies에 추가됨.

(\* mocha는 테스트를 위해 필요함)
