---
layout: single
title: "2-2. 220510 Software Requirement 기획"
categories: project
tag: [기록, 첫번째프로젝트, 자바스크립트, 코드스테이츠]
author_profile: false
---

코드스테이츠를 수강하면서 진행한 첫 번째 프로젝트에 대한 과정입니다.

## 1. 백엔드 세부기획 사항

[백엔드 schema design](https://github.com/codestates/Brewhere/wiki/DB-Schema)

![](https://user-images.githubusercontent.com/91467260/167611574-b3ab6ab8-e1f2-4e5a-ab8c-f55385acc9f4.png)

백엔드 포지션을 맡아 진행하면서, 스키마 디자인이 정말 힘든 부분 중 하나다.

분명 학습했는데, 어떻게 하는 것이 맞는지, 일대다 일대일 다대다 관계에 대해 생각하는 것은 정말 머리가 어지러웠다(하지만 대부분은 일대다 관계였다).

하지만 스키마 디자인이 없다면 결국 프로젝트의 진행 여부가 불투명해질 정도였다. 결론은 그래, 이것도 와이어프레임 작성 못지않게 중요하다.

## 2. 칸반보드 태스크 카드 구성 및 마일스톤 연결

github을 활용하여 칸반보드를 만들고 미리 추가해놓은 템플릿을 활용하여 태스크 카드를 구성하고 마일스톤을 만들어 구성한 태스크 카드들을 마일스톤에 연결했다.

그리고 태스크 카드들을 각각의 역할에 맞는 칸반보드에 드래그 앤 드롭한다.

## 3. 시스템 아키텍처 구성

[cloudcraft](https://www.cloudcraft.co/) 활용하여 common 탭에 있는 block, image, area, text label을 활용하여 아키텍처 다이어그램 작성.

![](https://blog.kakaocdn.net/dn/bpUAH4/btrBJL0DyC4/D72zTGwL1zNyUu6zvNUuI0/img.png)

## 4. S3 및 EC2 등의 배포 환경에 대한 기획 진행

AWS를 활용하여 EC2, S3, RDS 생성 후 연결하여 배포.

## 5. 프로토타입 작성

와이어프레임 작성 완료 후 그를 바탕으로 한 프로토타입 작성.

## 6. KPT 회고록 작성

keep, problem, try를 팀원들과 함께 공유하여 작성하기. 작성한 내용은 내일 아침 9시에 링크와 함께 제출한다.
