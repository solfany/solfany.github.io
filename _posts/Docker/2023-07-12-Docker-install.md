---
title: "[Docker] 도커 란?"
categories:
  - Docker
tags: [Docker]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

![img](https://mblogthumb-phinf.pstatic.net/MjAxNzA0MTFfMjIy/MDAxNDkxOTIwOTA0NDIz.OixMjEJC1MWVlM_jFn-ELElnHT8ueLeGYX3yxRz0fRYg.IzQlW_BpIgBUlXUlKcd1ZsZMC1LYcCc48X_Ia_aIdtog.PNG.complusblog/%EB%8F%84%EC%BB%A4.png?type=w800)

# 도커 설치하기

홈페이지에서 다운받기

## **도커 다운로드(docker desktop)**

아래 링크에 접속해서 설치.

https://www.docker.com/products/docker-desktop/

![img](https://blog.kakaocdn.net/dn/dWGUip/btr1IKu6cGy/sNDaJA7cJMVIpQmp47QBy1/img.png)

정상적으로 설치 되었는지 확인해보기

```bash
docker -v
```

<br>
<hr>

## 도커 허브에서 이미지 다운받기

https://hub.docker.com/

![image](https://github.com/solfany/solfany.github.io/assets/123814718/d0775555-00b1-433d-b584-1d07fc5aeb3e)

해당 주소에서 상단 검색 창에 원하는 이미지 검색

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/94483bc0-517e-4c11-8e44-66e4377010b2)

검색 후 좌측 회색 박스의 **docker pull** 명령어를 통해 이미지 다운받기

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/20fc5722-d5e0-4887-b2f6-b12d373aa1b4)

터미널에 입력하면 해당 이미지를 다운받겠다 라는 뜻이다.
중요한 점은 해당 명령어 뒤에 :{version} 을 입력해야 한다는 것 !

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/b1256c5e-bb2d-4783-ad57-284d7995ac0f)

버전 정보는 위의 이미지에서 확인이 가능하다.
위의 버전 중 원하는 버전을 {} 해당 괄호 대신 붙이면 된다.

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/042f8dda-c3c4-455d-8f22-20a2dbe43a16)

나는 latest 버전을 다운 받았고!
다운받을 때 주의할 점은 Docker가 실행되고 있어야 다운이 가능하다!

<br>
<hr>

## 도커 컨테이너 실행 및 생성

```bash
//도커를 실행하겠다. 생성할 컨테이너 이름
docker run --name mysql-sample-contatiner -e

//비밀번호 설정, 3306포트로 연결하겠다.
MYSQL_ROOT_PASSWORD=<password> -d -p 3306:3306 mysql:{version}
```

위의 명령어를 수정해서 입력해주겠다.

<br>

```bash
docker run --name mysql-test-container -e
MYSQL_ROOT_PASSWORD=test -d -p 3306:3306 mysql:latest
```

password 부분과 컨테이너 이름, 컨테이너 이미지 버전 부분을 수정해줬는데,

기억하기 쉬운 비밀번호로 변경과 버전은 다운 받은 버전을 입력했다.

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/8e038738-4d43-4b09-8751-f625a6686a04)

컨테이너 생성 성공 화면

<br>
<hr>

## 현재 실행중인 도커 커테이너 목록 출력

```bash
docker ps -a
```

<br>
<hr>

## 도커 컨테이너 접속하기

```bash
docker exec -it{도커 컨테이너 이름}bash

```

위의 기본 명령어를 기반으로 나는 컨테이너 이름을 변경했기 때문에

<br>

```bash
docker exec -it mysql-test-container bash
```

해당 명령어를 입력해주었다.

<br>

![image](https://github.com/solfany/solfany.github.io/assets/123814718/d50c3330-9e9d-4185-bf10-5447f4d51a52)

접속이 성공적으로 이루어지면 위의 명령어를 반환한다.

<br>
<hr>

## MySQL 접속

```bash

mysql -u root -p
```

위의 명령어를 입력하고 이전에 설정했던 패스워드를 입력하면 mysql로 접속을 할 수 있다

![image](https://github.com/solfany/solfany.github.io/assets/123814718/30455b2c-52a9-4e65-bc1f-d554ef61b8d0)

정상적으로 mysql에 접속이 된 화면이다.

<br>

## 만들어둔 컨테이너 sql 재 접속

```bash
// 도커 컨테이너 접속하기
docker exec -it {도커 컨테이너 이름}bash

// mysql
mysql -u root -p
```

입력 후 패스워드 입력하면 만들어둔 컨테이너에 다시 로그인 할 수 있다!
