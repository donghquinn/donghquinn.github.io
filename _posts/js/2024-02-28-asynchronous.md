---
title: 비동기란?
author: donghquinn
date: 2024-02-28 10:12:00 +0900
categories: [Javascript]
tags: [asynchronous]
comments: true
math: true
mermaid: true
# image:
#   path: /restapi.png
#   alt: RESTful API
---

![Desktop View](assets/img/js/async/async.png){: .shadow}
_Async/Await_

비동기란 무엇일까?

# 비동기

비동기는 하나의 동작이 완료되는 것을 기다리지 않고, 동시에 다른 작업을 처리하는 방식이다.

자바스크립트는 싱글 스레드 언어이기 때문에 필수 불가결적으로 비동기 함수를 선택하게 되었다.
하나의 스레드를 가지고 다른 작업이 마칠때까지 대기해야 한다면, 작업이 너무나도 느려지기 때문이다.
비동기 처리를 지원하는 방식으로는 Promise와 async/await이 있다.

## 예시

비동기 함수는 에어프라이어에 음식 넣고 돌린 후, 다른 재료를 손질하면서 틈틈이 에어프라이어를 체크하는 것과 유사하다.
에어프라이어가 음식을 조리하는 것이 완료될 때 까지 기다리는 것이 아닌, 동시에 다른 작업을 진행하는 것이다.

# 동기

동기는 하나의 동작이 완료된 후에 다음 동작으로 실행하는 **순차적** 방식이다.

# 개인적인 헷갈림 정리

처음에 비동기와 동기의 개념을 반대로 생각하고 있었다.
오히려 동기를 "병렬 처리"와 개념적으로 혼동하고 있었던 것이 크다.

동기는 "순차적", 비동기는 "동시에"라고 외워야 겠다.

- [참고 링크](https://yozm.wishket.com/magazine/detail/1982/)
