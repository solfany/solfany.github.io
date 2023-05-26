---
title: "[Java] 변수,상수,리터럴"
categories:
  - Java
tags: [Java, 자바의 정석]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/3..png?raw=true)

## 변수란(variable)

변하는 수?

하나의 값을 저장할 수 있는 메모리 공간

## 변수의 선언

1. 변수의 선언 이유

   값(data)을 저장할 공간을 마련하기 위해서

2. 변수의 선언 방법

   변수타입 변수이름;

```java
int age;
//정수(int)타입의 변수를 age(변수이름)를 선언
//자바는 모든 문장은 ;세미콜론으로 끝나야 한다.
```

## 변수에 값 저장하기

1. 변수에 값 저장하기

   ```java
   int age;  //정수(int)타입의 변수 age를 선언
   age = 25; //변수 age에 25를 저장

   /* 나의 해석
   age는 이름 뿐인 껍데기
   int 는 성질이 정수(숫자)인데
   int age  라는 것은 숫자타입의 x를 age 안에
   집어 넣겠다는 의미
   age=25; 라는 것은 즉, age라는 껍데기에 25라는
   정수를 선언한다.*/

   int age = 25; //위의 두 식을 간단하게 표기 할 수 있다
   ```

1. 변수의 초기화

   변수에 처음으로 값을 저장하는 것

```java
int x = 0;
int y = 5;
int x = 0,y = 5;
//","콤마를 통해 여러 변수를 한줄에 정의할 수 있음
```

1. 변수의 종류

   1. 클래스 변수
   2. 인스턴스 변수
   3. 지역 변수 - 지역변수의 경우 값이 자동 초기화 되지 않는다.

      읽기 전에 꼭 초기화 해야한다. (안하면 컴파일시 에러)

2. 변수의 값 읽어오기

   1. 변수의 값이 필요한 곳에 변수의 이름을 적는다

      ```java
      int year = 0, age = 14;
      	year = age + 2000;
      	year = 14 + 2000;
      	year = 2014;

      	age = age + 1; //변수의 값을 1증가시키는 방법
      	age = 14 + 1;
      	age = 15;

      System.out.println(age);
      System.out.println(15);
      ```

## 변수의 타입

1. 변수의 타입은 저장할 값의 타입에 의해 결정된다.

   ```java
   int age = 25;  //(정수타입) = (정수) 일치한다

   age = 3.14;   //(정수타입) = (실수)  불일치 한다
   ```

1. 저장할 값의 타입과 일치하는 타입으로 변수를 선언

```java
char //문자형 변수
ch = "가" ; //char는 문자 타입으로 일치한다

double //실수형 변수
double pi = 3.14; //double은 실수 타입으로 일치한다
```

## 값의 타입

### 값 \_ 8개의 기본형

1. 문자 - char
2. 숫자
   1. 정수 - byte, short, int, long
   2. 실수 - float, double
3. 논리 - boolean
   1. ture
   2. false

## 변수, 상수, 리터럴

변수 (variable) - 하나의 값을 저장하기 위한 공간 변경이 가능

상수(constant) - 한 번만 값을 저장 가능한 변수 변경이 불가능

↓ = 기존의 상수

리터럴 (literal) - 그 자체로 값을 의미하는 것

기존의 상수가 리터럴이다?

근데 왜 리터럴이라는 낯선 용어를 사용하는 것일까?

이유는 : 자바에서 상수를 한번만 값을 저장할 수 있는 변수라 정의 했기 때문이다.

```java
int score = 100;
		score = 200; // 변수는 score 클래스 안에 값을 변경 가능하다.

final int MAX = 100; /*MAX는 상수, 상수를 선언하는 방법은 변수와 같다 또한 변수 앞에
											final 이라는 키워드를 붙여야 선언이 가능하다. */
					MAX = 200; // 상수는 값을 선언하고 나면 값을 바꿀 수가 없기 때문에 에러가 난다

char ch = 'A';
Staring str = "abx";
```

리터럴은 주황 형광펜

변수는 초록 형광펜

상수는 보라 형광펜

### 상수 final 사용 시 문제점

```java
public class VarEx1 {
	public static void main(String[] args) {
		final int score = 100;  // final 상수 100으로 선언했기 때문에
		score = 200;  // 200으로 선언이 불가하다. 에러 발생

		System.out.println(score);
	}

}
```

## 리터럴의 접두사와 접미사

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/variable/1.png?raw=true)

**모든 값에는 타입이 있다.**

**그렇다면 리터럴의 타입 구별하는 방법은 ?**

실수형 특징 소수점 “.” 이 붙습니다.

문자형 특징 ‘ ’ **소 따옴표**로 감싸져 있음

문자열 특징 “ ” **따옴표**로 감싸져 있음

**정수와 실수는 타입이 여러개 이기 때문에 점미사를 이용해 구분한다.**

정수는 접미사 “L”(long 타입)을 사용한다. 그 외는 int 타입을 이용한다.

실수형은 점미사 ”f”, “d” 를 사용한다.

**char**타입의 변수는 **단 하나의 문자만 저장**할 수 있다.

하지만 **여러 문자열**을 저장하고 싶을 땐 **String** 타입을 사용해야한다.

문자열 리터럴은 “ “ 안에 아무런 문자도 넣지 않는 걸 허용한다. empty string 라고 한다.

그러나 문자 리터럴은 반드시 ‘ ‘ 안에 하나의 문자가 있어야 한다.

String 은 클래스 이기 때문에 아래와 같이 객체를 생성하는

연산자 new를 사용해야 하지만 아래와 같은 표현도 허용한다.

```java
String name = new String("java"); //string 객체 생성
String name = "java";  //위의 문장을 간단히, 둘의 차이점은 ?
```

숫자 뿐만이 아닌 아래와 같이 두 문장을 합칠 때도 + 기호를 사용할 수 있다.

```java
String name = "ja" + "va";   //덧셈 연산자는 피연산자가 둘다 숫자일 때 사용 가능하지만,
String str = name + 8.0;
// 한쪽만 string 일 경우 두 숫자 모두 string로 변환해준 후 결합한다.
// 어떤 타입의 변수이던 문자열과 덧셈연산을 사용가능하다. = 문자열로 변경

String name = "중간" + " " + "공백";
// ' '따옴표 안에 담긴 공백도 문자열로 취급되어 연산이 가능하다.
중간 공백
// 출력결과
```

x, y 변수에 저장된 값을 서로 바꿀려면?

```java
int x = 10;
int y = 20;
```

w,y에 담긴 내용물을 바꾸려면 빈 공간이 필요하다.

```java
int tem;   //임시로 값을 저장하기 위한 빈 공간(변수)
tem = x;   // x의 값을 tem에 저장
x = y;    // y의 값을 x에 저장
y = tem;  // tem에 저장된 값을 y에 저장
```

왼쪽에서 오른쪽으로 옮긴다 라고 생각하면 이해하기 쉬울 것이다.
