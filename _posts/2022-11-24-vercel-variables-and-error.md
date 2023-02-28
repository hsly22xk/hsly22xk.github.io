---
layout: single
title: "[Vercel] Environment Variables & Mixed Content"
categories: React
tag: [기록, vercel, 배포]
author_profile: false
---

vercel 배포 시 환경변수 설정과 mixed content 에러.

## 개요

제일 처음 vercel에 배포를 했을 때, 조회 화면이 제대로 뜨지 않고 request url의 형태가

http://나의vercel배포주소/undefined/내가지정한params

의 형태로 떴다. 처음엔 내가 지정해준 주소는 .env의 서버 주소인데, 왜 내가 vercel로 배포한 도메인이 앞에 나올까 감이 잡히지 않았다.

다행히 지금의 나에게는 도움을 요청할 사람들이 많이 생겼기 때문에, 물어봤다. 물론, 그 전에 구글링을 선행하긴 했지만 내가 원하는 대답은 제대로 나오지 않았다.

## add environment variables

내가 처음 작성했던 코드는

```javascript
axios.post(`${process.env.REACT_APP_URL}/post`, {
 ...이하 생략
})

... 이하 코드들 전부 생략 ...
```

같은, 환경변수에서 URL을 가져오는 방식이었는데 vercel로 배포하면서 저 환경변수가 제대로 읽혀지지 않은 것이었다.

조금 더 구글링을 해보니 vercel에서 배포를 할 때는 .env를 읽어오지 못하고 내가 직접 등록해준 값을 읽어오는 방식이었다.

그래서 배포 과정에서 environment variable을 key-value에 맞게 add해주고 deploy해주었을 때 해결할 수 있었다.

## Mixed Content Error

[(링크)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/mixed-content.html?lang=ko-KR)

```javascript
Mixed Content: The page at 'https://' was loaded over HTTPS,
but requested an insecure script 'http://'.
This request has been blocked; the content must be served over HTTPS.
```

(https, http 뒤에 붙은 상세 링크는 일부러 지웠음)

https에서 ajax를 사용해서 비동기로 http에 request를 날려 발생한 에러 메시지다.

즉, https사이트에서 http로 리소스를 로드하도록 요청을 받아 Mixed Content가 발생한 것이다.

이 부분에 대한 해결은

```javascript
public/index.html

<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```

index.html파일의 <head>태그 안에 상기 코드 한 줄을 추가해주면 에러 메시지가 사라졌다.

하지만 이 코드에는 문제가 있었다.

해당 코드는 모든 non-ssl 사이트를 ssl로 강제 전환시켜주는 코드이기 때문에, 배포를 하고 조회를 했을 때는 콘솔창에 Mixed content 에러가 뜨지는 않지만 환경변수에서 http로 지정해주었던 url을 강제로 https로 바꿔버려, 화면 조회가 되지 않는 것이다.

그래서 해당 코드는 주석 처리해준 후, 크롬 설정에서 개인정보 및 보안 - 안전하지 않은 콘텐츠 옵션을 차단에서 허용으로 바꿔주는 방식으로 해결했다.

사실 이렇게 하면 여전히 콘솔창에 경고 메시지로 Mixed content 메시지가 뜬다. 그렇기 때문에 완전무결한 해결책은 아닌 것 같지만, 어쨌든 서버에서 데이터를 받아와 페이지 조회가 되고 구현했던 기능도 잘 돌아가는 중이다.

+)23.01.04)

전에 작성했던 글을 읽어보면서, 사실 배포를 할 때 http가 아닌 https로 배포를 하는 것이 일반적인 경우가 되기도 했고, 보안상으로도 안전하다. 그렇기 때문에 처음부터 https로 배포를 하는 것이 맞지 않을까 하는 생각을 하게 되었다.
