---
title: "[Java]Static, Instance"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/3..png?raw=true)

# Static 이란

< static > 을 선언하면 메모리에 계속 상주한다.

- 절차지향
- class에서 직접 호출이 가능하다. 이유는 처음부터 메모리에 할당 되어있기 때문이다.
- Static 이 없는 경우 메모리 할당이 필요하기 때문에 instance 를 통해서 메모리에 넣어놓고 사용.

- static은 별도의 선언없이 사용가능하다 (프로그램 시작과 동시에 할당) - 영구
- static이 없는 경우, lnstance 선언하고 사용 (메모리 할당) - 임시

- static은 모든 객체가 메모리를 공유한다.
  - 메인 메서드에서 변화를 주면 모든 객체가 동시에 변한다.
  - but, lnstance 의 경ㅇ우 새롭게 메모리를 할당하는 독립된 새로운 객체로 인식해야한다. 따라서, lnstance의 변화는 메인 메소드에 국한된다.

# ps

lnstance가 class를 복제해서 메모리에 새롭게 할당한다.+

class의 모든것을 완전이 복제해서 사용한다고 착각하면 안된다.

```java
package ch02;

class KHE {
		public static int exStatic = 88;
		public int exInstance = 99;

}

	public class StaticTestTwo {
			public static void main(String[] args) {
				System.out.println(KHE.exStatic);

				KHE E1 = new KHE();
				System.out.println(E1.exInstance);

				KHE.exStatic = 77;
				E1.exInstance = 11;
				E1.exStatic = 22;

				System.out.println(KHE.exStatic);	//77예
				System.out.println(E1.exStatic);	//22예
				System.out.println(E1.exInstance);	//11예
			}
		}
```

KHE.exStatic = 77; 이라는 코드로 exStatic 변수의 값을 77로 설정한 후

E1.exStatic = 22; 이라는 코드로 다시 exStatic 변수의 값을 22로 설정

이 때문에 System.out.println(`KHE.exStatic`); 와 `E1.exStatic` 모두 22를 출력.

```java
package ch02;

class KHE {
		public static int exStatic = 88;
		public int exInstance = 99;

}

	public class StaticTestTwo {
			public static void main(String[] args) {
				System.out.println(KHE.exStatic);

		        KHE E1 = new KHE();
		        KHE E2 = new KHE();
		        KHE E3 = new KHE();

		        KHE.exStatic = 44;
				System.out.println(KHE.exStatic);
				System.out.println(E1.exStatic);
				System.out.println(E2.exStatic);
				System.out.println(E3.exStatic);
		        KHE.exStatic = 33;
				System.out.println(KHE.exStatic);
				System.out.println(E1.exStatic);
				System.out.println(E2.exStatic);
				System.out.println(E3.exStatic);
		        KHE.exStatic = 0;
				System.out.println(KHE.exStatic);
				System.out.println(E1.exStatic);
				System.out.println(E2.exStatic);
				System.out.println(E3.exStatic);
			}
		}
```

> static 변수가 클래스의 모든 인스턴스에 대해 공유되며,
> 한 인스턴스에서 이 변수를 변경하면 해당 변경이 모든 인스턴스에 반영된다.

### 결론

Instance 객체 가운데 메모리에 할당되어 상주하고 있는 실체를 말한다.

즉, Instance는 기존의 Class가 가지고 있는 변수 / 함수와

메모리를 공유하지 않는 분절된 도구로 사용할 수 있다.

그러나 함수나 변수가 Static 을 선언한 경우는 예외다.

즉, class의 static 변수의 변화는 모든 Instance 에 적용된디.

1과 같이 E1, E2, E3 / KHE class 증 어느 하나의 exStatic만 바꿔도 넷의 결과값이 동시에 변한다.

<br>

---

<br>

# 여러 인스턴스에서 고통으로 사용하는 변수를 선언하자 - static 변수

## 공통으로 사용하는 변수가 필요한 경우

- 여러 인스턴스가 공유하는 기준 값이 필요한 경우
- 학생마다 새로운 학번 생성
- 카드회사에서 카드를 새로 발급할때마다 새로운 카드 번호를 부여
- 회사에 사원이 입사할때 마다 새로운 사번이 필요한

