---
layout: single
title: "D+50 사용 권한, 환경 변수"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

사용권한과 환경변수.

## 운영체제

컴퓨터에 있는 모든 장치와 컴퓨터에서 수행하는 모든 프로그램을 제어하며 사람과 피씨 간의 상호작용할 수 있는 도구와 명령을 제공하는 시스템 소프트웨어.

사용자 인터페이스 제공, 프로그램이 돌아갈 수 있도록 메모리에 프로그램 적재, 여러 하드웨어들의 원활한 동작 제어, 디스크에 정보를 저장, 검색하는 방식을 관리하는 기능들을 수행한다.

ex) 윈도우, 맥, 리눅스, 우분투, 안드로이드, ios, 유닉스 등등 우리가 알고 있는 것들이 운영체제의 예시로 들 수 있다.

터미널이라는 기계를 운영할 수 있게 하는 프로그램인 셸은 운영체제 상에서 다양한 운영체제 기능과 서비스를 구현하는 인터페이스를 제공하는 프로그램이다.

## 1. 사용 권한

CLI에서 파일을 보거나, 수정하거나, 실행할 때에 필요한 권한.

### ① Read(읽기), Write(쓰기), Execute(실행) 권한

[참고링크-(링크의 2-1의 ③번 ls 파트에 사용권한을 읽는 방법에 대해 서술해둠)](https://hsly22xk.github.io/javascript/javascript-cli/)

‣ mkdir과 nano 명령어로 폴더와 파일을 하나씩 만든다(폴더 안에 파일을 만들 필요는 없음).

‣ nano 명령어로 만든 파일에 내용을 수정하고 저장한다(ctrl + X, Y, Enter 순으로 새로운 파일을 저장할 수 있음)

‣ ls -l 명령어를 프롬프트에 입력하면 다음과 같은 출력을 볼 수 있다.

```
// username은 본인이 설정한 사용자 이름
// 소유자는 읽기와 쓰기, 실행이 가능하고, 다른 사용자 그룹은 읽기와 실행만 가능하다
drwxr-xr-x    2 username  staff     64  2 28 08:12 linux

// 소유자는 읽기와 쓰기가 가능하고, 다른 사용자 그룹은 읽기만 가능하다
-rw-r--r--    1 username  staff     28  2 28 08:12 helloworld.js

- : not directory, 파일일 때 나타내는 표현.
d : directory, 폴더이면 나타내는 표현.
r, w, x : read permission, write permission, execute permission. 읽기 권한, 쓰기 권한, 실행 권한.

⇒ 3번에 걸쳐 나타나는 이유: 사용자와 그룹, 나머지에 대한 권한을 표시하기 때문이다.
```

![](https://blog.kakaocdn.net/dn/slVHt/btryoYhy0uE/8PUOpXtmmp5PwrS23qB6oK/img.png)

```
✷ rwx: 읽기, 쓰기, 실행 권한이 전부 있음
  rw- : 읽기, 쓰기 권한만 있음
  r-x: 읽기, 실행 권한만 있음
  r-- : 읽기 권한만 있음
```

② user, group, and other

‣ user(===owner): 파일의 소유자. 기본적으로 파일을 만든 사람이 소유자가 된다.

‣ group: 여러 user가 포함될 수 있다. 그룹에 속한 모든 user는 파일에 대한 동일한 group 액세스 권한을 갖는다.

많은 사람이 파일에 액세스해야 하는 프로젝트가 있다고 가정할 때, 각 user에게 일일이 권한을 할당하는 대신 모든 user를 group에 추가하고, 파일에 group 권한을 할당할 수 있다.

‣ other: 파일에 대한 액세스 권한이 있는 다른 user. 파일을 만들지 않은 다른 모든 user. other 권한을 설정하면, 해당 권한을 global 권한 설정이라고 볼 수도 있다.

[✷ ls -l 커맨드를 사용하여 나오는 @과 + 는 뭘까?](https://unix.stackexchange.com/questions/92071/file-permissions-mode-ending-in-or)

③ [chmod](https://kb.iu.edu/d/abdb): 읽기, 쓰기, 실행 권한 변경 명령어

OS에 로그인한 사용자와, 폴더나 파일의 소유자가 같을 경우 명령어 chmod로 폴더나 파일의 권한을 변경 가능.

만약 OS에 로그인한 사용자와 폴더나 파일의 소유자가 다를 경우 관리자 권한을 획득하는 명령어 sudo 를 이용해 폴더나 파일의 권한을 변경 가능.

✷ chmod로 권한 설정을 해줘야 하는 이유: 내가 만든 파일이나 폴더(디렉토리)를 다른 사람이 마음대로 수정하거나 삭제했을 때 문제가 발생할 수 있기 때문에. ⇒ 권리 침해 방지.

✷ sudo(superuser do): 일반 사용자가 관리자 권한(루트 권한)을 빌려 명령어를 실행할 때 활용할 수 있는 커맨드. ⇒ 관리자 권한 획득 명령어.(편리할수록 보안에 취약해진다. 자주 남용하지 말 것)

✷ su: 계정 자체를 전환하는 커맨드. user(계정명)를 관리자 권한으로 바꾸는 것.

```
su 계정명
```

✷ sudo는 일회성 커맨드, su는 계정 자체를 전환하는 커맨드.

‣ root: 해당 시스템 전체를 관리할 수 있는 권한을 가진, 전지전능한 super user

‣ admin: 일반 유저의 하나. 그 자체가 관리자 권한을 가진 것은 아니다.

root가 admin에게 관리자 권한을 줄 수 있어 컴퓨터에서 시스템 관련한 명령을 내릴 때 admin 계정으로 들어와서 정식으로 허가를 얻으라고 말할 수 있음. 관리자 기능을 할 수 있다. ⇒ admin은 권한을 받아서 컴퓨터 관리에 관한 일만 처리.

‣ user: 일반 유저(sudo 명령어를 사용할 수 없다는 것은 아님).

### ② Symbolic method

더하기(+), 빼기(-), 할당(=)과 액세스 유형을 표기해서 변경. ⇒ 액세스 클래스와 연산자, 액세스 타입을 모두 기억해야만 권한을 변경할 수 있다.

|     Access class     |       Operator       | Access Type |
| :------------------: | :------------------: | :---------: |
|       u (user)       |    + (add access)    |  r (read)   |
|      g (group)       |  - (remove access)   |  w (write)  |
|      o (other)       | = (set exact access) | x (execute) |
| a (all: u, g, and o) |                      |             |

```
// 사용 방법
1. 명령어 chmod 뒤에 변경할 권한을 입력한다.
2. 액세스 클래스의 u, g, o, a를 변경할 조건에 따라 조합하여 입력한다.
3. 연산자와 액세스 타입을 순서대로 입력한다.

// 사용 방법 예시

// removes read permission from group
chmod g-r filename

// adds read permission to group
chmod g+r filename

// removes write permission from group
chmod g-w filename

// adds write permission to group
chmod g+w filename

// removes execute permission from group
chmod g-x filename

// adds execute permission to group
chmod g+x filename

// removes read permission from other
chmod o-r filename

// adds read permission to other
chmod o+r filename

// removes write permission from other
chmod o-w filename

// adds write permission to other
chmod o+w filename

// removes execute permission from other
chmod o-x filename

// adds execute permission to other
chmod o+x filename

// adds execute permission to user
chmod u+x filename

// -rw-rw-rw-
chmod a=rw helloworld.js

// ----rw-rw-
chmod u= helloworld.js

// -r-xrwxrwx
chmod a+rx helloworld.js

// -r-xr--r--
chmod go-wx helloworld.js

// ----------
chmod a= helloworld.js

// -rwx------
chmod u+rwx helloworld.js
```

‣ Absolute form: rwx를 3 bit로 해석하여, 숫자 3자리로 권한을 표기해서 변경.

⇒ 숫자 7까지 나타내는 3 bits의 합으로 표기

⇒ 사용자, 그룹, 또는 다른 사용자나 그룹마다 rwx가 나타나고, 각 영역의 boolean 값으로 표기할 수 있다.

✷ true이면 r,w,x로 쓸 수 있고 false이면 - 라고 표기할 수 있다.

| Permission  | Number |
| :---------: | :----: |
|  Read (r)   | 4(100) |
|  Write (w)  | 2(010) |
| Execute (x) | 1(001) |

|   #    | Sum(user, group, other) | rwx |       Permission        |
| :----: | :---------------------: | :-: | :---------------------: |
| 7(111) |   4(r) + 2(w) + 1(x)    | rwx | read, write and execute |
| 6(110) |   4(r) + 2(w) + 0(-)    | rw- |     read and write      |
| 5(101) |   4(r) + 0(-) + 1(x)    | r-x |    read and execute     |
| 4(100) |   4(r) + 0(-) + 0(-)    | r-- |        read only        |
| 3(011) |   0(-) + 2(w) + 1(x)    | -wx |    write and execute    |
| 2(010) |   0(-) + 2(w) + 0(-)    | -w- |       write only        |
| 1(001) |   0(-) + 0(-) + 1(x)    | --x |      execute only       |
| 0(000) |   0(-) + 0(-) + 0(-)    | --- |          none           |

user는 rwx 를, group과 other은 r-- 로 권한을 변경하려고 한다면, 위 표에 나와있는 숫자의 합을 user, group, other 순으로 입력하여 사용

```
# u=rwx (4 + 2 + 1 = 7), go=r (4 + 0 + 0 = 4)
// -rwxr--r--
chmod 744 helloworld.js
```

## 2. 환경 변수

프로세스가 컴퓨터에서 동작하는 방식에 영향을 미치는, 동적인 값들의 모임. ⇒ 운영체제가 굴러 가는 데 필요한 변수들의 모임.

### ① 환경변수 사용법

‣ export: 환경변수 확인하기와 환경변수 임시 적용

⇒ 터미널에 export를 입력하면 현재 설정되어 있는 환경변수들을 확인할 수 있다.

⇒ 새로운 환경변수를 추가할 수 있다. **<mark>등호 표시(Equal sign, =) 앞뒤에는 반드시 공백이 없어야 한다.</mark>**

```js
export urclass="is good"
```

⇒ 명령어 echo 와 함께 환경변수를 입력하면 설정한 환경변수의 값을 조회할 수 있다. 환경변수의 앞에는 달러사인($)을 입력하여, 변수라는 뜻을 터미널에 전달한다.

```
echo $urclass
is good
```

### ② dotenv

npm 모듈. 자바스크립트에서 환경변수를 사용할 수 있음. 이어지는 콘텐츠 .env 파일을 환경변수로 사용할 수 있게 돕는다. ⇒ .env 파일에 저장한 내용을 불러오기 위해서 dotenv 모듈이 필요하다.

```
mkdir environment_variable
cd environment_variable
npm init
// 폴더 자체를 npm init을 해주면
// node moudules를 다운받을 수 있는 상태로 변환해주고, package.json이 생성됨.

is this OK?라고 나올 때까지 엔터 키를 여러 번 누른다.
npm install dotenv --save

nano index.js
console.log(process.env);
cat index.js
node index.js
process.env를 이용해 환경변수를 객체로 받아올 수 있다.
```

⇒ **process.env 는 Node.js 환경에서 조회할 수 있다.**

‣ .env: Node.js에서 환경변수 영구 적용 ⇒ .env 파일의 내용은 key=value 형태로 써야 하며 문장의 맨 앞에 #를 붙이면 주석을 쓸 수 있다.

```
# This is sample .env
MESSAGE=hello
NUMBER=1234
```

```js
nano .env
myname=kimcoding
cat .env

nano index.js
// 내용 수정
const dotenv = require("dotenv");
dotenv.config();
console.log(process.env.myname);

cat index.js
node index.js
```

⇒ 환경변수를 이용해 API key, DB password와 같이 민감한 정보를 저장하고 관리할 수 있다.

⇒ 서로 다른 PC 또는 여러 .env 파일에서, 같은 변수 이름에 다른 값을 할당할 수 있다.

⇒ <mark>개발 환경과 제품을 제공하는 환경에서 사용하는 API 키가 다른 경우, 환경변수를 이용해 환경을 구분하여 코드를 작성할 수 있다.</mark>

⇒ .env 파일의 기본 위치는 프로젝트의 루트 디렉토리다.

⇒ .config() 함수에 path를 지정하면 다른 위치에 있거나 기본 이름이 다른 .env 파일을 참조할 수도 있다.

```js
require("dotenv").config({
  path: ".env.sample",
});
```

✷ 실제 제품(서비스)을 개발하는 과정에는 개발 환경(local 또는 development 등)과 테스트 서버의 환경(test), 실제 제품을 제공하는 환경(production)이 있다.

구글 API를 이용해 웹 애플리케이션을 만드는 경우, 개발 환경에서는 개발자 개인의 API 키를 이용할 수 있다. 제품을 서비스할 때 개인 API 키를 사용하면 일일 요청량을 초과하는 경우 제품이 정상적인 동작을 할 수 없다. 이런 경우를 방지하기 위해 실제 제품에서는 기업용 API 키를 사용한다.

✷ 데이터베이스도 개발, 테스트, 제품 환경으로 구분할 수 있다.

![](https://blog.kakaocdn.net/dn/F5IBF/btruoKO7wCe/JNkOpANLPRK5nm3KluyH11/img.png)

(다른 환경에 같은 변수 이름을 사용하여 DB를 구분하는 예시)

[✷ github에 DB관리를 하기 위한 방법](https://github.com/leejanghe/Today-I-Learned/blob/master/ReactStudy/api_%ED%82%A4_%EC%88%A8%EA%B8%B0%EA%B8%B0.md)

```
// .gitignore 파일도 직접 생성해야 한다.
// 파일 안에 들어가야할 내용
.env
/node_modules
```
