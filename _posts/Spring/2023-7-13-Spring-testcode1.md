---
title: "[Spring MVC]테스트 코드를 작성하는 이유"
categories:
  - Spring
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

1. 문서화 역할
2. 코드에 결함을 발견하기 위함
3. 리팩토링 시 안정성 확보
4. 테스트 하기 쉬운 코드를 작성하다 보면 더 낮은 결함도를 가진 설계를 얻을 수 있음

## TDD

(Test Driven Development : 테스트 주도 개발)

- 프로덕션 코드보다 테스트 코드를 먼저 작성하는 개발 방법
- TFD(Test First Development) + 리팩토링
- 기능 동작을 검증 (메소드 단위)

## BDD

(Behavior Driven Development : 행위 주도 개발)

- 시나리오 기반으로 테스트 코드를 작성하는 개발 방법
- 하나의 시나리오는 Given, When, Then 구조를 가진다.
