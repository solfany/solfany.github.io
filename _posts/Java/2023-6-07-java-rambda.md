---
title: "[Java] 람다식(Lambda Expression)"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)

# 람다식 (Lambda Expression)이란?

> Stream 연산들은 매개변수로 함수형 인터페이스(Functional Interface)를 받도록 되어있다.
>
> 그리고 람다식은 반환값으로 함수형 인터페이스를 반환하고 있다. 그렇기 때문에 우리는 Stream API를 정확히 이해하기 위해 람다식과 함수형 인터페이스에 대해 알고 있어야 한다.

JDK 8 부터 도입한 함수형 프로그래밍 기법 중 하나

자바는 무명 구현 객체 대신에 람다식을 매서드의 인수로 사용하도록 허용한다.

람다식은 메서드를 감싼 무명 구현 객체를 자바가 전달 할 수 있는 코드 블록처럼 흉내 낸 것

자바는 무명 구현 객체를 람다식으로 표현해 함수형 프로그래밍을 모방한 것

람다식을 사용하면 무명 객체보다 프로그램의 간결성 및 가독성이 향상된다.

매개변수가 하나 있다면 괄호를 생략 가능하다

실행문이 하나라면 중괄호와 세미콜론을 생략가능

단, 실행문이 return 문이면 return키워드도 생략

```java
(타입 매개변수) -> {실행문; 실행문;}
```

선언부, 2개 이상의 매개변수를 콤마로 연결 할 수 있다.

자바는 새로운 함수 문법을 정의한 거시 아니라 이미 있는 인터페이스를 빌어 람다식을 표현

**함수는 인터페이스의 메서드만 람다식 표현 가능**

---

람다식(Lambda Expression)이란 함수를 하나의 식(expression)으로 표현한 것이다. 함수를 람다식으로 표현하면 메소드의 이름이 필요 없기 때문에, 람다식은 익명 함수(Anonymous Function)의 한 종류라고 볼 수 있다.

익명함수(Anonymous Function)란 함수의 이름이 없는 함수로, 익명함수들은 모두 일급 객체이다.
일급 객체인 함수는 변수처럼 사용가능하며 매개 변수로 전달이 가능하는 등의 특징을 가지고 있다.

기존의 방식에서는 함수를 선언할 때 다음과 같이 선언하였다.

### 기존 방식

```java
리턴 타입 매서드 이름(입력매개변수){
	//매서드 내용
}
```

위의 식을 아래의 코드로 표현할 수 있다.

```java
A a = new A() {
		void abc() {
			//메서드내용
		}
	};
```

익명 이너 클래스

<br>

---

<br>

### 람다식 변환

```java
(타입 매개변수) -> {실행문; 실행문;}
```

위의 식을 아래의 코드로 표현할 수 있다.

```java
A a = () -> {
	//매서드 내용
};
```

하지만 람다 방식으로는 위와 같이 메소드 명이 불필요하며, 다음과 같이 괄호() 와 화살표-> 를 이용해 함수를 선언하게 된다.

```java
() 매개변수 리스트에는 함수에 전달되는 매개변수들이 나열

애로우 토큰 (→)

애로우 토큰은 매개변수 리스트와 함수 코드를 분리시키는 역할이다.

{} 함수 바디

함수 바디는 함수의 코드이다.
```

<br>
<!-- 
<!--
# 람다식(Lambda Expression) 의 특징

> 람다식 내에서 사용되는 지역변수는 final이 붙지 않아도 상수로 간주된다.
> 람다식으로 선언된 변수명은 다른 변수명과 중복될 수 없다.

### 람다식(Lambda Expression) 의 장점

1. 코드를 간결하게 만들 수 있다.
2. 식에 개발자의 의도가 명확히 드러나 가독성이 높아진다.
3. 함수를 만드는 과정없이 한번에 처리할 수 있어 생산성이 높아진다.
4. 병렬프로그래밍이 용이하다.

### 람다식(Lambda Expression) 의 단점

