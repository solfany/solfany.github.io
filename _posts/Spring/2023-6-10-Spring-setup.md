---
title: "[Spring MVC] 개발 환경 세팅"
categories:
  - Spring
tags: [Spring]
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## 1. 개발 도구 설치 & 설정

### VS Code

설치 - https://code.visualstudio.com/download

- 유용한 플러그인 - https://marketplace.visualstudio.com/VSCode한글 팩 - https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ko
- open in browser - https://marketplace.visualstudio.com/items?itemName=techer.open-in-browser
- Prettier - Code formatter - https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode
- indent-rainbow - https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow
- 태그이름 자동변경 - https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag

### git 설치

[Windows] https://git-scm.com/download/win
[Mac] 먼저 terminal열고, 아래와 같이 입력하고 엔터

`$ git`

'git'명령어는... 도구를 설치하시겠습니까?라고 묻는 창이 열리면 '설치'를 클릭.(몇분 소요) 설치 완료 후, 아래와 같이 입력후 엔터.

`$ git --version\
git version 2.28.0`

위와 같이 나오면 설치가 잘된 것입니다. 버전이 조금 달라도 괜찮

### JDK11 설치

[자바의 정석 - 무료강의] https://youtube.com/playlist?list=PLW2UjW795-f6xWA2_MUhEVgPauhGl3xIp

[Windows] https://download.java.net/java/ga/jdk11/openjdk-11_windows-x64_bin.zip

[Mac] SDKMAN을 이용해서 openJDK설치

- SDKMAN 설치 - https://sdkman.io/install

```bash
 $ curl -s "https://get.sdkman.io" | bash
 $ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

- SDKMAN 명령어

```bash
 $ sdk version  <--- sdkman 버전출력
 $ sdk list java  <-- 설치 가능 & 설치된 JDK목록
 $ sdk install java 11.0.12.7.2-amzn <--- 지정된 JDK설치(원하는 종류와 버전 지정)
 $ sdk default java 11.0.12.7.2-amzn <--- 사용할 java버전을 변경(모든 쉘에 적용)
 $ sdk use java 11.0.12.7.2-amzn <--- 사용할 java버전을 변경(현재 쉘에만 적용)
 $ sdk current java <--- 현재 사용중인 java버전 출력
 $ echo $JAVA_HOME  <--- JAVA_HOME으로 지정된 경로 출력
