---
layout: single
title: "D+56(57) MVC design pattern"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

mvc pattern.

## mvc pattern

[mvc pattern(1)](https://bsnippet.tistory.com/13)

[mvc pattern(2)](https://m.blog.naver.com/jhc9639/220967034588)

model-view-controller.

소프트웨어가 돌아가는 방식에 대한 하나의 디자인 패턴.

→ 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 소프트웨어 디자인 패턴

→ 어떤 특정한 역할들에 대해 역할분담을 할 때 가이드라인을 제시하는 방법 중 하나

→ 서비스 처리들을 각각 기능별로 나누게 됨으로써 프로그래밍을 할 때 하나의 코드베이스에서 모든 것들을 하는 것이 아닌 정돈된(의도된) 코드를 특정 역할에서 할 수 있게 한다.

⇒ 코드 가독성, 관리성, 코드 퀄리티, 협업 등의 모든 것이 좋아진다.

ex) Express, Angular, Django, Flask 등

![](https://blog.kakaocdn.net/dn/caxpRE/btrvy2s1to8/HqietD0yRuEV8FarwZzwE0/img.png)

브라우저에서 유저의 액션들이 일어나면 라우터 쪽으로 특정 엔드포인트들을 라우팅(분기), 각 라우터는 라우팅 엔드포인트에 맞는 컨트롤러 함수를 부른다.

컨트롤러는 데이터를 뷰로 바로 보내줄수도 있고, 모델을 거쳐 모델이 데이터베이스와 소통하여 다시 데이터를 받아 뷰로 보내줄 수도 있음.

```
‣ Browser → Router → Controller → View → Controller → Browser

‣ Browser → Router → Controller → Model → DB → Model → Controller → View
  → Controller → Browser
```

![](https://blog.kakaocdn.net/dn/DDZ7e/btrzhpy4Pc6/K8DwbI30KhBnrqn7lrWFLk/img.png)

### ① Model(데이터베이스의 모델하우스)

애플리케이션의 데이터(정보)를 가진 객체. 이런 집이 지어질 것이다 보여주는 모델하우스처럼, 데이터베이스가 이렇게 만들어질 것이라는 것을 보여주는 것.

→ 자신이 그 데이터를 갖고 있을 수도 있고, 데이터베이스와 연결이 되어 데이터를 가지고 올 수도 있음.

### ② View

유저가 보는 화면을 보여주게 하는 역할.

→ 사용자 인터페이스 요소를 나타냄.

→ Controller와'만' 소통함. Model / Database와 직접 접근이 없음.

⇒ 무언가 데이터를 받으면 그것을 그리는 역할에 충실한 모델.

### ③ Controller(=== API)

View에서 일어나는 action과 event의 input값을 받음.

→ Model에게 데이터를 넘겨주기 전에 일련의 가공 과정을 거쳐 가공된 데이터를 넘겨줌.

→ 데이터와 비즈니스 로직 사이의 상호동작을 관리

```js
// pesudo code
// 일종의 의사코드

// 특정 엔드포인트로 get request 요청을 보냄
http://www.abcd.com/users/profile/1

// Users라는 컨트롤러의 getProfile함수를 실행한다
/routes
  users/profile/:id=Users.getProfile(id)


/controllers
  class Users {
    function getProfile(id) {

      // 유저모델(/models)에 있는 getProfile을 부른 후
      profile = this.UserModel.getProfile(id)

      // View로 보내주게 됨
      renderView('users/profile', profile)
  }

/models
  class UserModel {
    function getProfile(id) {

      // 실제 데이터베이스에 접근,
      // 특정 조건이 걸린 쿼리문으로 id값을 받아와 그에 해당하는 데이터값을 받아오고
      // 데이터를 리턴함
      data=this.db.get('SELECT * FROM users WHERE id=id')
      return data;
  }

// 받은 데이터들을 다이나믹하게 이용하여 그려주는 역할을 함
/views
  /users
    /profile
    <h1>{{profile.name}}</h1>
    <ul>
      <li>{{profile.email}}</li>
      <li>{{profile.phone}}</li>
    </ul>
```

[배치 모드(batch mode)](https://velog.io/@southbig89/10%EC%9B%94-16%EC%9D%BC-%ED%86%A0-MySQL-%EB%B0%B0%EC%B9%98%EB%AA%A8%EB%93%9C)
[✷ 배치 모드(batch mode)](https://dev.mysql.com/doc/refman/8.0/en/batch-mode.html)
