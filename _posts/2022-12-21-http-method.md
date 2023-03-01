---
layout: single
title: "[HTTP Method] PUT vs PATCH"
categories: HTTP
tag: [기록, http, put, patch, 멱등성]
author_profile: false
---

put과 patch의 차이.

## 개요

수강생 시절에도 배웠던 내용들이지만, 요즘 개발을 하면서 더욱 잘 알 필요성이 느껴져 글로 작성하게 되었다.

put과 patch가 수정할 때 사용하는 http 메소드라는 것은 어렴풋이 알고 있었다. 하지만 둘의 차이점을 경험하지 못했다.

수강생 시절에 진행했던 프로젝트에서는 수정 요청을 받을 때마다 patch 메소드만을 사용해왔기 때문이다.

그러나 현재 진행하고 있는 개발에서 put과 patch 메소드 사용에 명확한 이유가 있어야 했다.

## 정의

put: 요청 페이로드를 사용해 새로운 리소스를 **생성**하거나, 대상 리소스를 나타내는 데이터를 **대체**합니다.

patch: 리소스의 **부분적인 수정**을 할 때에 사용됩니다.

## PUT의 실질적인 사용

```javascript
// User Entity
{
  "name": "Haley",
  "age": 18
}
```

다음과 같은 유저 엔티티(편의성을 위해 원본 데이터라고 칭함)가 있다고 가정하자.

만약 put 메소드를 사용하여 이름'만' 수정한다고 해보자.

```javascript
PUT /users?id=1
{
  "name": "Emily", // "Haley" -> "Emily"로 변경
}
```

이렇게 이름만 변경 요청을 했을 때,

```javascript
PUT /users?id=1
{
  "name": "Emily",
  "age": null
}
```

age는 null이 되었다. 보내지 않은 값이 nul이 된 것이다.

다시 말해, 앞서 언급한 put의 정의처럼 '대상 리소스를 나타내는 데이터를 대체'한 것이다.

제대로 된 요청을 보내려면,

```javascript
PUT /users?id=1
{
  "name": "Emily",
  "age": 20
}
```

다음과 같이 요청을 보내주어야한다.

## PATCH의 실질적인 사용

그렇다면 patch 요청은 어떻게 보내줄 수 있을까?

상단에 작성한 원본 데이터를 그대로 가져왔다고 가정하고 시작한다.

```javascript
// User Entity
{
  "name": "Haley",
  "age": 18
}
```

```javascript
PATCH /users?id=1
{
  "name": "Emily"
}
```

```javascript
PATCH /users?id=1
{
  "name": "Emily",
  "age": 18
}
```

patch는 부분을 교체하기 때문에 name만 수정 요청을 보냈지만 age의 값은 그대로 남아있다.

## 이런 경우?

작성하다보니 여기서 의문점이 하나 생기기 시작했다. 만약 요청한 URI에 자원이 존재하지 않으면 put과 patch는 각각 어떻게 응답을 보내줄까?

```javascript
PUT /users?id=2

{
  "name": "Leah",
  "age" : 21
}
```

| id  | name  | age |
| :-: | :---: | :-: |
|  1  | Emily | 20  |
|  2  | Leah  | 21  |

이렇게 새로운 자원을 생성한다.

```javascript
PATCH /users?id=2

{
  "name": "Leah",
  "age" : 21
}
```

| id  | name  | age |
| :-: | :---: | :-: |
|  1  | Emily | 20  |

patch는 새로운 자원을 생성하지 않고, 서버는 응답에 오류를 보내준다.

## 멱등성

위에서 보았듯, PUT과 PATCH는 멱등성의 관점에서 차이를 보인다.

그렇다면 멱등성은 무엇일까?

멱등성의 정의를 검색하면, 동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때, 해당 HTTP 메서드가 멱등성을 가졌다고 말합니다...라고 나온다.

즉, 이 말은 서버로 요청을 여러 번 날리는 행위와 한 번 날리는 행위가 같은 결과를 내면 멱등성이 있다고 말할 수 있다.

(이 부분에 대해 더 많은 검색을 해보고, 내가 정리해두었던 [블로그 정리본](https://hsly22xk.tistory.com/104)을 본 결과, put은 멱등성을 가지지만, patch는 멱등성을 가지지 않는다.)

## 멱등성을 보여주는 예시

그렇게 넘어가려다보니, put과 patch가 멱등성의 차이가 있다는 것은 알겠는데, patch 또한 멱등성이 있는 것'처럼' 작동하는 것 같아 보였다. 실제로는 그렇지 않음에도.

그래서 내가 작성한 예시를 살펴보았다. patch 요청도 서버에 계속 날렸을 때 같은 값을 리턴하지 않나 하는 생각이 들었다.

| id  | name  | age |
| :-: | :---: | :-: |
|  1  | Emily | 20  |
|  2  | Leah  | 21  |

이 리소스는 /users URI를 통해 접근하는 것으로 가정했다.

그렇다면 /users 자체에 요청을 보내는 경우로 가정해보면 어떻게 될까.

```javascript
PATCH /users
// 해당 PATCH 요청을 똑같이 '2번' 보내준다.

{
  "name": "Leah",
  "age" : 21
}
```

첫번째↓

| id  | name  | age |
| :-: | :---: | :-: |
|  1  | Emily | 20  |
|  2  | Leah  | 21  |

두번째↓

| id  | name  | age |
| :-: | :---: | :-: |
|  1  | Emily | 20  |
|  2  | Leah  | 21  |
|  3  | Leah  | 21  |

첫번째와 두번째 요청을 모두 같이 보내주었음에도 불구하고 결과가 다르게 도출된다.

이렇게 put과 patch의 차이를 알아보았다.

어떤 상황에서 사용해야하는지, 그리고 멱등성의 차이가 어떤 것인지 이번 정리를 통해 명확하게 알 수 있었다.
