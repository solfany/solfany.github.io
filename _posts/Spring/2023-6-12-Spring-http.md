---
title: "[Spring]HTTP와 HttpServletRequest  "
categories:
  - Spring
tags: [Spring, HTTP, AWS]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## 1. HTTP, 요청과 응답

### HTTP란?

HyperText(링크) Transfer Protocol 의 약자이다.

하이퍼텍스트(HTML) 문서를 교환하기 위해 만들어진 Protocol (통신 규약)인데, 쉽게 생각하면 웹 상에서 통신을 할 때 어떤 형식으로 통신을 하자고 정해놓은 약속이다.

프론트엔드 서버 ←→ 클라이언트 간의 통신

프론트엔드 서버 ←→ 백엔드 서버 간의 통신

HTTP는 TCP / IP 기반 (무슨말? )

두개의 다른 서버가 소통하려면 공통의 언어가 필요해서

HTTP 라는 양식을 정해서 서로 전달하고 받자! 하고 언어를 정해놓은 것이다.

---

### 요청과 응답

요청(request) ← → 응답(response) 의 구조로 되어있다.

클라이언트가 서버에 HTTP request 를 보내고,

서버가 HTTP response 를 돌려보낸다.

클라이언트와 서버의 모든 통신이 요청과 응답으로 이루어진다.

### HTTP는 Stateless

HTTP 는 stateless 이다. 즉 State 를 저장하지 않는다.

위의 말의 의미는 요청/응답하는 정보가 저장되지 않는다는 뜻이다. (여러가지의 요청/응답 과정을 거칠 때 그것들끼리 연결되서 작동하는것이 아니다. )

**클라이언트가 요청을 보내고 응답을 받은 후, 그 다음에 다시 요청을 보낼 때 그 전에 보낸 요청/응답에 대해 알지 못한다.**

---

### HTTP Request 의 구조

### 1. Starter line

해당 request 가 어떤 action 을 의미하는지 정보를 담는다. request target (url) 어떤 곳에다가 요청하는지를 담는다.

### 2. Headers

해당 request에 대한 추가 정보를 담고있는 부분이다.

Key:Value 값으로 되어있다.

Request Target도 주소. Host 도 주소. 두개를 합쳐서 보고 서버가 알게 된다.

### 3. Body

데이터가 담겨있는 부분이다. 여기서 내가 가졌던 의문은 Request 를 하는데 왜 정보를 담아서 보내야되지?하는 것이였다.

→ 클라이언트의 정보를 넘겨줘야, 서버에서 어떤 정보를 담아서 보내줘야할지 알려줄 수 있는 request들이 많다.

예를들면 유저의 로그인 정보를 담아서 서버쪽에 이런 사람이 로그인했다, 고 알려주면 서버측에서 그 사람의 프로필 사진은 뭔지, 그 사람이 어떤 사람을 팔로우하는지, 그런 정보들을 담아서 돌려보내줄것이다.

request 도 데이터를 담아서 요청할 수 있고, response 에서 데이터를 담아서 줄수 있다.

위에서 얘기한 어떤 사항들을 요청하는지는

**Content-type** 에 의해서 결정된다.

이런 내용들은 개발자도구 Network 패널에서 모두 확인 가능하다.

**Request 의 예시**

```
POST /payment-sync HTTP/1.1

Accept: application/json
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 83
Content-Type: application/json
Host: intropython.com
User-Agent: HTTPie/0.9.3

{
    "imp_uid": "imp_1234567890",
    "merchant_uid": "order_id_8237352",
    "status": "paid"
}
```

---

### HTTP Response 구조

Response 도 request와 마찬가지로 크게 3부분으로 구성되어있다.

### 1. Status Line

- Response 의 상태를 간략하게 나타내주는 부분
- 3부분으로 구성되어 있다.
  - HTTP 버전
  - Status code: 응답 상태를 나타내는 코드
  - Status text: 응답 상태를 간략하게 설명해주는 부분.

### 2. Headers

- Response의 headers와 동일하다.
- 다만 response에서만 사용되는 header 값들이 있다.
- 예를 들어, `User-Agent` 대신에 `Server` 헤더가 사용된다.

### 3. Body

- Response의 body와 일반적으로 동일하다.
- Request와 마찬가지로 모든 response가 body가 있지는 않다. 데이터를 전송할 필요가 없을경우 body가 비어있게 된다.

---

### HTTP Method 란?

- HTTP request가 의도하는 action을 정의한것.

`GET`

- 요청 입장에서 데이터 가져올때
- 이름 그대로 어떠한 데이타를 서버로 부터 받아(GET)올때 주로 사용하는 Method.

`POST`

- 요청 입장에서 데이터를 포스팅할때
- 데이터를 생성/수정/삭제 할때 주로 사용되는 Method.

`PUT`

- 데이터를 생성 (POST 와 비슷한 기능)

`DELETE`

- 데이터를 서버에서 삭제 요청

!https://velog.velcdn.com/images/pear/profile/fa5ee6c3-b74d-4565-bfc1-9440cad056eb/doyoonDev_white.jpg

### HttpServletRequest의 메서드

JSP 기본 내장 객체 중 request 객체는 JSP에서 가장 많이 사용되는 객체이다.

웹브라우저 사용자인 클라이언트로부터 서버로 요청이 들어오면

서버에서는 HttpServletRequest를 생성하며, 요청정보에 있는 패스로 매핑된 서블릿에게 전달다.

이렇게 전달받은 내용들을 파라미터로 Get과 Post 형식으로 클라이언트에게 전달하게 된다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/648bf5f9-bb11-4cd8-bf56-5c8527a696bd)

