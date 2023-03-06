---
layout: single
title: "로지텍 마우스 - 마우스 휠 작동 안될 때 해결 방법"
categories: Information
author_profile: false
---

맥을 사용하면서 로지텍 제품을 처음으로 입문하여 쭉 쓰고 있는데, 가끔 마우스 휠이 작동하지 않을 때가 있어 그런 상황에 해결할 수 있는 방법을 정리해보았습니다.

## 개요

로지텍 전 모델이 해당되는지는 모르겠으나 현재 사용하고 있는 로지텍 mx anywhere 3 for mac은 빅서 버전인 맥북에 연결시켜두면 간혹 마우스 휠이 작동이 안될 때가 잦다. 그럴 때를 대비하여 해결할 수 있는 방법이다.

## 첫번째 방법

로지텍 옵션에 들어가서 Smooth scrolling(부드러운 휠 동작)을 Disabled(비활성화)로 바꾸면 해결된다.

## 두번째 방법

만약 첫번째 방법으로 해결이 되지 않았다면, 해당 방법을 시도해볼 수 있다.

cmd + space를 누르면 Spotlight이 켜지는데(커스텀을 해놓았다면 spotlight을 켜면 됨),

Spotlight에서 '활성 상태 보기 - Activity Monitor'를 클릭 후 '로지텍 옵션 데몬 - Logitech Option Daemon' 프로그램을 강제 종료하면 다시 restart 되면서 정상적으로 스크롤 휠이 작동한다.(이 방법으로 해결봄)

## 추가

⇒ 완벽한 해결 방법은 아니지만, 현재 시점 기준으로 빅서 혹은 몬터레이로 업그레이드 후 마우스 버벅거림이 사라졌다는 사람도 있고, 다시 마우스 휠이 작동이 안 되는 등 문제가 생긴 사람도 있었다.

두 가지 방법들은 그때 그때 휠이 작동이 잘 안 될 때의 임시방편적인 해결방법인 것 같다.

+) [macOS Logitec 권한 설정](https://support.logi.com/hc/ko/articles/360023203954-macOS-Monterey-macOS-Big-Sur-macOS-Catalina-macOS-Mojave%EC%97%90%EC%84%9C-Logitech-Options-%EA%B6%8C%ED%95%9C-%EB%A9%94%EC%8B%9C%EC%A7%80)을 해주면 괜찮다고 한다.
