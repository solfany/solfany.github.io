---
title: "[Java] 인터페이스(interface)"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)

# 1. 인터페이스(interface)

## 1-1. 인터페이스란?

자식 클래스가 여러 부모 클래스를 상속받을 수 있다면, 다양한 동작을 수행할 수 있다는 장점을 가지게 될 것이다.

하지만 클래스를 이용하여 다중 상속을 할 경우 메소드 출처의 모호성 등 여러 가지 문제가 발생할 수 있어 자바에서는 클래스를 통한 다중 상속은 지원하지 않는다고 한다.

하지만 다중 상속의 이점을 버릴 수는 없기에 자바에서는 인터페이스라는 것을 통해 다중 상속을 지원하고 있다.

> 인터페이스(interface)란 다른 클래스를 작성할 때 기본이 되는 틀을 제공하면서, 다른 클래스 사이의 중간 매개 역할까지 담당하는 일종의 추상 클래스를 의미한다.

자바에서 추상 클래스는 추상 메소드뿐만 아니라 생성자, 필드, 일반 메소드도 포함할 수 있다.

하지만 인터페이스(interface)는 오로지 추상 메소드와 상수만을 포함할 수 있다.

<img src = "https://github.com/solfany/project02/assets/123814718/a8cd8353-1160-481e-b167-307d548f54c0" width="500"/>

- 모든 메서드가 추상 메서드로 선언됨 public abstract
- 모든 변수는 상수로 선언됨 public static final
-

```java
interface 인터페이스 이름{

    public static final float pi = 3.14F;
    public void makeSomething();
}
```

- 자바 8 부터 디폴트 메서드(default method)와 정적 메서드(static method) 기능의 제공으로 일부 구현 코드가 있음

---

## 1-2. 인터페이스의 선언

자바에서 인터페이스를 선언하는 방법은 클래스를 작성하는 방법과 같다.

인터페이스를 선언할 때에는 접근 제어자와 함께 interface 키워드를 사용하면 된다.

자바에서 인터페이스는 다음과 같이 선언한다.

### 문법

```java
접근제어자 interface 인터페이스이름 {
	public static final 타입 상수이름 = 값;

	public abstract 메소드이름(매개변수목록);
}
```

단, 클래스와는 달리 인터페이스의 모든 필드는 public static final이어야 하며,

모든 메소드는 public abstract이어야 한다.

이 부분은 모든 인터페이스에 공통으로 적용되는 부분이므로 이 제어자는 생략할 수 있다.

이렇게 생략된 제어자는 컴파일 시 자바 컴파일러가 자동으로 추가해 준다.

---

## 1-3. 인터페이스의 장점

인터페이스를 사용하면 다중 상속이 가능할 뿐만 아니라 다음과 같은 장점을 가질 수 있다.

1. 대규모 프로젝트 개발 시 일관되고 정형화된 개발을 위한 표준화가 가능하다.

2. 클래스의 작성과 인터페이스의 구현을 동시에 진행할 수 있으므로, 개발 시간을 단축할 수 있다.

3. 클래스와 클래스 간의 관계를 인터페이스로 연결하면, 클래스마다 독립적인 프로그래밍이 가능하다.

---

## 1-4. 인터페이스 정의와 구현

인터페이스는 추상 클래스와 마찬가지로 자신이 직접 인스턴스를 생성할 수는 없다.

따라서 인터페이스가 포함하고 있는 추상 메소드를 구현해 줄 클래스를 작성해야만 다.

자바에서 인터페이스는 다음과 같은 문법을 통해 구현한다.

### 문법

```java
class 클래스이름 implements 인터페이스이름 { ... }
```

만약 모든 추상 메소드를 구현하지 않는다면, abstract 키워드를 사용하여 추상 클래스로 선언해야 한다.

<img src= "https://github.com/solfany/project02/assets/123814718/3a2ce834-3d34-4e3e-aea5-b5938fef5eff" width="300" />

Calc.java

```java
public interface Calc {

	double PI = 3.14;
	int ERROR = -99999999;

	int add(int num1, int num2);
	int substract(int num1, int num2);
	int times(int num1, int num2);
	int divide(int num1, int num2);

}
```

Calculator.java

```java
public abstract class Calculator implements Calc{

	@Override
	public int add(int num1, int num2) {
		return num1 + num2;
	}

	@Override
	public int substract(int num1, int num2) {
		return num1 - num2;
	}
}
```

