---
layout: single
title: "Atlas Cluster 생성하기"
categories: Information
author_profile: false
---

mongoDB atlas cluster 생성 과정.

① [MongoDB](http://cloud.mongodb.com/) 사이트를 들어간다.

② Log in with Google을 클릭한다.

![](https://blog.kakaocdn.net/dn/cxekOI/btrvZ4q2GQK/2AIgKmgtdK5VF6OGs0y4g1/img.png)

③ View All Organizations를 클릭한다.

![](https://blog.kakaocdn.net/dn/b5Y02c/btrvWGSt50Z/FxqYLFj1mnDb340nKjsjj0/img.png)

④ 우측에 있는 Create New Organization을 클릭한다.

![](https://blog.kakaocdn.net/dn/doMBM5/btrvW3Ubz3g/Q7TmE3sPgr5Wntly0M5B70/img.png)

⑤ Organization Name을 설정하고, MongoDB Atlas에 체크되어 있는지 확인한 후 Next를 클릭한다.

![](https://blog.kakaocdn.net/dn/K618b/btrvPK1bPEz/EneEhSJXcStAs4wPJkvpDk/img.png)

⑥ Create Organization을 클릭한다.

![](https://blog.kakaocdn.net/dn/cV3tH2/btrvZ3ZXa2l/QPMqp4Upau0rhOrzxET3K1/img.png)

⑦ New Project를 클릭한다.

![](https://blog.kakaocdn.net/dn/bRKhk8/btrv118rDk4/hVQUZSItscWHfxfck2yWG1/img.png)

⑧ Project Name을 지정하고 Next를 클릭한다.

![](https://blog.kakaocdn.net/dn/ck9rbp/btrvXUJvDZn/nK2REs0vXk1qOQ8MZKOquK/img.png)

⑨ Create Project를 클릭한다.

![](https://blog.kakaocdn.net/dn/kSxVw/btrv06hkxeK/w0v4TSHUfQJqLQNaX76fH1/img.png)

➉ Build a Cluster를 클릭한다.

![](https://blog.kakaocdn.net/dn/QViGB/btrvX8fTCgW/OVN4QgtBWRbMbUA7AcqqEk/img.png)

⑪ FREE라고 써진 옵션의 Create a cluster를 클릭한다.

![](https://blog.kakaocdn.net/dn/bjCbdx/btrv06Io1dP/I7bvr7SuD1MIzyLGsiMh2k/img.png)

⑫ Cloud Provider & Region에서 현재 위치에 가장 가까운 지역(한국에서는 Seoul)을 선택한 후 Create Cluster를 클릭한다. 이 과정은 시간이 조금 소요될 수 있다. 여기까지가 Atlas Cluster 생성 과정이다.

![](https://blog.kakaocdn.net/dn/bAvFiY/btrv127nDN8/0SoWMoNhkoX5G6EBdrmHH0/img.png)

⑬ IP 주소에 대한 액세스 권한을 부여하고 데이터베이스의 유저를 생성하는 과정이다. 다음 사진처럼 클러스터 화면에서 Connect를 선택한다.

![](https://blog.kakaocdn.net/dn/cRT7HQ/btrv3gqwQ3h/k6PmejNC2VjFFSKoIybThK/img.png)

⑭ Allow Access From Anywhere를 선택하고 Add IP Address를 클릭하여 선택사항을 확인한다.

그러고 나서 Create a Database User에 Username과 Password를 입력한다. 여기서 사용하는 Password는 차후 과정에서 사용되니 기억해두기.

(Allowing access from anywhere 는 보안상 위험할 수 있으므로 프로덕션 단계에서 사용되는 클러스터는 이 기능이 활성화되어있지 않아야 한다.)

![](https://blog.kakaocdn.net/dn/dDrkRM/btrvXTRns7s/tBxq7Qti7wYJoPh3vsqNdK/img.png)

⑮ Connect with the mongo shell을 선택한다.

✷ mongo shell

→ 정렬되지 않은 결과물 리스트를 리턴한다.

→ GUI 사용 없이 MongoDB 아틀라스 클러스터와 상호작용할 수 있다.

→ 자바스크립트 인터프리터로 작동한다.

![](https://blog.kakaocdn.net/dn/bUxJzK/btrvWF7dnms/UJKjn6VDjKHdapMVSFXxsK/img.png)

⑯ 사진에 나와있는 것은 예시. Connect with the mongo shell을 클릭했을 때 화면에 나오는 대로 cli에 명령어를 입력한다.

![](https://blog.kakaocdn.net/dn/qFWfS/btrvYwaBhm8/oXQcTei77BLrloWhdfvo6K/img.png)

⑰ 이미 설치되어 있어 연결할 경우 Run your connection string in your command line에 써있는 command를 터미널에 입력하기.

![](https://blog.kakaocdn.net/dn/bHsofQ/btrzpjMbldg/fxxAAqjo97UFZcC9GS8U90/img.png)
