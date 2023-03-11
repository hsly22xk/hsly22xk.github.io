---
layout: single
title: "MySQL 설치하기"
categories: Information
author_profile: false
---

터미널에 mySQL 설치하기.

## 1. macOS에서 homebrew를 통한 MySQL 설치

```
brew install mysql
brew info mysql
```

(우분투 / 리눅스 환경 설치 명령어)

```
// 패키지 매니저 apt-get을 이용한 설치
// OS에 포함된 패키지 매니저이기 때문에 별도 설치 필요 X
sudo apt-get update
sudo apt-get install mysql-server
```

## 2. MySQL 프로그램 실행

```
brew services start mysql
```

(우분투 / 리눅스 환경 설치 명령어)

```
sudo systemctl start mysql
```

## 3. MySQL 접속과 비밀번호 세팅

```
mysql -u root
mysql을 처음 설치하면 root 비밀번호는 비어있기 때문에 엔터 키를 눌러준다.
welcome mysql이라는 문구가 뜨면 mysql 콘솔로 들어가진 상태. 그 다음에
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'yourPassword';
이라는 명령어를 입력하되, yourPassword 부분을 지우고 본인만의 mysql 비밀번호를 입력한다.
mysql -u root -p 명령어 입력 후 엔터
본인만의 지정 비밀번호 입력
비밀번호 설정 완료
```

✷ SQL GUI Support Tool

[MySQL Workbench](https://www.mysql.com/products/workbench/)

[Sequel Pro (OSX 전용)](https://www.sequelpro.com/)

[Table Plus](https://tableplus.com/)

[DBeaver](https://dbeaver.io/download/)

[DataGrip](https://www.jetbrains.com/datagrip/)

⇒ 뭘 사용하던 사용자의 편의에 맞는 방법을 사용하되 GUI, CLI 환경 모두 사용할 줄 알아야함.
