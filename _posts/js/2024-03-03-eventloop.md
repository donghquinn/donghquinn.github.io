---
title: 이벤트 루프 란?
author: donghquinn
date: 2024-03-03 12:28:00 +0900
categories: [Javascript]
tags: [javascript, eventloop, nodejs, backend]
comments: true
math: true
mermaid: true
---

<img src="assets/img/eventloop.png"/>
<em>Event Loop</em>

이벤트 루프란 무엇일까?

# Event Loop

이벤트 루프는 node.js의 기본적인 동작 방식이다. 총 6개의 단계를 가진다.

## 이벤트 단계

- Timer 단계

이벤트 루프의 시작 단계이다. 

- Pending(I/O) 콜백 단계

- Idel, Prepare 단계

- Poll 단계

- Check 단계

- Close 단계

# nextTickQueue & microTaskQueue
