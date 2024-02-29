---
title: 도커와 도커 컴포즈와 설치에 관하여
author: donghquinn
date: 2024-02-26 05:32:00 +0900
categories: [Docker]
tags: [docker, docker-compose]
comments: true
pin: true
math: true
mermaid: true
image:
  path: assets/img/docker-logo-blue.png
  alt: Docker logo
---

도커를 사용하는 방법은 도커 CLI를 사용하거나 컴포즈를 사용하는 것이다.

## 도커 설치

### 운영체제 패키지 업데이트

```shell
sudo apt-get update
```

### 필수 요소 설치

```shell
sudo apt-get install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg \
  lsb-release -y
```

### 도커 GPG 키 설치

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Stable 버전 도커 설치

```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 도커 엔진 설치

```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```

### 버전 확인

```shell
docker version
```

## 도커 컴포즈는 뭔데?

도커 컴포즈는 컨테이너 이미지를 빌드하고, 컨테이너 설정을 미리 할 수 있는 설계도이다.
빌드할 도커 파일을 설정하고, 컨테이너 이름 및 공개할 포트 번호, 네트워크 등을 미리 설정할 수 있다.

### 도커 컴포즈 설치

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/v2.9.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### 실행 권한 부여

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

### 버전 확인

```shell
docker-compose --version
```
