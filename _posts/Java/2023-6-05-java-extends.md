---
title: "[Java] 상속 extends, implements"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/3..png?raw=true)



# 상속이란 (Inheritance)

## OOP의 특징

1. 상속과 인터페이스 (계층성)

2. 다형성, 사용편의성 (모듈화)

3. 캡슐화, 정보은닉

4. 자료 추상화 (모델링)

5. 동적 바인딩 

상속을 설명할때 가장 쉽게 이해하려면 아래의 그림을 보면 좀 쉽게 다가 올 거다.

![이미지](https://velog.velcdn.com/post-images%2Fhkoo9329%2F63b7a830-1e57-11ea-8869-af114ab79736%2Fimage.png)

- 상자 하나하나는 모두 객체 (Object)이고, 자바 용어로는 class이다.
- 이러한 계층을 표현하기 위해 만들어진 것이 바로 상속이다.
- 하위 객체는 상위 객체 (부모)의 특징을 물려받는다.
    
    > 예를 들어 동물의 특징 '움직이다'를 포유류, 조류, 파충류는 그대로 물려받는다.
    > 
    > 
    > 즉. move()라는 메소드를 포유류,.조류, 파충류 객체가 모두 사용할 수 있다는 뜻이다.
    > 
- 또 다른 예로 변수 또한 객체에 선언되어 있다면 물려받게 된다.
    
    > 나이 (age) 변수가 동물 객체에 선언되어 있다면 물려받게 된다.
    > 

이 메소드 OR 변수를 '구현'하는가 그대로 '사용'하는가에 따라서 상속의 형태가 갈리게 된다.


1. extends
    - 부모에서 선언 / 정의를 모두하며 자식은 메소드 / 변수를 그대로 사용할 수 있음
2. implements (interface 구현)
    - 부모 객체는 선언만 하며 정의(내용)은 자식에서 오버라이딩 (재정의) 해서 사용해야함
3. abstract
    - extends와 interface 혼합. extends하되 몇 개는 추상 메소드로 구현되어 있음

<br>
<br>


# extends (상속)

- 사실 extends가 상속의 대표적인 형태다.
- 부모의 메소드를 그대로 사용할 수 있으며 오버라이딩 할 필요 없이 부모에 구현되있는 것을 직접 사용 가능하다.

```java
class Vehicle {
  protected int speed = 3;

  public int getSpeed(){
    return speed;
  }
  public void setSpeed(int speed){
    this.speed = speed;
  }
}

class Car extends Vehicle{
  public void printspd(){
    System.out.println(speed);
  }
}

public class ExtendsSample {
  public static main (String[] args){
    Car A = new Car();
    System.out.println(A.getSpeed());
    A.printspd();
  }
}
```

Car라는 클래스는 Vehicle을 상속 받았다. 그리고 getSpeed() 메소드로 speed를 print 했다.

그런데 vehicle의 getSpeed 메소드에서 speed를 직접 바로 사용했다. extends를 했으니 메소드 뿐만 아니라 변수까지 사용이 가능해 지는 것이다.

여기서 접근 제어자에 대해 다시 설명하지면.....

| public | protected | default | private |
| --- | --- | --- | --- |
| All | 상속 OR 동일패키지 | 상속 && 동일패키지 | 클래스 내부 |

그리고 하나 더 짚고 가자면....

**자바는 "다중상속"을 지원하지 않는다**는 점이다.

다중상속이란 부모클래스가 두개 이상 존재할 수 있다는 것인데, 자바에서는 이를 지원하지 않는다. 즉 , `public class Son extends Father, Mother{...}` 이것이 지원하되지 않는다는 것이다.

자바는 다중상속을 지원하지 않는다. 대신 implements(인터페이스)가 등장했다.

Interface 의 경우 다른 글에서 더 자세히 다뤄보겠다. 
지금은 간략히 설명만 하겠다. 


<br>
<br>

# implements (상속)

```java
interface TestInterface{
  public static int num = 8;
  public void fun1();
  public void fun2();
}

class InterfaceExam implements TestInterface{
  @Override
  public void fun1(){
    System.out.println(num);
  }

  @Override
  public void fun2() {

  }
}

public class InterfaceSample{
  public static void main(String args[]){
    InterfaceExam exam = new InterfaceExam();
    exam.fun1();
  }
}
```

**implements의 가장 큰 특징은 이렇게 부모의 메소드를 반드시 오버라이딩(재정의)해야 한다.**

또한 이 implements는 다중상속을 대신해준다.

```
public class Son implements Father, Mother{...}
```

이러한 형태로 말이다.

근데 "이러한 구현은 메소드를 어차피 재정의해야되니 '상속'의 의미가 아니지 않냐?" 이런 의문이 들 수 있다. ~~내가 그랬습니다...~~

이걸 진정한 상속이라고 생각하지는 않습니다만 자바가 그렇다는데 어쩌겠습니까....

단, 어느정도 이해하시는데 도움을 주자면, 
Java와 C#의 인터페이스 상속은 계약 및 분류의 의미가 강하다."


## 간단 정리

1. extends는 일반 클래스와 abstract 클래스 상속에 사용되고, implement는 interface 상속에 사용된다.
2. class가 class를 상속받을 땐 extends를 사용하고, interface가 interface를 상속 받을 땐 extends를 사용한다.
3. class가 interface를 사용할 땐 implements를 써야하고
4. interface가 class를 사용할 땐 implements를 쓸수 없다.
5. extends는 클래스 한 개만 상속 받을 수 있다.
6. extends 자신 클래스는 부모 클래스의 기능을 사용한다.
7. implements는 여러개 사용 가능하다.
8. implements는 설계 목적으로 구현 가능하다.
9. implements한 클래스는 implements의 내용을 다 사용해야 한다.
10. 

---

extends는 클래스를 확장하는 거고 implements는 인터페이스를 구현하는 것이다.

인터페이스와 보통 클래스의 차이는 인터페이스는 정의한 메소드를 구현하지 않아도 된다.

인터페이스를 상속받는 클래스에서 인터페이스에 정의된 메소드를 구현하면 된다.