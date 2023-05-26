---
title: "[Java]Static, Instance"
categories:
  - Java
tags: [Java, Fastcampus]
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
