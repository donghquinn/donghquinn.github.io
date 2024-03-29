---
title: RESTful API란?
author: donghquinn
date: 2024-02-29 00:7:00 +0900
categories: [Backend]
tags: [RESTful, API]
comments: true
math: true
mermaid: true
# image:
#   path: assets/img/restapi.png
#   alt: RESTful API
---

![Desktop View](assets/img/backend/restapi.png){: .shadow }
_RESTful API_

백엔드 코드를 구현할 때 RESTful API 라는 개념이 자주 등장한다. 과연 이게 무엇일까

# API란?

우선 API가 무엇인지 이해를 해야 할 것 같다. API란 Application Programming Interface의 약자로, 다른 소프트웨어 시스템과 통신하기 위해 따라야 하는 규칙이다.
즉 데이터와 기능의 집합을 제공하여 프로그램 간 성호 작용을 통해, 정보를 교환 가능하도록 하는 것

# HTTP URI

리소스를 고유하게 식별하는 것, URL과 보통 혼용되고 있다.

- ex. www.example.com/font/2 에서 2가 리소스

# REST 란?

## 목표

1. 컴포넌트 간 확장성을 가진 상호 연동성 확보
2. 범용 인터페이스
3. 각 컴포넌트들의 독립적인 배포
4. 지연 감소, 보안 강화, 레거시 시스템을 인캡슐레이션 하는 중간 컴포넌트로의 역할
  - 인캡슐레이션: 데이터에 헤더가 추가되는 과정. 즉, 한 프로그램에서 다른 프로그램으로 데이터를 전송할 때 데이터를 패키지화 하는 과정

## 개념

REST는 Representational State Transfer(REST)의 약자로, API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처이다.
네트워크 상에서 Client와 Server 사이의 통신 방신 중 하나로, **자원을 이름으로 구분**하여 해당 **자원의 상태를 주고 받는 모든 것**을 의미하는 것이다.
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

## REST 특징

- 클라이언트 / 서버 구조
  - 클라이언트는 유저 관련 처리, 서버는 REST API 제공으로 역할 분리
  - 때문에 서버와 클라이언트 간 의존성이 줄어든다.
    - REST Server: API 제공, 비즈니스 로직 처리 및 저장
    - Client: 사용자 인증 / Context(세션, 로그인 정보) 등을 직접 관리 및 책임

- 무상태성 (Stateless)
  - 서버에서 어떤 작업을 하기 위해 상태 정보를 기억할 필요가 없고, 들어온 요청에 대해 처리만 해주면 된다.

- 캐시 처리 가능 (Cacheable)
  - HTTP 웹 표준을 사용하기에, 기존 웹 인프라를 그대로 사용
  - 대량의 요청을 효율적으로 처리. 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상

- 자체 표현 구조 (Self- Descriptiveness)
  - JSON을 이용한 메세지 포맷을 이용해 요청에 대한 이해가 쉽다

- 계층화
  - 클라이언트와 서버가 분리되어 있기 때문에, 프록시 서버 / 암호화 계층 등 중간매체를 사용할 수 있음

- 유니폼 인터페이스
  - HTTP 표준에만 따른다면 모든 플랫폼에서 사용 가능하며, 리소스 조작이 통일되기 때문에 **특정 언어나 기술에 종속되지 않는다**

# RESTful API란?

REST 기반으로 API를 구현한 것을 RESTful 웹 서비스라고 지칭한다.
확장성과 재사용성을 높여 유지보수 및 운용의 편리성을 확보할 수 있다.
개인적으로 정의하자면, 통신의 표준화라고 생각한다.

# 규칙

1. 슬레시(/)는 계층 관계를 나타내는데 사용한다.
2. URI 마지막 문자로 슬레시(/)는 사용하지 않는다.
3. 하이픈(-)은 URI 가독성을 높이는데 사용한다.
4. 밑줄 (_)은 URI에 사용하지 않는다.
5. URI는 최대한 소문자를 사용한다.
6. 파일 확장자는 URI에 포함하지 않는다.

# 참고 링크

- [REST, REST API, RESTful 특징](https://hahahoho5915.tistory.com/54)
