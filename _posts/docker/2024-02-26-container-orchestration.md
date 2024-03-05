---
title: 도커 컴포즈와 도커 스웜을 이용한 오케스트레이션
author: donghquinn
date: 2024-02-26 05:50:00 +0900
categories: [Docker, Orchestration]
tags: [docker, docker-compose, docker-swarm]
comments: true
math: true
mermaid: true
# image:
#   path: assets/img/docker.png
#   alt: Docker Logo
---

<img src="assets/img/docker/docker.png" />
<em> Docker Logo </em>

# 컨테이너 오케스트레이션

도커로 컨테이너를 구동해 프로세스를 분리 시키고 구동한다.
그런데 만약 구동해야 할 필수 컨테이너의 개수가 많고 한번에 제어를 해야 한다면, 관리가 매우 힘들 수 있다. 이런 경우 많이 사용하는 것이 컨테이너 오케스트레이션이다.

가장 유명한 툴은 kubernetes(k8s)이고, 도커에서도 자체적으로 제공하는 오케스트레이션 기능이 바로 도커 스웜이다.
