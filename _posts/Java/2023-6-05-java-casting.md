---
title: "[Java] 다운캐스팅과(Downcasting) 업캐스팅(Upcasting)"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/3..png?raw=true)



> 자바에서 업 캐스팅과 다운 캐스팅은 상속 관계에 있는 클래스 간의 타입 변환을 의미
> 

## 업 캐스팅 (Upcasting):

- 부모 클래스의 객체를 자식 클래스의 타입으로 변환하는 것이다.
- 업 캐스팅은 자동으로 이루어집니다. 즉, 명시적인 타입 변환 없이 부모 클래스의 객체를 자식 클래스의 타입으로 참조할 수 있습니다.
- 업 캐스팅을 통해 부모 클래스의 필드와 메소드에 접근할 수 있지만, 자식 클래스에서 추가된 필드와 메소드에는 접근할 수 없습니다.

## 다운 캐스팅 (Downcasting):

- 부모 클래스의 객체를 자식 클래스의 타입으로 변환하는 것입니다.
- 다운 캐스팅은 명시적인 타입 변환을 해주어야 합니다.
- 다운 캐스팅을 통해 자식 클래스의 필드와 메소드에 접근할 수 있습니다.
- 다운 캐스팅은 업 캐스팅된 객체에 대해서만 수행할 수 있습니다. 그렇지 않은 경우 ClassCastException이 발생할 수 있습니다.
- 다운 캐스팅을 시도하기 전에 instanceof 연산자를 사용하여 실제 참조하는 객체가 해당 클래스의 인스턴스인지 확인하는 것이 좋습니다. 이를 통해 예외 상황을 방지할 수 있습니다.

> 업 캐스팅은 일반적으로 다형성을 활용하여 객체를 유연하게 다룰 수 있게 해주는 기능이며, 다운 캐스팅은 필요한 경우에 한정하여 자식 클래스의 특정 기능에 접근할 수 있도록 해준다
> 

<br>    
<br>    

## 예제

```java
package ch08;

class Parent {
    public void sayHello() {
        System.out.println("Hello from Parent");
    }
}

class Child extends Parent {
    public void sayHello() {
        System.out.println("Hello from Child");
    }

    public void sayGoodbye() {
        System.out.println("Goodbye from Child");
    }
}

class Downcasting {
    public static void main(String[] args) {
        Parent p = new Child(); // 업캐스팅: Child 객체를 Parent 타입으로 참조

        p.sayHello(); // 출력: Hello from Child (Child 클래스의 메서드가 실행됨)

        if (p instanceof Child) { // p가 Child 클래스의 인스턴스인지 확인
            Child c = (Child) p; // 다운 캐스팅: Parent 타입을 Child 타입으로 형변환
            c.sayGoodbye(); // 출력: Goodbye from Child (Child 클래스의 메서드가 실행됨)
        }
    }
}
```

1. **`Parent`** 클래스와 **`Child`** 클래스가 정의되어 있다. 
2. **`Parent`** 클래스에는 **`sayHello()`** 메서드가 정의되어 있고, **`Child`** 클래스는 이를 오버라이딩한다.  
또한 **`Child`** 클래스에는 **`sayGoodbye()`** 메서드가 추가로 정의되어 있다. 
3. **`Downcasting`** 클래스의 **`main()`** 메서드에서 **`Parent`** 타입의 변수 **`p`**를 선언하고, **`Child`** 객체를 생성하여 **`p`**에 대입한다. 
이러한 형태는 업캐스팅이라고 불립니다. **`Child`** 객체는 **`Parent`** 타입으로 참조될 수 있다.
4. **`p.sayHello()`**를 호출하면, 실행 시점에서 객체의 실제 타입을 기준으로 메서드가 실행되므로 출력 결과는 "Hello from Child"가 됩니다. 즉, 다형성의 특성을 확인할 수 있다 f.
5. **`p`**가 **`Child`** 클래스의 인스턴스인지 확인하기 위해 **`instanceof`** 연산자를 사용합니다. 조건문을 통과하면 **`p`**를 **`Child`** 타입으로 다운 캐스팅하여 **`Child`** 타입의 변수 **`c`**에 대입한다.
6. **`c.sayGoodbye()`**를 호출하면, 다운 캐스팅이 정상적으로 이루어져 **`Child`** 클래스의 메서드가 실행되어 "Goodbye from Child"가 출력된다. 

