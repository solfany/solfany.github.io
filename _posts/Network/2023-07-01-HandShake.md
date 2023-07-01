---
title: "[Network] 3way - HandShake & 4way - HandShake"
categories:
  - Network
tags: [Network]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

## **TCP 3-way Handshake 란?**

TCP는 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 three-way handshake를 사용한다.

**TCP 3 Way Handshake는 TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에**

**먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다..**

1단계 : Client > Server : TCP SYN

2단계 : Server > Client : TCP SYN ACK

3단계 : Client > Server : TCP ACK

여기서 SYN은 'synchronize sequence numbers', 그리고 ACK는'acknowledgment' 의 약자이다.

이러한 절차는 TCP 접속을 성공적으로 성립하기 위하여 반드시 필요하다.

## **TCP의 3-way Handshaking 역할**

- 양쪽 모두 데이타를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이타 전달이 시작하기전에 한쪽이 다른 쪽이 준비되었다는 것을 알수 있도록 한다.
- 양쪽 모두 상대편에 대한 초기 순차일련변호를 얻을 수 있도록 한다.

![img](https://t1.daumcdn.net/cfile/tistory/225A964D52F1BB6917)

## **TCP의 3-way Handshaking 과정**

**[STEP 1]**

A클라이언트는 B서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 A클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는SYN_SENT 상태가 되는 것이다.

**[STEP 2]**

B서버는 SYN요청을 받고 A클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 A가 다시 ACK으로 응답하기를 기다린다. 이때 B서버는 SYN_RECEIVED 상태가 된다.

**[STEP 3]**

A클라이언트는 B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것이다. 이때의 B서버 상태가 ESTABLISHED 이다.

위와 같은 방식으로 통신하는것이 신뢰성 있는 연결을 맺어 준다는 TCP의 3 Way handshake 방식이다.

## **4-way Handshaking**

3-Way handshake는 TCP의 연결을 초기화 할 때 사용한다면, 4-Way handshake는 세션을 종료하기 위해 수행되는 절차이다.

![img](https://t1.daumcdn.net/cfile/tistory/2152353F52F1C02835)

## **TCP의 4-way Handshaking 과정**

**[STEP 1]**

클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.

**[STEP 2]**

서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 **TIME_WAIT**상태다.

**[STEP 3]**

서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.

**[STEP 4]**

클라이언트는 확인했다는 메시지를 보낸다.

그런데 만약 "Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN패킷보다 늦게 도착하는 상황"이 발생한다면 어떻게 될까?

Client에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 데이터는 유실될 것이다.
