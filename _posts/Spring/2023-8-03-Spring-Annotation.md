---
title: "[Spring Boot]어노테이션(Annotation)이란?"
categories:
  - Spring
tags: [Java, Spring, Annotation]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

### **1. 어노테이션(Annotation)이란?**

- **자바 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종.**
- 보통 @ 기호를 앞에 붙여서 사용.(컴파일러는 컴파일 시 @문자로 시작이 되면 어노테이션으로 판단하여 진행)
- JDK 1.5 버전 이상부터 사용 가능.

```java
//	Example@RequiredArgsConstructor
@GetMapping
@Entity
	...
```

- 클래스, 인터페이스, 메소드, 메소드 파라미터, 필드, 지역 변수 위에 작성하여 사용.
- 값을 저장할 수 있는 엘레먼트를 가지고, 어노테이션 이름 다음에 괄호 안에 엘레먼트를 정의.

```java
@Entity(name = "MEMBER_TABLE")
```

### **1-1. 어노테이션의 용도**

- 컴파일러에게 코드 작성 문법 에러를 체크하도록 정보를 제공.
- 소프트웨어 개발툴이 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보 제공.
- 실행 시(런타임 시) 특정 기능을 실행하도록 정보를 제공.

### **2. 어노테이션 사용 순서**

1. 어노테이션 정의
2. 어노테이션 배치

### **2-1. 어노테이션 정의**

- 어노테이션을 적용할 때는 어노테이션이 어디(클래스, 메소드, 파라미터 등)에 적용되며, 언제까지 어노테이션 소스가 유지될 것인지를 설정해야 한다.
- 아래와 같이 어노테이션을 정의 할 수 있다.

```java
@Target({ElementType.[적용대상]})//  클래스, 파라미터, 메소드 등@Retention(RetentionPolicy.[정보유지되는 대상])//  런타임, 클래스, 소스public @interface [어노테이션명]{
    public 타입 elementName() [default 값]
    	...
}
```

- 예를 들어보자면, 우리가 자주 사용하는 룸북에서 제공하는 생성자 관련 어노테이션을 볼 수 있다.

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.SOURCE)
public @interface RequiredArgsConstructor {
	....
}
```

- @Target 에는 어느 위치(클래스, 파라미터, 메소드 등)에 어노테이션을 적용할지 작성한다.
- @Retention 에는 언제까지 어노테이션을 유지할 것인지 작성한다.

> @Retention 어노테이션은 보통 Runtime 을 많이 사용하고 있어, 어노테이션을 확인하다 보면 Retention 값이 RUNTIME 으로 되어 있는 것을 확인할 수 있다.

### **2-2. 어노테이션 배치.**

- 어노테이션의 사용은 클래스를 참고하는 소스의 흐름상에서 Reflection 을 사용하는 방법을 통해 활용한다.
- 해당 내용을 이해하기 위해 간단하게 예제를 작성해서 확인해보고자 한다.
- 추가로 코드가 실행되는 중 Reflection(리플렉션)을 이용하여 추가 정보를 통해 기능 동작도 확인한다.

> Reflection(리플렉션)???

- JaewonAnnotation.java (어노테이션)

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface JaewonAnnotation {
    String value() default "-";
    String str() default "Test Jaewon Annotation :)";
}
```

- TestAnnotationService.java (어노테이션을 사용하고자 하는 클래스)

```java

public class TestAnnotationService {
    @JaewonAnnotation
    public void test1() {
        System.out.println("테스트1");
    }

    @JaewonAnnotation("***")
    public void test2() {
        System.out.println("테스트2");
    }

    @JaewonAnnotation(value = "Test", str = "JaewonAnnotaion 테스트 입니다!!!")
    public void test3() {
        System.out.println("테스트3");
    }
}
```

- TestMain.java (TestAnnotationService.java 를 사용하는 클래스)

```java

import java.lang.reflect.Method;

public class TestMain {

    public static void main(String[] args){

        Method[] methodList = TestAnnotationService.class.getMethods();

        for(Method method : methodList) {
//  어노테이션 적용 여부 확인if(method.isAnnotationPresent(JaewonAnnotation.class)) {
                System.out.println("Method Name : " + method.getName());
                JaewonAnnotation annotation=method.getDeclaredAnnotation(JaewonAnnotation.class);

                String value = annotation.value();
                String str = annotation.str();
                System.out.println("Value : " + value);
                System.out.println("Str : " + str);
            }
        }
    }
}
```

- TestMain 을 실행하게 되면 결과는 아래와 같다.

```java

Method Name : test1
Value : -
Str : Test Jaewon Annotation :)
Method Name : test2
Value : ***
Str : Test Jaewon Annotation :)
Method Name : test3
Value : Test
Str : JaewonAnnotaion 테스트 입니다!!!
```

### **3. 어노테이션의 종류**

- 어노테이션에도 종류가 존재한다.
- 표준(내장) 어노테이션 : 자바가 기본적으로 제공하는 어노테이션
- 메타 어노테이션 : 어노테이션을 위한 어노테이션
- 사용자 정의 어노테이션 : 사용자가 직접 정의(생성)하는 어노테이션

### **3-1. 표준(내장) 어노테이션**

- 7개의 표준 어노테이션 중에 3개가 java.lang 의 일부이고, 나머지 4개는 java.lang.annotation 으로부터 가져온다.
- @Override오버라이딩을 올바르게 했는지 컴파일러가 체크.Override 는 오버라이딩 시, 메서드의 이름을 잘못되었는지 확인한다.

