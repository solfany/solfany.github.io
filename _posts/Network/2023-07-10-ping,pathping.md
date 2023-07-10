---
title: "[Network] Well-Known Port 번호"
categories:
  - Network
tags: [Network]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

# ping, pathping tracert

```bash
	ping icqa.or.kr
```

![image](https://github.com/solfany/solfany.github.io/assets/123814718/dc171aac-b10d-4f7d-a065-41b206f28675)

ping 명령어를 이용하여 목적지([www.icqa.or.kr](http://www.icqa.or.kr/))와 정상적으로 통신되었을 확인하였다.

> 위의 기능은 ICMP 을 사용한 방법
> Internet Control Message Potocol
> 에러보고 목적으로 만들어짐

---

```bash
	pathping icqa.or.kr
```

![image](https://github.com/solfany/solfany.github.io/assets/123814718/67c7a108-385d-40d8-806d-392777480db9)

1번은 라우터 + 게이트웨이 주소

> 절달되는데 몇초가 걸렸고, 어떤 문제가 있는지 통계적으로 보여주며, 세밀한 확인이 가능하다.
> ping 명령어 보다 구체적인 명령어이다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/0514d325-3311-4fac-9516-0da6c384cc3e)

> 게이트웨이 등 구체적인 부분이 나열된다.
> 출발지 - 목적지 경로를 나타낸다.

---

```bash
tracert icqa.or.kr
```

![image](https://github.com/solfany/solfany.github.io/assets/123814718/432bcca1-5a31-4bc3-bc24-78777c5d4e88)

최적의 경로를 찾아줌

> 마찬가지로 1번이 내가 소속되어있는 게이트웨이 주소이다.
> 어떤 경로로 가든 목적지 까지 가장 빠른 방법으로 도착한다.
> 실시간 교통상황 반영하는 네비게이션과 비슷하다.

내가 사용하는 건 라우터 = 공유기 =

목적지는 마지막 , 위의 사진으로 치면 7번 째 가 공유기 주소가 된다.
