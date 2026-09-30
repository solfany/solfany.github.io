---
title: "[Spring MVC] 동적 리소스, 정적 리소스 RequestMapping"
categories:
  - Spring
tags: [Spring, Fastcampus]
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

# 리소스의 종류

서버가 제공하는 리소스에는 2가지가 있다.

## 동적 리소스

프로그램이 생성하는 리소스, 리소스 내용이 고정되어 있지 않은 것

- ex) 프로그램, 스트리밍(라이브 방송)

## 정적 리소스

파일 형태로 바뀌지 않는 것

- ex) \*.html, img, js, css

💡 코드로 예시를 살펴보자

```java
package com.fastcampus.ch2;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class TowDice {



	 //주소와 연결
	@RequestMapping("/rollDice")

	//Servlet은 HttpServletResponse객체에 Content Type, 응답코드, 응답 메시지등을 담아서 전송함
	public void main(HttpServletResponse response ) throws IOException {
		int idx1 = (int)(Math.random()*6)+1;
		int idx2 = (int)(Math.random()*6)+1;
		int idx3 = (int)(Math.random()*6)+1;
		int idx4 = (int)(Math.random()*6)+1;
		int idx5 = (int)(Math.random()*6)+1;
		int idx6 = (int)(Math.random()*6)+1;

		// type 선언
		response.setContentType("text/html");
		response.setCharacterEncoding("utf-8");

		//출력문
		PrintWriter out = response.getWriter();
		out.println("<html>");
		out.println("<head>");
		out.println("</head>");
		out.println("<body>");
		out.println("<img src = 'resources/img/dice"+idx1+".jpg' >");
		out.println("<img src = 'resources/img/dice"+idx2+".jpg' >");
		out.println("<img src = 'resources/img/dice"+idx3+".jpg' >");
		out.println("<img src = 'resources/img/dice"+idx4+".jpg' >");
		out.println("<img src = 'resources/img/dice"+idx5+".jpg' >");
		out.println("<img src = 'resources/img/dice"+idx6+".jpg' >");
		out.println("</body>");
		out.println("</html>");

	}
}
```

> 새로고침시 주사위가 랜덤으로 6개 출력된다.

```java
		out.println("<img src = 'resources/img/dice"+idx6+".jpg' >");
```

dice + 이미지 번호가 오게 되나, random 함수로 매번 바뀌도록 변수 선언

이렇게 매번 바뀌는 결과가 바뀌는 코드를 “동적 리소스” 라고 한다.

<img src="https://github.com/solfany/solfany.github.io/assets/123814718/a68f5c97-5416-41d8-b132-74e5e47879a1" width="300px"></img><br/>

반면에 이런 이미지 파일 같은 경우는 “정적 리소스” 라고 불린다.

## 출력화면

![image](https://github.com/solfany/solfany.github.io/assets/123814718/d53353f5-2017-4c97-9d67-fbcf514c1a81)