CompleteCalc.java

```java
public class CompleteCalc extends Calculator{

	@Override
	public int times(int num1, int num2) {
		return num1 * num2;
	}

	@Override
	public int divide(int num1, int num2) {
		if( num2 == 0 )
			return ERROR;
		else
			return num1 / num2;
	}

	public void showInfo() {
		System.out.println("모두 구현하였습니다.");
	}
}
```

CalculatorTest.java

```java
public class CalculatorTest {

	public static void main(String[] args) {
		Calc calc = new CompleteCalc();
		int num1 = 10;
		int num2 = 2;

		System.out.println(num1 + "+" + num2 + "=" + calc.add(num1, num2));
		System.out.println(num1 + "-" + num2 + "=" +calc.substract(num1, num2));
		System.out.println(num1 + "*" + num2 + "=" +calc.times(num1, num2));
		System.out.println(num1 + "/" + num2 + "=" +calc.divide(num1, num2));
	}
}
```

<br>
<br>

<img src= "https://github.com/solfany/project02/assets/123814718/4b848416-1f33-46b8-8ca7-093c77cd6593" width="300" />

## 1-5. 인터페이스 구현과 형 변환

- 인터페이스를 구현한 클래스는 인터페이스 형으로 선언한 변수로 형 변환 할 수 있음

```java
Calc calc = new CompleteCalc();
```

- 상속에서의 형 변환과 동일한 의미
- 클래스 상속과 달리 구현 코드가 없으므로 여러 인터페이스를 구현할 수 있음 ( cf. extends)
- 형 변환되는 경우 인터페이스에 선언된 메서드만을 사용가능함

<img src= "https://github.com/solfany/project02/assets/123814718/996ef38f-3fb2-48bd-ae74-0f51628b52e3 />

# 2. 인터페이스는 왜 쓰는가?

## 2-1. 인터페이스가 하는 일

- 클래스나 프로그램이 제공하는 기능을 명시적으로 선언
- 일종의 클라이언트 코드와의 약속이며 클래스나 프로그램이 제공하는 명세(specification)
- 클라이언트 프로그램은 인터페이스에 선언된 메서드 명세만 보고 이를 구현한 클래스를 사용할 수 있음
- 어떤 객체가 하나의 인터페이스 타입이라는 것은 그 인터페이스가 제공하는 모든 메서드를 구현했다는 의미임
- 인터페이스를 구현한 다양한 객체를 사용함 - 다형성
- 예) JDBC 인터페이스

# 3. 인터페이스를 활용한 다형성 구현 (dao 구현하기)

## 3-1. 인터페이스와 다형성

- 하나의 인터페이스를 여러 객체가 구현하게 되면 클라이언트 프로그램은 인터페이스의 메서드를 활용하여 여러 객체의 구현을 사용할 수 있음 ( 다형성)
- 여러가지 예

<img src= "https://github.com/solfany/project02/assets/123814718/230a2a38-dddc-402c-af72-f7942802d209" width="500"/>

<img src= "https://github.com/solfany/project02/assets/123814718/9c012a15-a1c6-497f-9da0-631d70779aa5" width="500"/>

## 3-2 인터페이스를 활용한 dao 구현하기

- DB에 회원 정보를 넣는 dao(data access object)를 여러 DB 제품이 지원될 수 있게 구현함
- 환경파일(db.properties) 에서 database의 종류에 대한 정보를 읽고 그 정보에 맞게 dao 인스턴스를 생성하여 실행될 수 있게 함
- source hierachy

<img src= "https://github.com/solfany/project02/assets/123814718/860f92f0-6907-4388-a384-4bd6bf9767a9" width="400"/>

UserInfo.java (사용자 정보 클래스)

```java
public class UserInfo {

	private String userId;
	private String passwd;
	private String userName;

	public String getUserId() {
		return userId;
	}

	public void setUserId(String userId) {
		this.userId = userId;
	}

	public String getPasswd() {
		return passwd;
	}

	public void setPasswd(String passwd) {
		this.passwd = passwd;
	}

	public String getUserName() {
		return userName;
	}

	public void setUserName(String userName) {
		this.userName = userName;
	}
}
```

