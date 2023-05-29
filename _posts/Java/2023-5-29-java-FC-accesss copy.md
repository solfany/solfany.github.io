---
title: "[Java]접근 제어 지시자(access modifier)와 정보은닉(infomation hiding)"
categories:
  - Java
tags: [Java, Fastcampus]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/fast-main.png?raw=true)

## 접근 제어 지시자 (accesss modifier)

- 클래스 외부에서 클래스의 멤버 변수, 메서드, 생성자를 사용할 수 있는지 여부를 지정하는 키워드
- private : 같은 클래스 내부에서만 접근 가능 ( 외부 클래스, 상속 관계의 클래스에서도 접근 불가)
- 아무것도 없음 (default) : 같은 패키지 내부에서만 접근 가능 ( 상속 관계라도 패키지가 다르면 접근 불가)
- protected : 같은 패키지나 상속관계의 클래스에서 접근 가능하고 그 외 외부에서는 접근 할 수 없음
- public : 클래스의 외부 어디서나 접근 할 수 있음

<br>

<br>

## get()/ set() 메서드

- private 으로 선언된 멤버 변수 (필드)에 대해 접근, 수정할 수 있는 메서드를 public으로 제공
- get() 메서드만 제공 되는 경우 read-only 필드
- 이클립스에서 자동으로 생성됨

<br>

<br>

## 정보 은닉

- private으로 제어한 멤버 변수도 public 메서드가 제공되면 접근 가능하지만 변수가 public으로 공개되었을 때보다

private 일때 각 변수에 대한 제한을 public 메서드에서 제어 할 수 있다.

```java
public void setMonth(int month) {

		if ( month < 1 || month > 12) {
			isValid = false;
		}
		else {
			this.month = month;
		}
	}
```

- 객체 지향 프로그램에서 정보 은닉은 필요한 외부에서 접근 가능한 최소한의 정보를 오픈함으로써 객체의 오류를 방지하 클라이언트 객체가 더 효율적으로 객체를 활용할 수 있도록 해준다.

<br>

<br>

## 실습 (스위치 캐스를 이용해 달별로 출력하기 )

BirthDay.java

```java
package ch10;public class BirthDay {

	 private int day;
	 private int month;
	 private int year;

	 private boolean isValid;

	 public int getDay() {
		 return day;
	 }

	 public void  setDay(int day) {
		 this.day = day;
	 }

	public int getMonth() {
		return month;
	}

	public void setMonth(int month) {
		if (month < 1 || month > 12)
		{
			isValid = false;
		}
		else {
			isValid = true;
			this.month = month;
		}
		this.month = month;
	}

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	public void showDate()
	{
		if(isValid) {
			System.out.println(year + "년" + month + "월" + day + "일 입니다.");
		}
		else {
			System.out.println("유효하지 않은 날짜 입니다.");
		}
	}

	}
```

<br>

BirthDayTest.java

```java
package ch10;

public class BirthDayTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		BirthDay date = new BirthDay();
		date.setYear(2019);
		date.setMonth(12);
		date.setDay(30);

		date.showDate();
	}

}
```

객체의 멤버 변수에 접근제한를 가하므로써 객체를 사용할 때 오류를 막을 수 있다.

사용측에서의 오류를 대폭 줄여준다.

해당 정보의 경우 오용이 되면 안되기 때문에 접근 제어를 가한다.

<br>

<br>

```java
public boolean getValid() {
		return isValid;
	}
```

> Valid 같은 경우에도 보여줄 필요는 없지만 굳이 공개를 해야한다면 get만 가능하고
> set은 불가능하다.
