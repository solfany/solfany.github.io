---
title: "[Java] Unhandled exception type IOException 에러 발생 원인"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![image](https://github.com/solfany/solfany.github.io/assets/123814718/20775dd8-de4d-47b2-8187-0878688831f8)


<aside style="background-color: #f7dce0; font-size: 0.6rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
[Java] Unhandled exception type IOException 에러 발생 원인
</aside>

# 

※ 예외 클래스 상속도

![image](https://github.com/solfany/solfany.github.io/assets/123814718/45108dd1-bdb3-4594-bd2e-6d9d68c21109)
---

<예외 처리 방법>

1. 직접 처리 : **try ~ catch**    -> 더 효율적!

2. 선언 처리 : throws

**[try ~ catch]**

사용법 :

try {

예외 발생 예상 코드

} catch(해당예외클래스 e) {

예외 처리 코드

}

=> 구체적인 예외 처리가 가능!

try문 내에서 예외 발생 시 아래에 있는 코드는 실행하지 않고 try문을 빠져나옴

그러므로 예외가 발생하더라도 실행해야하는 코드가 있다면 finally문 사용!!!

catch문을 여러 개 사용할 때 해당예외클래스가 상위일수록 아래에 배치해야 한다!

**[finally]**

예외가 발생하더라도 꼭 실행해야 하는 코드는 finally문을 사용하여 작성한다!

(-> try ~ catch 문은 예외가 발생하면 그 이후의 코드는 실행되지 않기 때문)

try ~ catch 문과 함께 사용한다.

- 예외 발생 시 DB와의 접속을 완전히 종료하므로 DB의 효율을 높여줌

**[throws]**

사용법 :

예외발생메소드() throws 해당예외클래스 {

예외발생예상코드

}

throws를 달아놓은 메소드는 내부에서 예외가 발생할 것임을 알려주는 것.

throws는 예외 처리를 직접하지 않고 메소드를 호출하는 곳에서 하도록 한다

- > 메소드 내부에서 예외를 발생시키고, 해당 메소드를 호출하는 곳에서 예외 처리를 하도록 함!!

*ex)*

```java
package ExceptionExs;

public class ExceptionEx {
	public static void main(String[] args) {
		ThrowEx th = new ThrowEx();

        // 해당 메소드를 실행하는 부분에서 예외 처리
        try {
			th.throwSample(12);
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
}

class ThrowEx{
	public void throwSample(int n) throws Exception {
			if(n > 10)
				throw new Exception("n값이 10보다 크다");		// 예외 발생
	}
}
```

*실행 결과 >*

java.lang.Exception: n값이 10보다 크다

at ExceptionExs.ThrowEx.throwSample(ExceptionEx.java:18)

at ExceptionExs.ExceptionEx.main(ExceptionEx.java:7)

main 메소드의 try문 내에서 예외가 발생하여 catch문이 실행되었고,

발생한 예외의 내용이 'throw new Exception' 부분에서 작성한대로 "n값이 10보다 크다"라고 출력되는 것을 알 수 있다.

*심화)*

```java
class ThrowEx{
	public void throwSample(int n) throws IllegalArgumentException {
		if(n > 10)
				throw new IllegalArgumentException("n값이 10보다 크다");

        int var = System.in.read();
	}
}
```

이전 예시에서 ThrowEx 클래스의 throws Exception을 throws IllegalArgumentException 으로 바꾸고, 메소드 내에 int var = System.in.read(); 라는 코드를 추가하였다.

그랬더니 새로 추가한 줄에 'Unhandled exception type IOException'이라는 오류가 뜬다.

throwSample 메소드는 throws IllegalArgumentException라고 작성하였으므로 IllegalArgumentException이라는 예외클래스만을 다룬다.

그렇기 때문에 System.in.read 메소드를 실행할 때 발생할 수 있는 예외클래스 IOException를 다루지 않으므로 이런 오류가 발생하는 것이다.

이에 대한 해결은 IOException 예외클래스를 다룰 수 있도록 'throws IllegalArgumentException , IOException'으로 고쳐주면 된다.

---

발생한 예외에 대해 출력하고 싶다면

=> catch문 내에 e.getMessage() 출력 / e.toString() 출력 / e.printStackTrace() 실행

(자세한 정도 : getMessage < toString < printStackTrace)

---

# 중요★

(1) **예측 가능한 예외** **- checked Exception** 

*(예: IOException, ClassNotFoundException)*

: 컴파일 시 체크함  (-> 예외 처리 안 해주면 오류 발생)

throws와 try~catch로 반드시 예외 처리해줘야 함!!

(2) **예측 불가한 예외** **- unchecked Exception (Runtime Exception)**

*(예: ArithmeticException, NullPointerException, IndexOutOfBoundsException)*

: 컴파일 시 체크하지 않음  (-> 예외 처리 안 해도 오류는 발생하지 않음)

명시적으로 예외 처리 해주지 않아도 됨 (throws 사용 안함)

# 

---

*실습1.*  < IOException 예외 처리하기 >

방법1) try~catch 이용

```java
void IOExc1() {
		try {
			throw new IOException();
		} catch (IOException e) {
			e.printStackTrace();
		}
}
```

방법2) throws 이용

```java
void IOExc2() throws IOException{
      throw new IOException();
}
```

*실습2.*  < ArithmeticException 예외 처리하기 >

(※ 상속관계 : Exception > RuntimeException > ArithmeticException)

방법1) Exception 예외클래스 이용

```java
public class ExceptionEx {
	public static void main(String[] args) {
		Divide di = new Divide();
		di.setNumber(5, 0);

		try {
			di.divide();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

class Divide {
	int n1, n2;

	public void setNumber(int n1, int n2) {
		this.n1 = n1;
		this.n2 = n2;
	}

	public void divide() throws Exception {
		if(this.n2 == 0 )
		{
			throw new Exception("예외 발생 : 0으로 나눔");
		}

		System.out.println(this.n1 / this.n2);
	}
}
```

RuntimeException이 아닌 모든 예외클래스는 컴파일 시 체크되므로 Exception 예외클래스도 컴파일 시 체크된다.

따라서, 예외 발생 메소드명 뒤에 'throws Exception'을 써주고, 해당 메소드를 호출하는 main 메소드 내 'di.divide();' 라는 코드를 try~catch문으로 예외처리 해주어야 한다.

방법2) RuntimeException 예외클래스 이용  (ArithmeticException를 이용해도 동일)

```java
public class ExceptionEx {

	public static void main(String[] args) {
		Divide di = new Divide();
		di.setNumber(5, 0);

		di.divide();
}

class Divide {
	int n1, n2;

	public void setNumber(int n1, int n2) {
		this.n1 = n1;
		this.n2 = n2;
	}

	public void divide() {
		if(this.n2 == 0 ) {
			throw new RuntimeException("예외 발생 : 0으로 나눔");
		}

		System.out.println(this.n1 / this.n2);
	}
}
```

RuntimeException 예외클래스와 그 하위 클래스들은 컴파일 시 체크되지 않으므로 예외처리를 명시해주지 않아도 된다.

따라서, 예외가 발생하는 divide 메소드명 뒤에 'throws RuntimeException'을 쓰지 않아도 된다.

또한, throw한 코드에 대해 catch를 하지 않아도 되기 때문에 해당 메소드 실행문 'di.divide();'를 try~catch로 예외처리 하지 않아도 된다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}