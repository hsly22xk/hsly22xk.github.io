---
layout: single
title: "사용 중인 포트를 찾고 강제 종료하기"
categories: Information
author_profile: false
---

How to find and kill a process running on a port.

## 개요

가끔 로컬 환경에서 배포를 시도하다보면, 포트가 열려있는 상태에서 같은 포트 번호를 열게 될 때가 있다.

그럴 때마다 매번 포트 죽이기 방법을 검색해야하는 것이 힘들어, 블로그에 기록해둠과 동시에 기억해두려 한다.

## 해결방법

```
// 숫자는 연결을 끊을 포트 번호로 쓰기
// 3000번 포트라면 3000
// port 번호로 PID 찾기
sudo lsof -i :3000

lsof -i TCP:3000

// pc password 입력 후 PID 번호를 알아낸다
// -15 뒤에 붙는 숫자는 PID 번호(11111은 임의로 쓴 숫자)
kill -15 11111

다시 npm start 하기
```

## ✷ -15 vs -9

kill -15 [pid#]는 연결을 끊고 나머지 잔여물들이 남지 않도록 말끔히 처리하는 반면, kill -9 [pid#]는 데이터베이스 같은 잔여물들이 불안정한 상태로 남아있을 수 있어 권장하지 않는 분위기라고 한다.