```

**[참고]** openJDK버전별 다운로드 - https://jdk.java.net/archive/

Tomcat 9 설치 - https://tomcat.apache.org/download-92.cgi
[Windows] https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.52/bin/apache-tomcat-9.0.52-windows-x64.zip
[Mac] https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.52/bin/apache-tomcat-9.0.52.tar.gz다운로드 받은 파일을 설치하고자하는 디렉토리로 이동후 아래의 명령을 실행. 압축을 풀어서 사용자의 홈디렉토리(~)에 저장.

```bash
$ tar -xvf apache-tomcat-9.0.52.tar.gz -C ~
```
### tomcat 실행 방법

```bash
cd apache-tomcat-9.0.76/bin
```

으로 이동

```bash
ls -la
```

명령가능한 목록을 보여준다.

```bash
./startup.sh
```

톰캣 실행시키는 명령어 위에 말한 바와 같이 `ls -la` 명령어를 통해 확인한 리스트에 해당 명령어가 있다.

위의 명령어 입력 후 브라우저에 `localhost:8080` 서버 진입시 tomcat 홈페이지가 뜨는걸 확인할 수 있는데

정상적으로 해당 프로그램이 실행되고 있다는 뜻이다.

### tomcat 종료 방법

```bash
./shutdown.sh
```

위의 명령어를 통해 해당 프로그램을 종료 시킬 수 있다.

### 프로젝트 시작하기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/5672c0e0-4559-4b5b-b88f-b6fb459c8fb5)

File → New →

- Spring Starter Project 👉🏻 Spring Boot Project
- Spring Lagacy Project 👉🏻 Spring Project
  우리가 만들려는 spring 프레임 워크

![image](https://github.com/solfany/solfany.github.io/assets/123814718/98e1201e-096e-4715-a932-ad32273dbba4)

project 이름 기입 후 Spring MVC project 선택 후 Finish 해주면 된다.

## 이슈 사항

src 폴더의 Error 발생

> “Can not find the tag library descriptor for "http://java.sun.com/jsp/jstl/core”

위와 같은 에러 발생

원인은 여러 가지 요소가 있겠지만

JSP Standard Tag Library)이 없어서 발생한 문제라고 나왔고

첫번째 해결 방법은 pom.xml로 이동해서 java.servlet 부분을 확인하고,

다음과 같이 메이븐 디펜던시 (Maven Dependency)를 추가해주면 된다.

```bash
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>jstl</artifactId>
<version>1.2</version>
</dependency>
```

두번째 해결 방법은 pom.xml 파일이 위와 같이 설정 되어있을 땐

상단 메뉴 → Project → Clean → All project or 해당 프로젝트 선택 후 ‘OK’ 를 누르면

src 폴더의 에러가 사라진 것을 확인 할 수 있다.

필자는 두번째 방법으로 해당 오류를 잡았다.

## 톰캣 연동하기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/fde71df0-9574-4898-a101-b54e41f56b59)

파란색 글씨의 링크를 클릭해보자

![image](https://github.com/solfany/solfany.github.io/assets/123814718/b5afb6c5-74d9-4a28-ace4-8ed04805c8df)

이런 창이 뜨게 되는데 검색창에 tomcat이라고 검색을 하면 된다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/59e5144b-47ef-4efe-9b68-63bb05212de4)

내가 설치한 버전은 9.0이기 때문에 9.0을 선택한 후 next 버튼을 눌러 위치를 지정해주겠다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/87b201b5-7bb7-469a-878a-df3ffa6bf894)

위치는 tomcat을 다운 받은 홈 디렉터리 동일 폴더를 지정 후 Finish 해주면 된다.

## 정상적으로 작동 되는지 Test 해보기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/d2ec5830-0f6e-4685-beb9-2a05edfd7901)

이미 실행을 해본 뒤 캡쳐해서 올리는 거라 clonsole에 떠있는 내용은 무시하면 된다.

project 폴더 우 클릭 후 Run As → 1 Run on Server 클릭 후 finish를 눌러 실행해주면

Ansi Console 창이 하나 뜨게 되는데 (캡쳐를 못했다 ㅠ)

[Never remind me again] 을 눌러 다음에 설정하도록 했다.

> 버퍼에 관한 알림창인데 당장은 중요하지 않기 때문에 패스!

그럼 “Hello word ” 라는 문구가 테스트 출력 된다.

**그런데 만약 알림창이 뜨면서 출력이 안된다고 하면 아래 해결 방법을 참고 바란다.**

## 오류 발생

![image](https://github.com/solfany/solfany.github.io/assets/123814718/ca95eea4-cc34-4276-8d34-7e640ff8bcd4)

> Page load falied with error:The resource could not de loaded …

해당 알람창이 뜨는 원인 Https 프로토콜 제약 때문에 나타나는 알람창이다.

mac os는 windows 와 다르게 보안이 강해서 mac os에만 나타나는 알람창이다.

내부 브라우저에서 https 프로토콜을 사용하지 못하게 막아두었기 때문에 “Hello word” 라는 테스트 문을 확인할 수 없을 것이다.

이런 경우에는 외부 브라우저를 사용하면 된다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/afd53780-0e55-4b0f-a111-5e28010646ab)

우측 상단의 돋보기에 web browser 라고 검색하면

Perferences 의 Web Browser 를 클릭해주면 된다.

그 후 Web Browser → Use external web browser → New → 사용하는 웹 이름 (ex. 구글 크롬) 작성 과 위치는 해당 웹 어플리케이션이 들어가있는 주소를 찍어주면 된다. → ok → Apply and Close

하면 외부 브라우저랑 연동이 완료 된다.

마지막으로 다시 테스트 해보면 정상적으로 브라우저가 열리는 것을 확인 할 수 있다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/f8726bd9-6ad9-4cd5-8b6e-c7be416fc0ea)

글씨가 깨져 보이는데 UTF-8 설정은 다음시간에 다뤄보고 업로드 하겠다!
