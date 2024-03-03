---
title: 암호화
author: 
  name: donghquinn
  link: https://github.com/donghquinn
date: 2024-03-03 04:30:00 +0900
categories: [Backend]
tags: [crypto, md5, hash, sha, seed]
comments: true
math: true
mermaid: true
# image:
#   path: assets/img/restapi.png
#   alt: RESTful API
---

보안을 위해서라면 암호화는 중요하다.

# 해시 계열

## 해시(Hash)

해시는 암호화 과정이라고 하기에는 어렵고 보안이 이미 뚫린 바가 있으나,
암호화 기법과 함께 사용하여 시너지를 발휘할 수 있다.

<img src="assets/img/hash.png" />

- 임의의 크기를 가진 데이터를 하나의 고정된 데이터로 변환시킨 것
- 예시: "12345" -> 고정 길이 해시 값 

## MD5 (Message Digest algorithm 5)

RFC1321로 지정된 128비트의 해시 함수. 본 데이터가 다를지라도 같은 해시 값이 생성(충돌) 되고 이미 보안이 뚫린 바가 있기에, 보안 관련 용도로는 사용하지 않음.

- 원프로그램 / 파일 무결성 검사할 때 사용
- 32개의 16진수로 이루어진 해시 값 생성 (16^32)

## SHA (Secure Hash Algorithm)

서로 관련된 암호학적 해시 함수들의 모음.

- TLS, SSL, PGP, SSH, IPSec 등 많은 보안 프로토콜에서 채택
- 원본 데이터의 작은 변화에도 해시 값의 변동이 매우 큼
- SHA-2 계열 알고리즘은 현재까지 많이 쓰이고,SHA-256 / SHA-512가 널리 쓰임

# 암호화 알고리즘

## Adaptive Key Derivation Dunction

- 다이제스트(해시화된 데이터)를 생성할 때 **Salting**과 **Key-Stretching**을 반복하여 공격자가 유추할 수 없게 보안의 강도를 선택할 수 있는 함수

- Salting: 해시 함수 실행 전 원문에 임의의 문자를 덧붙여 보안성을 높이는 기법

- Key-Stretching: 입력한 패스워드의 다이제스트를 생성하고, 생성된 다이제스트를 입력값으로 하여 다이제스트를 생성하는 것을 반복하는 기법

### PBKDF2 (Password-Based Key Derivation Function)

해시 함수의 컨테이너 역할을 하는 함수

- 검증된 해시함수만을 사용
- 해시함수와 salt를 적용하여 해시함수의 반복 횟수를 지정하여 암호화
- 가장 많이 사용되는 ISO 표준에 적합한 알고리즘

### Bcrypt

패스워드 해싱 함수 (Blowfish 암호 기반)

- 현재까지 가장 강력한 암호화 알고리즘
- 해시화 반복횟수를 늘려 연산속도를 늦출 수 있어, 연산 능력이 강화된 Brute-Force 공격에 대비 가능

- Blowfish 알고리즘

  - 32비트 ~ 448비트의 가변길이의 키를 이용하는 비밀키 블록암호

- Brute-Force

  - 랜덤한 값을 무차별적으로 대입하여 해시 알고리즘의 원본 데이터를 알아내는 공격 기법

Scrypt

PBKDF2와 유사한 함수

- 다이제스를 생성할 때 메모리 오버헤드를 갖도록 설계되어 Brute-Force 시도 시 병렬화 처리 어려움
- Bcrypt보다 더 경쟁력 있다고 평가 됨

### Seed

한국인터넷진흥원(KISA)에서 개발한 128비트의 대칭키 블록 암호 알고리즘
