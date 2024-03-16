---
title: 쿠키와 세션
author: donghquinn
date: 2024-03-04 02:28:00 +0900
categories: [Backend]
tags: [cookie, session]
comments: true
math: true
mermaid: true
# image:
#   path: assets/img/rdb.png
#   alt: RDB
---

유저 로그인 인증 등에 사용되는 세션과 쿠키는 무엇일까?

# Cookie

쿠키는 클라이언트의 브라우저에 저장되는 영속성 정보이다.
유저 아이디, 선택한 테마 등을 저장해 두고 요청시 마다 쿠키를 담아 보내어, 매번 로그인할 필요 없게 할 수 있다.
이는 무상태성(Stateless)인 HTTP 요청 특성에 따라 상태를 담아 보낸다고 이해하면 좋을 것 같다.

<img src="assets/img/backend/cookieSession/cookie.png" />
<em>Cookie 예시</em>

- 단점

그러나 쿠키는 탈취당하면 유저 인증 상태를 공격자에게 넘겨주는 것이므로, 모든 권한을 빼앗기게 될 수 있다.

# Session

세션은 쿠키와 달리 접속 상태를 서버에 저장한다.
클라이언트에 유일한 세션 ID 를 부여하고, 쿠키에 담아 돌려준다.
그러나 서버에서 모든 정보를 가지고 있기 때문에, 분산 처리에 불리하며 메모리 사용량이 많아진다.

<img src="assets/img/backend/cookieSession/session.png" />
<em>Session 예시</em>

# 세션과 쿠키의 차이

둘의 가장 큰 차이는 정보의 저장 위치이다.
쿠키는 브라우저에, 세션은 서버에 저장한다는 것이 큰 차이이다.

<img src="assets/img/backend/cookieSession/session_cookie_diff.png" />
<em>세션과 쿠키의 차이</em>

# 참고 링크

- [인증/보안 (쿠키, 세션)](https://velog.io/@hihijin/Backend-%EC%9D%B8%EC%A6%9D-%EB%B3%B4%EC%95%88-%EC%BF%A0%ED%82%A4%EC%84%B8%EC%85%98)