<br>    

> 이를 통해 업캐스팅과 다운 캐스팅의 개념을 이해할 수 있다. 
 업캐스팅은 하위 클래스 객체를 상위 클래스 타입으로 참조하는 것이며, 다운 캐스팅은 상위 클래스 타입을 다시 하위 클래스 타입으로 형변환하는 것이다.
> 

<br>    
<br>    


# 자세히 알아보기 

## **자바의 참조형 캐스팅**

하나의 데이터 타입을 다른 타입으로 바꾸는 것을 타입 변환 혹은 **형변환(캐스팅)** 이라고 한다.

자바의 데이터형을 알아보면 크게 두가지로 나뉘게 된다.

- 기본형(primitive type) - Boolean Type(boolean) - Numeric Type(short, int, long, float, double, char)
- 참조형(reference type) - Class Type - Interface Type - Array Type - Enum Type - 그 외 다른 것들

기본형(primitive) 이든 참조형(referece) 이든 하나의 타입이다. 이는 즉, 서로 타입간의 형변환(casting)이 가능하다는 말이다.

기본적으로 자바에선 대입 연산자 ~~=~~ 에서 변수 와 값 서로 양쪽의 타입이 일치하지 않으면 할당이 불가능하다. 프로그램에서 값의 대입이나 연산을 수행할 때는 같은 타입끼리만 가능하기 때문이다.

```java
long d = 10.233;// ERRORCopy
```

그래서 우리는 다음과 같이 ~~(타입)~~ 캐스팅 연산자를 사용하여 강제적으로 타입을 지정하여 변수에 대입하도록 설정 해주었다.

```java
long d = (long)10.233;Copy
```

상속 관계의 클래스는 크게 부모 클래스(슈퍼 클래스)와 자식 클래스(서브 클래스)로 구분할 수 있다. 기본형 타입을 서로 형변환 할 수 있듯이, 자바의 **상속 관계에 있는 부모와 자식 클래스 간**에는 서로 간의 형변환이 가능하다. 클래스는 reference 타입으로 분류되니 이를 **참조형 캐스팅(업캐스팅 / 다운캐스팅)**이라고 불리운다.