```java

      <java />

//	부모 클래스class Parent {
    void parentMethod(){}
}

//	자식 클래스(부모 클래스 상속)class Child extends Parent {
    @Override
    void parentMethodTest(){}//	컴파일 에러 발생! 오버라이드 메소드명이 틀림
}
```

- @Deprecated앞으로 없어지거나, 사용하지 않을 것을 권장하는 필드나 메서드에 사용.StringUtils.~~isEmpty~~() 과 같이 밑줄이 그어져 있지만, 사용은 가능한 것을 종종 확인할 수 있다.

> 그러나 나중에 버전업시 어느 순간 메소드가 사라져 있을 수 있다.

```java

      <java />

@Deprecated
public static boolean isEmpty(@Nullable Object str) {
    return (str == null || "".equals(str));
}
```

- @FunctionalInterfaceJava 8 부터 지원하는, 함수형 인터페이스를 지정하는 어노테이션.함수형 인터페이스의 하나의 추상 메서드만 가져야 한다는 제약을 확인.메서드가 존재하지 않거나, 1개 이상의 메서드(default 메서드 제외) 가 존재할 경우 컴파일 오류를 발생.
- @SuppressWarnings선언한 곳의 컴파일 경고를 무시하도록 하는 어노테이션.

```java

      <java />

@SuppressWarnings("unchecked")
ArrayList list = new ArrayList();// 제네릭 타입을 지정하지 않음
list.add(obj);// 경고 발생 !!!(UnChecked)
```

### **3-2. 메타 어노테이션**

- @Target@Target 에는 어느 위치(클래스, 파라미터, 메소드 등)에 어노테이션을 적용할지 작성한다.

| ElementType 열거 상수 | 적용 대상                     |
| --------------------- | ----------------------------- |
| TYPE                  | 클래스, 인터페이스, 열거 타입 |
| ANNOTATION_TYPE       | 어노테이션                    |
| FIELD                 | 필드                          |
| CONSTRUCTOR           | 생성자                        |
| PARAMETER             | 파라미터                      |
| METHOD                | 메소드                        |
| LOCAL_VARIAblE        | 로컬 변수(지역 변수)          |
| PACKAGE               | 패키지                        |

- @Retention@Retention 에는 언제까지 어노테이션을 유지할 것인지 작성한다.

| RetentionPolicy 열거 상수 | 설명                                                                                                                             |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| RUNTIME                   | 바이트 코드 파일(컴파일/빌드파일)까지 어노테이션 정보를 유지하여,  리플렉션을 이용해서, 런타임에 어노테이션 정보를 얻을 수 있다. |
| CLASS                     | 바이트 코드 파일까지 어노테이션 정보를 유지하지만, 리플렉션을 이용해서  런타임에 어노테이션 정보를 얻을 수 없다.                 |
| SOURCE                    | 소스상에서만 어노테이션 정보를 유지한다.  소스코드를 확인할 때만 의미가 있고, 바이트 코드 파일에는 정보가 남지 않는다.           |

- @Documented해당 어노테이션을 JavaDoc 에 포함시킨다.
- @Inherited어노테이션도 상속이 가능하다.어노테이션을 자식 클래스에 상속하고자 할 때 해당 어노테이션을 작성한다.

```java

      <java />

@Inherited
@interface SuperAnno{}

@SuperAnno
class Parent{}

//	SuperAnno 가 붙은 것으로 인식class Child extends Parent{}
```

- @RepeatableJava 8 부터 지원하고, 연속적으로 어노테이션을 선언할 수 있게 한다.

### **3-3. 사용자 정의 어노테이션**

- 위 2번 항목에서 예제로 생서안 것을 참고하면 된다.

### **4. 어노테이션 요소 특징**

- 적용시 값을 지정하지 않으면, 사용될 수 있는 기본값을 지정할 수 있다.
- 요소가 하나이고 이름이 value 라면 어노테이션 작성 시 요소의 이름은 생략이 가능하다.

```java

      <java />

//	요소가 생략되면 default 값@JaewonAnnotation
public void test1() {
}

//	요소가 하나이고 이름이 value 라면 이름 생략 가능@JaewonAnnotation("***")
public void test2() {
}

//	요소가 하나가 아니면 이름 생략 불가능@JaewonAnnotation(value = "Test", str = "JaewonAnnotaion 테스트 입니다!!!")
public void test3() {
}
```

- 요소의 타입이 배열인 경우 중괄호{} 를 사용해야 한다.

```java

      <java />

@interface TestAnnotation{
	String[] strArr();
}

//	요소가 배열이면 중괄호를 통해 선언한다.@TestAnnotation(strArr={"Test", "Annotation"})

//	요소가 1개일 때는 {}를 사용하지 않아도 된다.@TestAnnotation(strArr="Hello Annotation")

//	요소가 없으면 {}를 써넣어야 한다.@TestAnnotation(strArr={})
```

### **5. 어노테이션 규칙**

- 어노테이션에서도 지켜야하는 규칙이 있다.

1. 요소의 타입은 기본형, String, Enum, 어노테이션, Class 만 허용
2. 괄호() 안에 매개변수를 선언할 수 없다.
3. 예외를 선언 할 수 없다.
4. 요소의 타입을 매개변수로 정의할 수 없다.(<T>)
