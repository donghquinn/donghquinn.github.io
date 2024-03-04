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

<img src="assets/img/cookie.png" />
<em>Cookie 예시</em>

- 단점

그러나 쿠키는 탈취당하면 유저 인증 상태를 공격자에게 넘겨주는 것이므로, 모든 권한을 빼앗기게 될 수 있다.

# Session

세션은 쿠키와 달리 접속 상태를 서버에 저장한다.
클라이언트에 유일한 세션 ID 를 부여하고, 쿠키에 담아 돌려준다.
그러나 서버에서 모든 정보를 가지고 있기 때문에, 분산 처리에 불리하며 메모리 사용량이 많아진다.

<img src="assets/img/session.png" />
<em>Session 예시</em>

# 세션과 쿠키의 차이

둘의 가장 큰 차이는 정보의 저장 위치이다.
쿠키는 브라우저에, 세션은 서버에 저장한다는 것이 큰 차이이다.

<img src="assets/img/session_cookie_diff.png" />
<em>세션과 쿠키의 차이</em>

# RDBMS(Relational Database Management System)

관계형 데이터베이스를 생성하고 수정하여 관리하는 소프트웨어

- 모든 데이터를 2차원 테이블로 표현
- DB 레코들을 CRUD 연산할 수 있게 하는 소프트웨어
- 테이블은 row (record, tuple)과 column(field, item)으로 이뤄진 기본 데이터 저장 단위
- 상호관련성을 가진 테이블 집합
- 데이터베이스 설계도를 E-R(Entity Relationship) 모델로 표현
- MariaDB, Mysql, PostgreSQL... 등이 포함됨

## CRUD 작업

- Create: 생성 - INSERT
- Read: 읽기 - SELECT
- Update: 업데이트 - UPDATE
- Delete: 삭제 - DELETE