![image](https://github.com/solfany/solfany.github.io/assets/123814718/368bcc30-1799-41b5-aa10-1c0819233483)

HttpServletRequest를 사용하면, 값을 받아올 수가 있는데

만약 회원 정보를 컨트롤러로 보냈을 때 HttpServletRequest 객체 안에 모든 데이터들이 들어가게 다!

원하는 데이터를 꺼낼때는 HttpServletRequest의 객체 안의 메소드인 getParameter()를 이용하면 다.

**(getParameter의 반환타입은 String)**

## 2. 클라이언트와 서버

클라이언트(client) : 서비스를 요청하는 애플리케이션

서버(server) : 서비스(service)를 제공하는 애플리케이션

![image](https://github.com/solfany/solfany.github.io/assets/123814718/3f2235b4-21dc-45a5-97c5-14236d135295)

## 3. 실습

### 실습 코드

```java
package com.fastcampus.ch2;

import java.util.Calendar;

// 년 원 일을 입력하면 요일을 알려주는 프로그램

public class YoilTeller {

	public static void main(String[] args) {
		//1. 입력
		String year = args[0];
		String month = args[1];
		String day = args[2];

		int yyyy = Integer.parseInt(year);
		int mm = Integer.parseInt(month);
		int dd = Integer.parseInt(day);

		// 2. 직업a
		Calendar cal = Calendar.getInstance();
		cal.set(yyyy, mm -1, dd);

		int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
		char yoil = "월화수목금토일".charAt(dayOfWeek);


		// 3. 출력
		System.out.println( year + "년 " + month + "월 " + day + "일은 ");
		System.out.println(yoil + "요일 입니다. ");
	}

}

// 날짜 입력시 무슨 요일인지 알려주는 로직
```

날짜를 입력하면 요일을 출력하는 로직이다.

### 터미널로 결과 값 확인하기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/eb2d2533-8ca6-4e51-b736-fc5f501773e3)

좌측 target → show In → Terminal

```bash
cd/classes
```

입력 후

```bash
java com.fastcampus.ch2.YoilTeller 2023 6 11
```

입력

> `java com.fastcampus.ch2.YoilTeller` - (main 호출 )
> `2023 6 11` 해당 문자열은 아래의 코드에 배열로 순자적으로 담기게 된다. 👇🏻

```bash
		String year = args[0];
		String month = args[1];
		String day = args[2];
```

![image](https://github.com/solfany/solfany.github.io/assets/123814718/9df54586-9e53-47d7-8fd4-fe43b39a3aeb)

이렇게 터미널로 확인이 가능하다.

> java 인터페이터가 입력받은 값은 문자열로 받아 main으로 넘겨주게 된다.

## 4. 과제

```java
package com.fastcampus.ch2;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import javax.servlet.http.HttpServletRequest;

@Controller
public class RequestInfo {
    @RequestMapping("/requestInfo")
    //    public static void main(String[] args) {
    public void main(HttpServletRequest request) {
        System.out.println("request.getCharacterEncoding()="+request.getCharacterEncoding()); // 요청 내용의 인코딩
        System.out.println("request.getContentLength()="+request.getContentLength());  // 요청 내용의 길이. 알수 없을 때는 -1
        System.out.println("request.getContentType()="+request.getContentType()); // 요청 내용의 타입. 알 수 없을 때는 null

        System.out.println("request.getMethod()="+request.getMethod());      // 요청 방법
        System.out.println("request.getProtocol()="+request.getProtocol());  // 프로토콜의 종류와 버젼 HTTP/1.1
        System.out.println("request.getScheme()="+request.getScheme());      // 프로토콜

        System.out.println("request.getServerName()="+request.getServerName()); // 서버 이름 또는 ip주소
        System.out.println("request.getServerPort()="+request.getServerPort()); // 서버 포트
        System.out.println("request.getRequestURL()="+request.getRequestURL()); // 요청 URL
        System.out.println("request.getRequestURI()="+request.getRequestURI()); // 요청 URI

        System.out.println("request.getContextPath()="+request.getContextPath()); // context path
        System.out.println("request.getServletPath()="+request.getServletPath()); // servlet path
        System.out.println("request.getQueryString()="+request.getQueryString()); // 쿼리 스트링

        System.out.println("request.getLocalName()="+request.getLocalName()); // 로컬 이름
        System.out.println("request.getLocalPort()="+request.getLocalPort()); // 로컬 포트

        System.out.println("request.getRemoteAddr()="+request.getRemoteAddr()); // 원격 ip주소
        System.out.println("request.getRemoteHost()="+request.getRemoteHost()); // 원격 호스트 또는 ip주소
        System.out.println("request.getRemotePort()="+request.getRemotePort()); // 원격 포트
    }
}
```

> 어떤 메서드가 어떤 값을 반환시키는지 확인해보자 !

해당 코드를 입력받아 출력 시켜보고
서버에 배포시켜 출력 확인해보기

## 출력 결과

![image](https://github.com/solfany/solfany.github.io/assets/123814718/1bde449b-18cc-4fa5-a755-457fbdf9a85d)

```java
http://[Ipv4 주소]/[포트번호]/[패키지명]/[클래스명]

http://52.62.213.42:8080/ch2/requestInfo
```

서버에 성공적으로 출력된 것을 확인할 수 있다..

서버에 배포하는 과정도 추후 자세히 정리해서 올려야겠다!

과정이 복잡하기 때문에 조금 더 익숙해지고 실습해보고 포스팅 하기로!
