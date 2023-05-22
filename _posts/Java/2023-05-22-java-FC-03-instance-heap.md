---
title: "[Java] 인스턴스 생성 & heap memory"
categories:
  - Java
tags: [Java, Fastcampus]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

<br>



![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/fast-main.png?raw=true)

# 인스턴스 생성과 힙 메모리 (heap memory)

## 인스턴스 (instance)

- 클래스는 객체의 속성을 정의 하고, 기능을 구현하여 만들어 놓은 코드 상태
- 실제 클래스 기반으로 생성된 객체(인스턴스)는 각각 다른 멤버 변수 값을 가지게 됨
    
    가령, 학생의 클래스에서 생성된 각각의 인스턴스는 각각 다른 이름, 학번, 학년등의 값을 가지게 됨
    
- new 키워드를 사용하여 인스턴스 생성
   


## 힙 메모리

- 생성된 인스턴스는 동적 메모리(heap memory) 에 할당됨
- C나 C++ 언어에서는 사용한 동적 메모리를 프로그래머가 해제 시켜야 함 ( free() 난 delete 이용)
- 자바에서 Gabage Collector 가 주기 적으로 사용하지 않늠 메모리를 수거
- 하나의 클래스로 부터 여러개의 인스턴스가 생성되고 각각 다른 메모리 주소를 가지게 됨

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/FC03-java/POST1.png?raw=true)
   



## 참조 변수, 참조 값

```jsx
  Student studentLee = new Student();
  studentLee.studentName = "홍길동";

  System.out.println(studentLee);
```
   


## 용어 정리

    객체 : 객체 지향 프로그램의 대상, 생성된 인스턴스

    클래스 : 객체를 프로그래밍 하기위해 코드로 정의해 놓은 상태

    인스턴스 : new 키워드를 사용하여 클래스를 메모리에 생성한 상태

    멤버 변수 : 클래스의 속성, 특성

    메서드 : 멤버 변수를 이용하여 클래스의 기능을 구현한 함수

    참조 변수 : 메모리에 생성된 인스턴스를 가리키는 변수

    참조 값 : 생성된 인스턴스의 메모리 주소 값
   
<br>
<br>

# 예제 분석

```jsx
package ch04;

public class Student {

//	클래스 속성 선언한다.
	public int studentID;
	public String studentName;
	public String address;
	
//	클래스의 메서드를 만든다.
	public void showStudentinfo() {
		System.out.println( studentID + " 학번의 학생의 이름은 " + studentName + "이고, 주소는 " + address + "입니다.");
	}
	public String getStudentName() {
		return studentName;
	}
	public void setStudentName(String name) {
		studentName = name;
	}
	
}
```

<br>


```jsx
package ch04;

public class StudentTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		//크키가 정해져 있기 때문에 그냥 써도 된다. 하지만 class의 경우 사이즈가 정해져 있지 않기 
		//때문에 정의해줘야한다.
		//int num; 
		
		//class를 기반으로 여러개의 인스턴스가 생긴다(studnetLee)
		//다른 말로 참조 변수라고 칭한다. 
		// 참조변수의 역할은 생성되는 메모리의 위치를 나타낸다. 
//		타입은 student고, studentLee라는 변수가 선언되었다. 
		Student studentLee = new Student();
		
		//클래스를 생성한다. 
		studentLee.studentID = 12345;
		studentLee.setStudentName("Lee");
		studentLee.address = "서울 강남";
	
		studentLee.showStudentinfo();
//		만든 인스턴스들을 호출한다. 
		
		Student studentPark = new Student();
		
		studentPark.studentID = 180506;
		studentPark.setStudentName("Park");
		studentPark.address = "충북 제천";
		
		studentPark.showStudentinfo();
	}

}

//실행을 하기 위한 클래스를 만든다
```

<br>


```java

		System.out.println(studentLee);
		System.out.println(studentPark);
```

위의 코드를 찍어보면  

![스크린샷 2023-05-15 오후 6.00.16.png](https://github.com/solfany/solfany.github.io/blob/master/blog/FC03-java/POST2.png?raw=true)

콘솔에 이런 창이 하나 뜨는데 

```java
ch03.Student
```

해당 부분은 패키지의 이름과 클래스의 이름으로 풀네임이라고 하며 

```java
@3cb5cdba
```

> @ 뒤에 오는 값이 주소값이다.
참조값이라고도 하며, 레퍼런스 value이다. 
가르키는 주소가 가르키는 것은 student Lee와 Park이 자리잡은 어드레스주소를 
말하며, 실제 물리적인 주소가 아니고, 가상 어드레스를 말한다.
>

<br>
<br>


# 실습해보기

```java
package ch04;

public class Mango {

	public int mangoID;
	public String mangoName;
	public int mangoAge;
	public String mangoAddress;

	
	public void mangodans() {	
		System.out.println("품번" + mangoID +"는 " + mangoAge  + "년 산 망고이며, 이름은 " + mangoName + "(이)라고도 불립니다. 구매 문의는 " + mangoAddress +"시장으로 주세요 " );
	}

}
```

```java
package ch04;

public class MangTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Mango mangoS = new Mango();
		mangoS.mangoID = 0023;
		mangoS.mangoAge = 88;
		mangoS.mangoAddress = "강원도 강릉 ";
		mangoS.mangoName = "당망고 ";
		
		mangoS.mangodans();
	}

}
```

출력 결과
![스크린샷 2023-05-15 오후 6.09.13.png](https://github.com/solfany/solfany.github.io/blob/master/blog/FC03-java/POST3.png?raw=true)