![image](https://github.com/solfany/solfany/assets/123814718/c889a404-6bd8-4703-b998-224c6990b881)

## static 변수 선언과 사용하기

static int serialNum;

- 인스턴스가 생성될 때 만들어지는 변수가 아닌, 처음 프로그램이 메모리에 로딩될 때 메모리를 할당
- 클래스 변수, 정적변수라고도 함(vs. 인스턴스 변수)
- 인스턴스 생성과 상관 없이 사용 가능하므로 클래스 이름으로 직접 참조

Student.serialNum = 100;

## static 변수 테스트하기

Employee.java

```java
public class Employee {

	public static int serialNum = 1000;

	private int employeeId;
	private String employeeName;
	private String department;

	public int getEmployeeId() {
		return employeeId;
	}
	public void setEmployeeId(int employeeId) {
		this.employeeId = employeeId;
	}
	public String getEmployeeName() {
		return employeeName;
	}
	public void setEmployeeName(String employeeName) {
		this.employeeName = employeeName;
	}
	public String getDepartment() {
		return department;
	}
	public void setDepartment(String department) {
		this.department = department;
	}

}
```

<br>

EmployeeTest.java

```java
public class EmployeeTest {

	public static void main(String[] args) {
		Employee employeeLee = new Employee();
		employeeLee.setEmployeeName("이순신");
		System.out.println(employeeLee.serialNum);

		Employee employeeKim = new Employee();
		employeeKim.setEmployeeName("김유신");
		employeeKim.serialNum++;

		System.out.println(employeeLee.serialNum);
		System.out.println(employeeKim.serialNum);

	}
}
```

<br>

![image](https://github.com/solfany/solfany/assets/123814718/55d0f29f-789e-457d-8a81-7d4d0bb245b4)

인스턴스가 하나의 메모리 공간을 가르킨다.

- static 변수는 인스턴스에서 공통으로 사용하는 영역임음 알 수 있음

<br>

![image](https://github.com/solfany/solfany/assets/123814718/08384cea-d5c0-492b-898f-53e142a6f527)

<br>

## 회사원이 입사할 때마다 새로운 사번 부여하기

Employee.java 생성자 구현

```java
...

	public Employee()
	{
		serialNum++;
		employeeId = serialNum;
	}

...
```

EmployeeTest.java

```java
public class EmployeeTest {

	public static void main(String[] args) {
		Employee employeeLee = new Employee();
		employeeLee.setEmployeeName("이순신");

		Employee employeeKim = new Employee();
		employeeKim.setEmployeeName("김유신");

		System.out.println(employeeLee.getEmployeeName() + "," + employeeLee.getEmployeeId());
		System.out.println(employeeKim.getEmployeeName() + "," + employeeKim.getEmployeeId());
	}
}
```

![image](https://github.com/solfany/solfany/assets/123814718/dc2fff9f-f5ed-4ce0-9793-5f154ec9902a)

<br>

## static 변수와 메서드는 인스턴스 변수, 메서드가 아니므로 클래스 이름으로 직접 참조

```java
System.out.println(Employee.serialNum);
```

<br>

# static메서드의 구현과 활용, 변수의 유효 범위

## static 메서드 만들기

- serialNum 변수를 private으로 선언하고 getter/setter 구현

Employee.java

```java
private static int serialNum = 1000;

 ...
public static int getSerialNum() {
	return serialNum;
}

public static void setSerialNum(int serialNum) {
	Employee.serialNum = serialNum;
}
```

- 클래스 이름으로 호출 가능 ( 클래스 메서드, 정적 메서드 )

```java
System.out.println(Employee.getSerialNum());
```

<br>

## static 메서드(클래스 메서드)에서는 인스턴스 변수를 사용할 수 없다

- static 메서드는 인스턴스 생성과 무관하게 클래스 이름으로 호출 될 수 있음
- 인스턴스 생성 전에 호출 될 수 있으므로 static 메서드 내부에서는 인스턴스 변수를 사용할 수 없음

Employee.java

```java
public static void setSerialNum(int serialNum) {
		int i = 0;

		employeeName = "Lee";  //오류발생
		Employee.serialNum = serialNum;
	}
```

EmployeeTest2.java

```java
public class EmployeeTest2 {

	public static void main(String[] args) {

		System.out.println(Employee.getSerialNum());
		Employee.setSerialNum(1003);
		System.out.println(Employee.getSerialNum());
	}
}
```

## 변수의 유효 범위와 메모리

- 변수의 유효 범위(scope)와 생성과 소멸(life cycle)은 각 변수의 종류마다 다름
- 지역변수, 멤버 변수, 클래스 변수는 유효범위와 life cycle, 사용하는 메모리도 다름

![image](https://github.com/solfany/solfany/assets/123814718/4e2f5b1b-e6aa-41ec-8179-122ecba5664b)

- static 변수는 프로그램이 메모리에 있는 동안 계속 그 영역을 차지하므로 너무 큰 메모리를 할당하는 것은 좋지 않음
- 클래스 내부의 여러 메서드에서 사용하는 변수는 멤버 변수로 선언하는 것이 좋음
- 멤버 변수가 너무 많으면 인스턴스 생성 시 쓸데없는 메모리가 할당됨
- 상황에 적절하게 변수를 사용해야 함

<br>
<br>

# static 응용 - 싱글톤 패턴(singleton pattern)

## 싱글톤 패턴이란?

- 프로그램에서 인스턴스가 단 한 개만 생성되어야 하는 경우 사용하는 디자인 패턴
- static 변수, 메서드를 활용하여 구현 할 수 있음

## 싱글톤 패턴으로 회사 객체 구현하기

- 생성자는 private으로 선언

```java
private Company() {}
```

- 클래스 내부에 유일한 private 인스턴스 생성

```java
private static Company instance = new Company();
```

- 외부에서 유일한 인스턴스를 참조할 수 있는 public 메서드 제공

```java
public static Company getInstance() {

	if( instance == null) {
		instance = new Company();
	}
	return instance;

}
```

CompanyTest.java

```java
public class CompanyTest {

	public static void main(String[] args) {
		Company company1 = Company.getInstance();

		Company company2 = Company.getInstance();

		System.out.println(company1);
		System.out.println(company2);

		//Calendar calendar = Calendar.getInstance();
	}
}
```

![image](https://github.com/solfany/solfany/assets/123814718/570291ce-862b-4dbf-bb8d-d2828d9a9853)

```
클래스다이어그램

클래스 이름

변수

생성자와 메서드

-: private

+: public
```