1. 람다를 사용하면서 만든 무명함수는 재사용이 불가능하다.
2. 디버깅이 어렵다.
3. 람다를 남발하면 비슷한 함수가 중복 생성되어 코드가 지저분해질 수 있다.
4. 재귀로 만들경우에 부적합하다.

결국 무조건 람다가 좋다는 보장은 없다. 상황에 따라 필요에 맞는 방법을 사용하는 것이 중요하다.

<br>
<br>

# 예제

## 람다식으로 내림차순 표현하기

```java

package ch10;

import java.util.Arrays;

public class Ex_05 {
    public static void main(String[] args) {
        String[] strings = { "로마에 가면 로마법을 따르라. ", "시간은 금이다. ", "펜은 칼보다 강하다. "};

        // Arrays.sort 메서드를 사용하여 문자열을 오름차순으로 정렬합니다.
        // Comparator를 람다식으로 표현하여 문자열의 길이를 기준으로 정렬합니다.
        Arrays.sort(strings, (first, second) -> first.length() - second.length());

        // 정렬된 문자열을 출력합니다.
        for (String s : strings)
            System.out.println(s);
    }
}
```

인터페이스 구현한 부분을 람다식으로 바꾸어 할당 (대입 )한 것이다.
람다식은 기본적으로 함수를 만들어 사용하는 것이다.

배열을 정렬하는데 사용될 Comarator 객체 : 람다식 객체
Comparator 의 compare()매소드구현

compare() 매소드는 두개의 인자를 받아, 첫번째 인자가 두번째 인자보다
작으면 음수, 같으면 0, 크면 양수를 반환한다.

문자열의 길이가 짧은 순으로 정렬

```java
sort(Strings, (first, second) -> strings(매소드의 첫번째 인자) 배열
first, second) 람다식은 두번째 인자이다. (매개변수) -> 매소드의 내용
```

<br>
<br>

## 매개변수 없는 매소드를 구현할 때

인터페이스 객체명을 f로 선언하고 매개변수 괄호에 아무 것도 없이 화살표로 동작을 구현하면 된다.

<br>

---

<br>

1. 예제

```java
package ch10;

interface MyFunctuin2{
	void print();
}

public class Ex_06 {
    public static void main(String[] args) {

    	MyFunctuin2 f = () -> {
    	System.out.println("Hello");
    	};
    	f.print();

    	// 한 번 구현된 매소드를 재 (사용) 구현할 수도 있다
    	f = () -> {
    		System.out.println("안녕 ");
    	};
    	f.print();
    }
}
```

<br>
<br>

2. 예제

```java
package ch10;

interface A {
    void abc();
}

class B {
    void bcd() {
        System.out.println("메서드");
    }
}

public class Ex_07 {
    public static void main(String[] args) {
        //#1. 인스턴스 메서드 참조 타입 1: 익명 이너 클래스
        A a1 = new A() {
            @Override
            public void abc() {
                B b = new B();
                b.bcd(); // 'bcd' 메서드를 호출
            }
        };

        //#2. 람다식
        A a2 = () -> {
            B b = new B();
            b.bcd();
        };

        //#3. 인스턴스 참조 타입 1의 표현
        B b = new B();
        A a3 = b::bcd;
        // 람다식 () -> b.bcd()의 축약형

        // 인스턴스 'bcd' 메서드를 참조하여 인터페이스 A의 'abc' 메서드 정의
        a1.abc();
        a2.abc();
        a3.abc();
    }
}
```

> 이렇게 람다식이 등장하게 된 이유는 불필요한 코드를 줄이고, 가독성을 높이기 위함이다.
> 그렇기 때문에 함수형 인터페이스의 인스턴스를 생성하여 함수를 변수처럼 선언하는 람다식에서는 메소드의 이름이 불필요하다고 여겨져서 이를 사용하지 않는다.
> 대신 컴파일러가 문맥을 살펴 타입을 추론한다.
> 또한 람다식으로 선언된 함수는 1급 객체이기 때문에 Stream API의 매개변수로 전달이 가능해진다. --> -->