UserInfoDao.java ( dao 에서 제공되어야 할 메서드를 선언한 인터페이스 )

```java
public interface UserInfoDao {

	void insertUserInfo(UserInfo userInfo);
	void updateUserInfo(UserInfo userInfo);
	void deleteUserInf(UserInfo userInfo);
}
```

UserInfoMySqlDao.java (UserInfoDao 인터페이스를 구현한 MySql 버전 dao)

```java
public class UserInfoMySqlDao implements UserInfoDao{

	@Override
	public void insertUserInfo(UserInfo userInfo) {
		System.out.println("insert into MYSQL DB userId =" + userInfo.getUserId() );
	}

	@Override
	public void updateUserInfo(UserInfo userInfo) {
		System.out.println("update into MYSQL DB userId = " + userInfo.getUserId());
	}

	@Override
	public void deleteUserInf(UserInfo userInfo) {
		System.out.println("delete from MYSQL DB userId = " + userInfo.getUserId());

	}

}
```

UserInfoOracleDao.java (UserInfoDao 인터페이스를 구현한 Oracle 버전 dao)

```java
public class UserInfoOracleDao implements UserInfoDao{

	public void insertUserInfo(UserInfo userInfo){
		System.out.println("insert into ORACLE DB userId =" + userInfo.getUserId() );
	}

	public void updateUserInfo(UserInfo userInfo){
		System.out.println("update into ORACLE DB userId = " + userInfo.getUserId());
	}

	public void deleteUserInf(UserInfo userInfo){
		System.out.println("delete from ORACLE DB userId = " + userInfo.getUserId());
	}
}
```

UserInfoClient.java (UserInfoDao 인터페이스를 활용하는 클라이언트 프로그램)

```java
public class UserInfoClient {

	public static void main(String[] args) throws IOException {

		FileInputStream fis = new FileInputStream("db.properties");

		Properties prop = new Properties();
		prop.load(fis);

		String dbType = prop.getProperty("DBTYPE");

		UserInfo userInfo = new UserInfo();
		userInfo.setUserId("12345");
		userInfo.setPasswd("!@#$%");
		userInfo.setUserName("이순신");


		UserInfoDao userInfoDao = null;

		if(dbType.equals("ORACLE")){
			userInfoDao = new UserInfoOracleDao();
		}
		else if(dbType.endsWith("MYSQL")){
			userInfoDao = new UserInfoMySqlDao();
		}
		else{
			System.out.println("db support error");
			return;
		}

		userInfoDao.insertUserInfo(userInfo);
		userInfoDao.updateUserInfo(userInfo);
		userInfoDao.deleteUserInf(userInfo);
	}
}
```

db.properties 환경파일이 MYSQL 일때

`DBTYPE=MYSQL`

실행결과

<img src= "https://github.com/solfany/project02/assets/123814718/6f4d7ebc-b467-45d7-9022-59666ac642fa" width="300"/>

db.properties 환경파일이 ORACLE 일때

`DBTYPE=ORACLE`

실행결과

<img src= "https://github.com/solfany/project02/assets/123814718/09bb45c2-9805-4f43-b4bf-d7552303d10c" width="300"/>

# 4. 인터페이스의 여러가지 요소

## 4-1. 상수

- 모든 변수는 상수로 변환 됨 public static final

```java
double PI = 3.14;
int ERROR = -999999999;
```

## 4-2. 추상 메서드

- 모든 선언된 메서드는 추상 메서드 public abstract

## 4-3. 디폴트 메서드 (자바 8이후)

- 구현을 가지는 메서드, 인터페이스를 구현하는 클래스들에서 공통으로 사용할 수 있는 기본 메서드
- default 키워드 사용

```java
default void description() {
	System.out.println("정수 계산기를 구현합니다.");
	myMethod();
}
```

- 구현 하는 클래스에서 재정의 할 수 있음

```java
@Override
public void description() {
	System.out.println("CompleteCalc에서 재정의한 default 메서드");
	//super.description();
}
```

- 인터페이스를 구현한 클래스의 인스턴스가 생성 되어야 사용 가능함

## 4-4. 정적 메서드 (자바 8이후)

- 인스턴스 생성과 상관 없이 인터페이스 타입으로 사용할 수 있는 메서드

```java
static int total(int[] arr) {
	int total = 0;

	for(int i: arr) {
		total += i;
	}
	mystaticMethod();
	return total;
}
```

