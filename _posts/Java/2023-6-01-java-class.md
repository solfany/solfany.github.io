---
title: "[Java] 클래스 구성 요소와 생성자"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/3..png?raw=true)

## 클래스 밖에 올 수 있는 3가지

1. package - java 파일의 폴더 (패키지) 위치 - default 의 경우 폴더가 생성되지 않음
2. inport - 다른 폴더 (패키지) 위치의 클래스를 참조
3. 외부 클래스 (external class)

   3-1. 외부에 포함된 또 다른 클래스

   3-2. public 키워드를 사용할 수 없음

<br>
<br>

## 클래스 안에 올 수 있는 4가지

1. 필드(멤버) - 클래스 특징(속성)을 나타내는 변수 (int age = 20)
2. 메서드 (멤버) - 클래스의 기능 (void working(){…})

   2-1. 리턴 타입 + 메서드 이름 + () + {} 로 구성

3. 생성자

   3-1. 객체 생성 기능 (생성자이름 + () + {}) - 생성자 이름은 클래스 이름과 동일하여야 합니다.

   3-2. 메서드 이지만 반환형이 없는 형태이다.

4. 내부 클래스 (inner class)(멤버)

   4-1. 클래스 내부 정의된 클래스

<br>
<br>

## 기본 생성자의 자동 추가

- 생성자 이름하고 똑같다
- 매개변수 없다
- 반환형이 없다.

<br>
<br>

## 예제

```java
package ch06;

// A 클래스는 에나서 임시 D클래스로 설정
	class D {
		int m;
		void work() {
			System.out.println(m); //0
		}
		// 컴파일러가 자동으로 추가해주는 기본 생성자
//		A()
//		{
//			객체 생성 이후에 해야 할 추가 일
//		}

		}
	class B {
		int m;
		void work() {
			System.out.println(m);
		}
		B(){ //기본 생성

		}
	}
	class C{
		int m;
		void work() {
			System.out.println(m); // 생성자로 넘어온 값
		}	// 오버로딩 된 생성
		C(int a){	//생성자의 기본 기능 : 객체 생성 + 필드 초기화
		m=a;
		}
	}
public class DefaultConstructor {

	public static void main(String[] args) {
//		#1. 클래스의객체 생성
		 D d = new D();
// 클래스참조 변수 = new(Heep 메모리에 넣어라)
//	A(); 생성자 --> 출력값은 객체 (필드, 매서드, 이너 클래스 등)
		B b = new B();
		// C c = new C(); // 불가능
		C c = new C(3);
		//#2. 매서드 호출
		d.work();
		b.work();
		c.work();
	}

}
```

<br>

## 이슈 사항

**아래의 코드가 오류가 나는 이유를 알아보자 ?**

```java
 C c = new C();
```

> 해당 코드에서 **`C c = new C();`**가 오류가 나는 이유는 **`C`** 클래스에 매개변수가 있는 생성자 **`C(int a)`**만 정의되어 있기 때문이다.
>
> 생성자를 직접 정의하면 컴파일러는 기본 생성자를 자동으로 추가하지 않는다.
>
> 따라서 매개변수가 없는 기본 생성자 **`C()`**를 사용하려면, **`C`** 클래스에서 기본 생성자를 명시적으로 정의해야 한다.
