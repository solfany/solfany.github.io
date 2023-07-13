---
title: "[Spring MVC]서블릿 과 JSP"
categories:
  - Spring
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## 서블릿과 컨트롤러 비교

**Servlet (서블릿)**

- 자바를 사용하여 웹페이지를 동적으로 생성하는 서버 측 프로그램 혹은 그 사양을 말함

**Controller**

- 스프링 서버 개발자 입장에서는 시작점과 끝점으로 보이지만, 사실 스프링이 사용자의 요청 (Request)과 응답 (Response)을 처리해 주고 있다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/ecda9862-ec44-476e-845e-753cafeeee6b)

## 서블릿의 생명 주기

```java
package com.fastcampus.ch2;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/test")
public class Test extends HttpServlet {


	@Override
	public void init() throws ServletException {
		// 서블릿이 초기화 될 때 자도 호출 되는 메서드 (init)
		// 1. 서블릿의 초기화 작업 담당
		System.out.println("[testServlet] init() is called. ");

	}

	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// 1. 입력
		// 2. 처리
		// 3. 출력
		System.out.println("[testServlet] service() is called. ");

	}

	@Override
	public void destroy() {
		//3 . 뒷정리 - 서블릿이 메모리에서 제거 될 때 컨테이너에 의해서 자동 호출 (한번만 수행)
		System.out.println("[testServlet] destroy() is called. ");

	}
}
```

init 은 처음 한번만 호출이 되고, 다음으로

요청이 올 때 마다 서비스가 반복적으로 호출 되면서 실행이 된다. 그 이후

서블릿이 메모리에서 내려올 때 리로딩 되거나 웹 어플리케이션이 종료될 때 호출이 된다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/a5e05738-9bc8-446f-aa0b-a077e678dd9b)

위의 코드를 실행시켜보면 서버에는 아무것도 뜨지 않지만 콘솔창에 정상적으로 값이 나온 걸 확인 할 수있다.

초기화하고, 실행이 되고 있는 것을 확인 할 수 있다.

## 서블릿의 생명 주기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/e95d8292-653c-419c-9f7a-da75b760455e)

요청이 오면 Servlet Context 에서 확인을 한다.

서블릿 인스턴스가 존재 여부에 따라 처리 방법이 달라진다.

Servlet Context 안에는 children 이라는 멤버가 있는데 맵 형태로 등록이 되어있다.

요청이 왔을 때 서블릿 인스턴스가 존재하는지 children에서 확인 후 처리한다ㅏ.

또한 서블릿은 싱클톤으로 1개의 인스턴스만 만들어진다. → 1개의 인스턴스만 만들어서 재활용한다.

## JSP(Java Server Pages)란 ?

= 서블릿

jsp 로 작성하게 되면 서블릿으로 자동 변환이 된다.

html 안에 자바 코드가 있는 것

<% ~ %> 해당 코드 안에 자바 코드를 넣는다 !

## JSP 표현식

### 스크립틀릿

<% %> - 자바 코드 실행

자버에서 하는 모든 일을 여기서 할 수 있다.

(if문 , for문, while문, switch문 등등 )

### 표현식

<%= %>

- 변수 출력, 수식 출력, 메서드 호출 등의 역할
- 웹 컨테이너에 의해 out.print(출력할 것)은 동일함

### 지시자

<%@ %>

디렉티브 태그, 외부 문서나 태그 라이브러리를 활용함, import 등의 역할도 수행

contentType, pageEncoding 을 사용하여 문서타입과 인코딩을 설정함

contentType 인코딩은 JSP 파일을 HTML 문서로 변환할 때 적용되는 인코딩

pageEncoding 인코딩은 그냥 JSP 파일에 적용되는 인코딩

### 선언문

<%! %>

함수선언 같은 것을 여기서 할 수 있음