## 4-5. private 메서드 (자바 9이후)

- 인터페이스를 구현한 클래스에서 사용하거나 재정의 할 수 없음
- 인터페이스 내부에서만 사용하기 위해 구현하는 메서드
- default 메서드나 static 메서드에서 사용함

```java
private void myMethod() {
	System.out.println("private method");
}

private static void mystaticMethod() {
	System.out.println("private static method");
}
```

##

# 5. 여러 인터페이스 구현하기, 인터페이스의 상속

## 5-1. 여러 인터페이스 구현

- 자바의 인터페이스는 구현 코드가 없으므로 하나의 클래스가 여러 인터페이스는 구현 할 수 있음
- 디폴트 메서드가 중복 되는 경우는 구현 하는 클래스에서 재정의 하여야 함
- 여러 인터페이스를 구현한 클래스는 인터페이스 타입으로 형 변환 되는 경우 해당 인터페이스에 선언된 메서드만 사용 가능 함

<img src= "https://github.com/solfany/project02/assets/123814718/11b6aa92-a0f8-464f-aa11-27584b08cf41" width="300"/>

Sell.java

```java
public interface Sell {

	void sell();


}
```

Buy.java

```java
public interface Buy {

	void buy();

}
```

Customer.java

```java
public class Customer implements Buy, Sell{

	@Override
	public void sell() {
		System.out.println("customer sell");
	}

	@Override
	public void buy() {
		System.out.println("customer buy");
	}

	public void sayHello() {
		System.out.println("Hello");
	}
}
```

CustomerTest.java

```java
public class CustomerTest {

	public static void main(String[] args) {

		Customer customer = new Customer();
		customer.buy();
		customer.sell();
		customer.sayHello();

		Buy buyer = customer;
		buyer.buy();

		Sell seller = customer;
		seller.sell();

	}
}
```

## 5-2. 디폴트 메서드가 중복 되는 경우

- 구현 코드를 가지고 인스턴스 생성된 경우만 호출되는 디폴트 메서드의 경우 두 개의 인터페이스에서 중복되면 구현하는 클래스에서 반드시 재정의를 해야 함

Sell.java

```java
public interface Sell {

	void sell();

	default void order() {
		System.out.println("판매 주문");
	}
}
```

Buy.java

```java
public interface Buy {

	void buy();

	default void order() {
		System.out.println("구매 주문");
	}
}
```

Customer.java

```java
public class Customer implements Buy, Sell{

	@Override
	public void sell() {
		System.out.println("customer sell");
	}

	@Override
	public void buy() {
		System.out.println("customer buy");
	}

	public void sayHello() {
		System.out.println("Hello");
	}

	@Override
	public void order() {
		System.out.println("customer order");
	}

}
```

CustomerTest.java

```java
public class CustomerTest {

	public static void main(String[] args) {

		Customer customer = new Customer();
		customer.buy();
		customer.sell();
		customer.sayHello();

		Buy buyer = customer;
		buyer.buy();

		Sell seller = customer;
		seller.sell();

		buyer.order();
		seller.order();

	}
}
```

## 5-3. 인터페이스의 상속

- 인터페이스 사이에도 상속을 사용할 수 있음
- extends 키워드를 사용
- 인터페이스는 다중 상속이 가능하고 구현 코드의 상속이 아니므로 타입 상속 이라고 함

<img src= "https://github.com/solfany/project02/assets/123814718/79698188-24ea-4fb6-a995-af778099c0e5" width="300"/>

X.java

```java
public interface X {

	void x();
}
```

Y.java

```java
public interface Y {

	void y();
}
```

MyInterface.java

```java
public interface MyInterface extends X, Y{

	void myMethod();
}
```

MyClass.java

```java
public class MyClass implements MyInterface{

	@Override
	public void x() {
		System.out.println("x()");
	}

	@Override
	public void y() {
		System.out.println("y()");
	}

	@Override
	public void myMethod() {
		System.out.println("myMethod()");
	}
}
```

MyClassTest.java

```java
public class MyClassTest {

	public static void main(String[] args) {

		MyClass mClass = new MyClass();

		X xClass = mClass;
		xClass.x();


		Y yClass = mClass;
		yClass.y();

		MyClass iClass = mClass;
		iClass.x();
		iClass.y();
		iClass.myMethod();
	}

}
```

