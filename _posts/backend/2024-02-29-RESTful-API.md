---
title: RESTful API란?
author: donghquinn
date: 2024-02-29 00:7:00 +0900
categories: [Backend]
tags: [RESTful, API]
comments: true
math: true
mermaid: true
image:
  path: /docker-logo-blue.png
  alt: Docker logo
---

백엔드 코드를 구현할 때 RESTful API 라는 개념이 자주 등장한다. 과연 이게 무엇일까

##  API란?

우선 API가 무엇인지 이해를 해야 할 것 같다. API란 Application Programming Interface의 약자로, 다른 소프트웨어 시스템과 통신하기 위해 따라야 하는 규칙이다.
즉 데이터와 기능의 집합을 제공하여 프로그램 간 성호 작용을 통해, 정보를 교환 가능하도록 하는 것

## REST 란?

REST는 Representational State Transfer(REST)의 약자로, API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처이다.
네트워크 상에서 Client와 Server 사이의 통신 방신 중 하나로, 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것을 의미하는 것이다.
HTTP Method (POST, GET, PUT, DELETE)를 통해 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

- 자원: 해당 소프트웨어가 관리하는 모든 것
  - 문서, 그림, 데이터, 소프트웨어 자체 등...

- 자원의 이름(자원의 표현)
  - 학생 정보가 자원일 때, 'student'를 자원의 표현으로 정한다.

- 상태 전달
  - 데이터가 요청되는 시점의 자원의 상태를 전달
  - 일반적으로 JSON 혹은 XML 포맷을 통해 주고받는다.

- CRUD Operation
  - Create: 생성 (POST)
  - Read: 조회 (GET)
  - Update: 수정 (PUT)
  - Delete: 삭제 (DELETE)
  - HEAD: header 정보 조회 (HEAD)

## RESTful API란?

REST 기반으로 API를 구현한 것을 RESTful 웹 서비스라고 지칭한다.
확장성과 재사용성을 높여 유지보수 및 운용의 편리성을 확보할 수 있다.
