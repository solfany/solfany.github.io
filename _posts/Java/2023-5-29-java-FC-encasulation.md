---
title: "[Java] 캡슐화 (encapsulation)"
categories:
  - Java
tags: [Java, Fastcampus]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/fast-main.png?raw=true)

## 정보 은닉을 활용한 캡슐화

- 꼭 필요한 정보와 기능만 외부에 오픈함
- 대부분의 멤버 변수와 메서드를 감추고 외부에 통합된 인터페이스만은 제공하여 일관된 기능을 구현 하게 함
- 각각의 메서드나 멤버 변수를 접근함으로써 발생하는 오류를 최소화 한다.

<br>

## 레포트 만들기 예제

```java
public class MakeReport {

	StringBuffer buffer = new StringBuffer();

	private String line = "===========================================\n";
	private String title = "  이름\t   주소 \t\t  전화번호  \n";
	private void makeHeader()
	{
		buffer.append(line);
		buffer.append(title);
		buffer.append(line);
	}

	private void generateBody()
	{
		buffer.append("James \t");
		buffer.append("Seoul Korea \t");
		buffer.append("010-2222-3333\n");

		buffer.append("Tomas \t");
		buffer.append("NewYork US \t");
		buffer.append("010-7777-0987\n");
	}

	private void makeFooter()
	{

		buffer.append(line);
	}

	public String getReport()
	{
		makeHeader();
		generateBody();
		makeFooter();
		return buffer.toString();
	}
}
```

```java
public class TestReprt {

	public static void main(String[] args) {

		MakeReport report = new MakeReport();
		String builder = report.getReport();

		System.out.println(builder);
	}

}
```

<div style: width:30px>

![image](https://github.com/solfany/solfany/assets/123814718/c49131b5-18ea-4886-a780-d946f5e69624)

</div>