## 5-4. 클래스 상속과 인터페이스 구현 함께 쓰기

- 실무에서 프레임워크나 오픈소스와 함께 연동되는 구현을 하게 되면 클래스 상속과 인터페이스의 구현을 같이 사용하는 경우가 많음

<img src= "https://github.com/solfany/project02/assets/123814718/ec51a30c-0dce-472c-8eac-0878c0406260" width="300"/>

- 책이 순서대로 대여가 되는 도서관 구현
- 책을 보관하는 자료 구조가 Shelf에 구현됨 (ArrayList)
- Queue 인터페이스를 구현함
- Shelf 클래스를 상속 받고 Queue를 구현한다.

Shelf.java

```java
public class Shelf {

	 protected ArrayList<String> shelf;

	 public Shelf() {
		 shelf = new ArrayList<String>();
	 }

	 public ArrayList<String> getShelf(){
		 return shelf;
	 }

	 public int getCount() {
		 return shelf.size();
	 }

}
```

Queue.java

```java
public interface Queue {

	void enQueue(String title);
	String deQueue();

	int getSize();
}
```

BookShelf.java

```java
public class BookShelf extends Shelf implements Queue{

	@Override
	public void enQueue(String title) {
		shelf.add(title);
	}

	@Override
	public String deQueue() {
		return shelf.remove(0);
	}

	@Override
	public int getSize() {
		return getCount();
	}

}
```

BookShelfTest.java

```java
public class BookShelfTest {

	public static void main(String[] args) {

		Queue bookQueue = new BookShelf();
		bookQueue.enQueue("태백산맥1");
		bookQueue.enQueue("태백산맥2");
		bookQueue.enQueue("태백산맥3");

		System.out.println(bookQueue.deQueue());
		System.out.println(bookQueue.deQueue());
		System.out.println(bookQueue.deQueue());
	}

}
```

<img src= "https://github.com/solfany/project02/assets/123814718/26ffe725-e180-4c9a-a3a6-95e7178c3d2f" width="300"/>

## 실습

```java
package ch09;

// MobilePhoneInterface 인터페이스는 PhoneInterface를 확장하고, 문자 메시지를 보내고 받는 기능을 추가로 정의합니다.
interface MobilePhoneInterface extends PhoneInterface {
    void sendSMS();

    void receiveSMS();
}

// MP3Interface 인터페이스는 음악을 재생하고 정지하는 기능을 정의합니다.
interface MP3Interface {
    void play();

    void stop();
}

// PDA 클래스는 두 수의 합을 계산하는 기능을 가지고 있습니다.
class PDA {
    int calculate(int x, int y) {
        return x + y;
    }
}

// Smartphone 클래스는 PDA를 확장하면서 MobilePhoneInterface와 MP3Interface 인터페이스를 구현합니다.
class Smartphone extends PDA implements MobilePhoneInterface, MP3Interface {

    @Override
    public void sendCall() {
        System.out.println("따르릉 따르릉");
    }

    @Override
    public void receiveCall() {
        System.out.println("전화왔어요");
    }

    @Override
    public void sendSMS() {
        System.out.println("문자를 보냅니다.");
    }

    @Override
    public void receiveSMS() {
        System.out.println("문자를 받았습니다.");
    }

    @Override
    public void play() {
        System.out.println("음악을 연주합니다.");
    }

    @Override
    public void stop() {
        System.out.println("음악을 중지합니다.");
    }

    void schedule() {
        System.out.println("일정을 관리합니다.");
    }
}

public class Ex_03 {
    public static void main(String[] args) {
        Smartphone phone = new Smartphone();
        phone.printLogo(); // Smartphone 클래스에 정의되지 않은 메서드를 호출하면서 컴파일 오류 발생 (주석 처리 필요)
        phone.sendCall(); // MobilePhoneInterface의 sendCall 메서드를 호출하여 전화를 걸음
        phone.play(); // MP3Interface의 play 메서드를 호출하여 음악을 재생
        System.out.println("3과 5를 더하면 " + phone.calculate(3, 5)); // PDA의 calculate 메서드를 호출하여 두 수의 합을 계산
        phone.schedule(); // Smartphone 클래스에 정의된 schedule 메서드를 호출하여 일정을 관리
    }
}
```
