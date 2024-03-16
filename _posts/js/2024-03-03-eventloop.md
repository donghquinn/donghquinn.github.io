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

![Desktop View](assets/img/js/eventloop.png){: .shadow}
_Event Loop_

이벤트 루프란 무엇일까?

# Event Loop

이벤트 루프는 node.js의 기본적인 동작 방식이다.
Call Stack과 Callback Queue의 상태를 체크하여, Call Stack이 빈 상태가 되면 Callback Queue의 첫번째 콜백을 Call Stack으로 밀어넣는다. 이를 틱(Tick)이라 한다.

- Call Stack: 코드가 실행될 때 쌓이는 곳. Stack 형태로 쌓임. 함수를 실행하고 값을 **return 하면 call Stack에서 제거**된다.
- Callback Queue: 비동기적으로 실행된 콜백함수가 보관된 영역. eg. setTimeout에서 타이머 완료 후 실행되는 함수 등...

이벤트 루프는 총 6개의 단계를 가진다.

## 이벤트 단계

- Timer 단계

이벤트 루프의 시작 단계이다.

- Pending(I/O) 콜백 단계

- Idel, Prepare 단계

- Poll 단계

- Check 단계

- Close 단계

# microTaskQueue

이벤트 루프는 우선적으로 Microtask Queue를 먼저 확인한다.
MicroStack Queue에 콜백이 있다면 이를 먼저 Call Stack에 담는다.

# 참고 링크

- [JavaScript 비동기 핵심 Event Loop 정리](https://medium.com/sjk5766/javascript-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%95%B5%EC%8B%AC-event-loop-%EC%A0%95%EB%A6%AC-422eb29231a8)

- [Event Loop와 비동기](https://pozafly.github.io/javascript/event-loop-and-async/)