![이미지](https://blog.kakaocdn.net/dn/kOsig/btrLLXRW1cE/V9rilSShuWugrkaiYkbQYK/img.png)

자식 클래스의 객체는 부모 클래스를 상속하고 있기 때문에 부모의 멤버를 모두 가지고 있다. 반면 부모 클래스의 객체는 자식 클래스의 멤버를 모두 가지고 있지는 않는다. (당연한 소리이다)

즉, **참조변수의 형변환은 사용할 수 있는 멤버의 갯수를 조절**하는 것이다. 예를들어 기본형 타입의 형변환 (실수 → 정수) 는 값(3.6 → 3)이 바뀌게 된다 . 그렇지만 객체 형변환 멤버 갯수만 달라지게 된다. 참조 캐스팅은 이러한 클래스의 멤버 구성 관점에서 판별하면 와닿기 쉬울 것이다.

```java
class Parent {
	String name;
    int age;
}

class Child extends Parent {
	/*
    String name;
    int age;
    */
	int number;
}

Parent p = new Parent(); 
Child c = new Child();

Parent p2 = (Parent)c; // 업캐스팅 - 자식에서 부모로
Child c2 = (Child)p2; // 다운캐스팅 - 부모에서 자식으로
```

부모 객체는 자식 객체에 상속을 받고 있으니 더 상위 요소로 판별될 수 있다. 그래서 **Up 캐스팅**이라고 한다. 반대로 하위 요소인 자식 객체로 형변환하는 것은 **Down 캐스팅**이라고 보면 된다.

이러한 참조형 캐스팅의 특징으로는, 대표적으로 ~~ArrayList~~ 자료형을 선언문을 볼 수 있다. 자바 프로그래밍에서 가끔 리스트 자료형을 다음과 같이 선언하는 코드를 본 적이 있을 것이다.

```java
List<int> l = new ArrayList()<>;
```

ArrayList 면 ArrayList 지 ~~List~~로 변수 타입을 선언해도 문제가 없는 이유는 ArrayList가 List를 부모 클래스로서 상속 받기 때문이다. 따지고 보면 위의 코드도 업캐스팅(upcasting) 인 것이다.

한가지 주의해야 할점은, 같은 부모 클래스를 상속받고 있더라도 **형제 클래스 끼리는 아예 타입이 다르기 때문에 참조 형변환 불가능**하다.

Cat 과 Dog 는 서로 참조 캐스팅이 불가능하다

![이미지](https://blog.kakaocdn.net/dn/b5RsAv/btrLOmi5oZe/u6XZRBhKHekFh7pZCp9fw1/img.png)

---

### **업캐스팅(UpCasting)**

- 업캐스팅은 자식 클래스가 부모 클래스 타입으로 캐스팅 되는 것이다.
- 업캐스팅은 캐스팅 연산자 괄호를 생략할 수 있다
- 단, 부모 클래스로 캐스팅 된다는 것은 멤버의 갯수 감소를 의미한다.이는 곧 자식 클래스에서만 있는 속성과 메서드는 실행하지 못한다는 뜻이다.
- 업캐스팅을 하고 메소드를 실행할때, 만일 자식 클래스에서 오버라이딩한 메서드가 있을 경우, 부모 클래스의 메서드가 아닌 오버라이딩 된 메서드가 실행되게 된다.

다음과 같이 부모 클래스 Unit을 상속하는 Zealot 자식 클래스가 있다. Zealot 클래스는 Unit 클래스를 상속하기 때문에 따지고 보면 Unit 클래스가 상위 요소라고 볼 수 있다. (부모는 자식보다 상위니까) 따라서 객체 ~~zealot~~을 객체 ~~unit_up~~에 할당하는 것을 업캐스팅이라 한다.

```java
class Unit {
    public void attack() {
        System.out.println("유닛 공격");
    }
}

class Zealot extends Unit {
    public void attack() {
        System.out.println("찌르기");
    }

    public void teleportation() {
        System.out.println("프로토스 워프");
    }
}

public class Main {
    public static void main(String[] args) {
    
        Unit unit_up;
        Zealot zealot = new Zealot();
        
        // * 업캐스팅(upcasting)
		unit_up = (Unit) zealot;
		unit_up = zealot; // 업캐스팅은 형변환 괄호 생략 가능
    }
}
```

사실 업캐스팅(upcasting)을 이해하는데 있어 미리 객체 지향(oop)의 **참조 다형성**에 대해 미리 알고 있는 분들은 크게 어려움이 없을 것이다. 
결국 한번에 대입하느냐 변수에 나눠 대입하느냐 차이가 있을 뿐이기 때문이다.

```java
Unit unit_zealot = new Zealot(); // 참조 다형성

// ------------------------------------------------

Zealot zealot = new Zealot();
Unit unit_up = zealot; // 변수 업캐스팅(upcasting)
```

### **업캐스팅 멤버 제한**

업캐스팅에는 주의해야 할 점이 있다. 바로 멤버 갯수 감소로 인한 멤버 접근 제한이다.

부모를 상속해서 멤버가 많은 자식 클래스에서 부모 클래스로 업캐스팅 했으니 당연히 멤버 갯수가 감소하게 된다. 그리고 이는 실행할 수 있는 속성과 메서드가 제한된다는 뜻이기도 하다.

위 코드에서 ~~unit_up~~ 레퍼런스 변수에 할당한 데이터 ~~zealot~~ 변수는 Zealot 객체이다. 그런데 업캐스팅 되면서 Unit 타입으로 형변환 되었기 때문에 오로지 부모 클래스에 속한 멤버만 접근이 허용되게 제한되었다.

예를들어 부모 클래스 Unit에 없고 자식 클래스에만 있는 ~~teleportation()~~ 메서드를 실행해보면, 아래 코드에서 볼 수 있듯이 빨간줄이 뜨며 컴파일 에러가 발생하게 된다.

```java
unit_up.teleportation(); //! COMPILE ERROR - 자식 클래스 고유의 메서드는 업캐스팅하면 사용 불가능 (부모에 정의되지 않았으니까)
//? 컴파일단에서 ERROR 처리가 되기 때문에 바로바로 수정이 가능하다
```

![이미지](https://blog.kakaocdn.net/dn/tTNle/btrLQxYNGm6/ciD4PXKbije7H80fVb0dO1/img.png)

이와같이 업캐스팅을 하게되면 부모 클래스 멤버로 멤버 갯수가 한정되었기 때문에 자식 클래스 내에 있는 모든 멤버에 접근할 수 없게 된다. 이는 메서드(method)뿐만 아니라 멤버 필드(field)에도 동일하게 적용된다.

요약하자면 객체를 업캐스팅을 하게 되면 자식과 부모의 공통된 것만 사용할 수 있고 자식클래스에서 새로 만들어진 건 사용 할 수 없다.

### **업캐스팅 오버라이딩 메서드**

이번에는 부모 클래스에도 있는 ~~attack()~~ 메서드를 실행해보자. 그런데 가만 보니 이 ~~attack()~~ 메서드는 자식 클래스에서 오버라이딩(overriding) 하여 재정의 하였다. 이러한 구조에서 업캐스팅한 객체의 attack() 메서드를 실행하면 어느 위치에 있는 클래스으 메서드가 실행 될까?

JAVA

```java
unit_up.attack(); // "찌르기" - 오버라이딩 된 자식 메서드 실행 (왜냐하면 변수에 들어가있는 실제 객체는 Zealot() 이니까)
```

!https://blog.kakaocdn.net/dn/biTMyQ/btrLPnPELTW/wavBmDj8yTaZHsR3GZ7LvK/img.png

업캐스팅 되었기 때문에 부모 클래스에 정의된 메서드를 사용할 것 같았지만 오버라이딩 된 자식 클래스의 메서드를 사용하는 것을 볼 수 있다. 이는 오버라이딩 특성상 코드가 실행하는 런타임 환경에서 동적으로 바인딩 되었기 때문이다.

정리하자면 업캐스팅을 다루는데 있어 조심해야 할점은 크게 두가지로 요약할 수 있게 된다.

- 업캐스팅 하면 멤버 갯수가 제한되어 자식 클래스에만 있는 멤버는 사용할 수 없게 된다
- 업캐스팅 했지만 오버라이딩 된 메서드는 자식 클래스의 메서드로 실행이 된다

### **업캐스팅 하는 이유**

이처럼 업캐스팅 하는 방법과 특징과 주의점은 알겠지만 **정작 왜 하는지는 모호할 것이다.**

결론부터 말하자면, 업캐스팅을 사용하는 이유는 공통적으로 할 수 있는 부분을 만들어 간단하게 다루기 위해서이다. 상속 관계에서 상속 받은 서브 클래스가 몇 개이든 하나의 인스턴스로 묶어서 관리할 수 있기 때문이다.

예를들어 다음과 같이 부모 클래스 Shape에 각각 자식 클래스 Rectangle, Triangle, Circle가 상속 관계를 맺었다고 하자.

![이미지](https://blog.kakaocdn.net/dn/n33PN/btrLLiPDFbh/LBkmodysAEnimkOLIU4yK1/img.png)

본래라면 Rectangle, Triangle, Circle 클래스는 서로 다른 타입이니 각각 타입을 정의해서 사용해야 한다.

```java
Rectangle[] r = new Rectangle[];
r[0] = new Rectangle();
r[1] = new Rectangle();

Triangle[] t = new Triangle[];
t[0] = new Triangle();
t[1] = new Triangle();

Circle[] c = new Circle[];
c[0] = new Circle();
c[1] = new Circle();
```

하지만 상속 관계를 맺어 부모 클래스로 업캐스팅이 가능하다면, 다음과 같이 하나의 타입으로 묶어 배열을 구성할 수 있게 된다.

```java
Shape[] s = new Shape[];
s[0] = new Rectangle();
s[1] = new Rectangle();
s[2] = new Triangle();
s[3] = new Triangle();
s[4] = new Circle();
s[5] = new Circle();
```

하나의 자료형으로 관리하니 코드량도 훨씬 줄어들고 가독성도 좋아지며 유지보수성도 좋아짐을 알 수 있다. 그런데 위에서 언급했던 것처럼 자식 클래스에만 있는 고유한 메서드를 실행하려면 어떻게 해야 할까?

오버라이딩 한 메서드가 아닌 이상 업캐스팅한 부모 클래스 타입에서 자식 클래스의 고유 메소드를 실행할 수 없다. 따라서 업캐스팅한 객체를 다시 자식 클래스 타입으로 되돌리는 다운 캐스팅(down casting)이 필요한 것이다.

---

### **다운 캐스팅(DownCasting)**

- 다운캐스팅은 거꾸로 부모 클래스가 자식 클래스 타입으로 캐스팅 되는 것이다.
- 다운캐스팅은 캐스팅 연산자 괄호를 생략할 수 없다
- 다운캐스팅의 목적은 업캐스팅한 객체를 다시 자식 클래스 타입의 객체로 되돌리는데 목적을 둔다. (복구)

다운 캐스팅은 부모 클래스를 자식클래스로 캐스팅하는 단순히 업캐스팅의 반대 개념이 아니다.

다운 캐스팅의 진정한 의미는 부모 클래스로 업 캐스팅된 자식 클래스를 복구하여, 본인의 필드와 기능을 회복하기 위해 있는 것이다. 즉, 원래 있던 기능을 회복하기 위해 다운캐스팅을 하는 것이다.

```java
class Unit {
    public void attack() {
        System.out.println("유닛 공격");
    }
}

class Zealot extends Unit {
    public void attack() {
        System.out.println("찌르기");
    }

    public void teleportation() {
        System.out.println("프로토스 워프");
    }
}

public class Main {
    public static void main(String[] args) {

        Unit unit_up;
        Zealot zealot = new Zealot();

        unit_up = zealot; // 업캐스팅
        
        // * 다운캐스팅(downcasting) - 자식 전용 멤버를 이용하기위해, 이미 업캐스팅한 객체를 되돌릴때 사용
        Zealot unit_down = (Zealot) unit_up; // 캐스팅 연산자는 생략 불가능. 반드시 기재
        unit_down.attack(); // "찌르기"
        unit_down.teleportation(); // "프로토스 워프"
    }
}
```

업캐스팅 된 객체 ~~unit_up~~ 에서 만일 자식 클래스에만 있는 ~~teleportation()~~ 메서드를 실행해야 하는 상황이 온다면, 다운 캐스팅을 통해 자식 클래스 타입으로 회귀 시킨뒤 메서드를 실행하면 된다. 만일 메서드를 한번 만 실행 할 것이라 따로 변수에 저장해둘 필요성이 없다면, 아래와 같이 다운 캐스팅을 한줄로 표현할 수도 있다.

```java
((Zealot) unit_up).teleportation(); // "프로토스 워프"
```

이때 캐스팅 연산자를 업캐스팅과는 달리 생략할 수 없는데, 나름의 이유가 있기 때문이다. 다운캐스팅은 곧 사용할 수 있는 객체 멤버 증가를 의미하는데, 멤버의 증가는 불안전 하다. 왜냐하면 실제 참조변수가 가리키는 객체가 무엇인지 모르기 때문에 어떠한 멤버가 추가 되는지 알수가 없다. 그래서 반드시 형변환 괄호를 기재함으로써 증가된 클래스의 멤버가 무엇인지 알게 하도록 개발자한테 알려줘야 하기 때문이다.

### **다운 캐스팅 주의점**

앞서 다운 캐스팅의 목적은 **업캐스팅한 객체를 되돌리는데** 있다고 했다. 그래서 다음과 같이 업캐스팅 되지 않는 생 부모 객체 ~~unit~~ 일 경우, 이를 그대로 ~~(Zealot) unit~~ 다운캐스팅 하면 오류(ClassCastException)가 발생하게 된다.

```java
Unit unit = new Unit();

// * 다운캐스팅(downcasting) 예외 - 다운캐스팅은 업스캐팅한 객체를 되돌릴때 적용 되는것이지, 오리지날 부모 객체를 자식 객체로 강제 형변환은 불가능
Zealot unit_down2 = (Zealot) unit; //! RUNTIME ERROR - Unit cannot be cast to Zealot
unit_down2.attack(); //! RUNTIME ERROR
unit_down2.teleportation(); //! RUNTIME ERROR
```

![이미지](https://blog.kakaocdn.net/dn/ANpka/btrLOmKdaiy/0HTkcORYnlFW8J6uOJK4D0/img.png)

이러한 다운 캐스팅 특성은 원래 참조 다형성에서도 불가능 했기 때문에 발생하는 것이다.

```java
Zealot unit_down = new Unit(); // 참조 다형성 위배
```

위와 같은 다운 캐스팅 특성에 대해 주의해야 할 이유는 에디터에서 컴파일 에러가 발생하기 않고 런타임 에러가 발생하는 위험성이 있기 때문이다.

예를들어 기본형 캐스팅은 값의 손실만 있을 뿐 프로그램이 작동하는데는 문제없다. (3.16 → 3)

하지만 다운 캐스팅은 에디터에서는 빨간줄이 없는데 코드를 실행 도중에 갑자기 에러가 터져 프로그램이 죽어버릴 수 있다.

![이미지](https://blog.kakaocdn.net/dn/b3JWPa/btrLVYIatzK/vpQjqflnFq9FKNCgvfHRqK/img.png)

추가로 위에서 잠깐 소개한 적이 있는데, 아무리 같은 부모 클래스를 상속하고 있더라도 형제 클래스 끼리는 서로 캐스팅이 불가능하다는 것이다. 이는 잘못 판단하면 컴파일 에러와 런타임 에러 둘다 생길 수 있는 가능성이 있으니 매우 조심해야 한다.

```java
class Unit {
    public void attack() {
        System.out.println("유닛 공격");
    }
}

class Zealot extends Unit {
    public void attack() {
        System.out.println("찌르기");
    }

    public void teleportation() {
        System.out.println("프로토스 워프");
    }
}

class Marine extends Unit {
    public void attack() {
        System.out.println("총쏘기");
    }

    public void stimpack() {
        System.out.println("스팀 팩");
    }
}

public class Main {
    public static void main(String[] args) {

        Unit unit = new Unit();
        Zealot zealot = new Zealot();

        // * 다운캐스팅(downcasting) 예외 - 같은 상속 자식 클래스라도 구성이 같아도 타입이 다르니 불가능
        Marine marine = new Marine(); // 마린 클래스
        
        Unit unit_m = marine; // 업캐스팅
        
        Zealot zealot_marine = (Zealot) unit_m; // 다른 자식클래스 질럿으로 다운캐스팅
        zealot_marine.attack(); //! RUNTIME ERRPR - Marine cannot be cast to Zealot
        zealot_marine.stimpack(); //! COMPILE ERRPR - Zealot 클래스에 없는 메소드이니 에러
    }
}
```

이 처럼 무분별한 다운캐스팅은 컴파일 시점에는 오류가 발생하지 않아도 런타임 오류를 발생시킬 가능성이 있다. 따라서 다운 캐스팅을 다룰때에는 다운 캐스팅 할 객체가 오리지날 부모 객체인지, 업캐스팅된 부모 객체인지 항상 머릿속에서 가능한지 생각해 볼 필요성이 있다.

다행인 점은 이렇게 혼동되는 객체를 구별하기 위해 도움을 주는 **연산자**를 자바에서 지원해준다.

---

<br>    
<br>    


## **instanceof 연산자**

참조 캐스팅을 잘못했다가 런타임 환경에서 에러가 나 프로그램이 종료 되버리면 서비스에 크나큰 차질이 생기게 된다.

따라서 코드 디버깅을 많이 하여 미리 예방하는 것이 베스트이지만, 이마저도 부족하면 직접 업캐스팅 / 다운캐스팅 유무를 확인하여 참조 캐스팅 동작을 결정하면 된다.

이때 사용되는 것이 ~~instanceof~~ 연산자인데, 이 연산자는 어느 객체 변수가 어느 클래스 타입인지 판별해 true/false를 반환해준다. 사용시 주의할 점은 ~~instanceof~~ 연산자는 객체에 대한 클래스(참조형) 타입에만 사용할 수 있다는 점이다. (int, double 같은 primitive 타입에는 사용 불가능)