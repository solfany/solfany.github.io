---
title: "[Java] final 이란?"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)

## final의 정의

- 자바 언어에서 final은 오직 한 번만 할당할 수 있는 entity를 정의할 때 사용 된다.
- final로 선언된 변수가 할당되면 항상 같은 값을 가진다.
- 만약 final 변수가 객체를 참조하고 있다면,
  그 객체의 사이가 바뀌어도 final 변수는 매번 동일한 내용을 참조한다.
- final 클래스에서 사용하게 되면 그 클래스는 최종 상태가 되어, 더 이상 상속이 불가능하다.
- 보안이나 효율성 측면에서 장점이 있다.

> final 클래스여도 필드는 setter 함수를 통해 변경은 가능하다.
>
> 어떤 클래스여도 필드는 setter 함수를 통해 변경은 가능하다.

어떤 클래스를 상속하는데 그 안에 final 메서드가 있다면 오버라이딩으로 수정할 수 없다.

즉) 메서드에 final을 사용하게 되면 상속받은 클래스에서 부모의 final 메서드를 재 정의 할 수 없다.

final을 가장 많이 사용하는 곳은 필드(전역변수)이다.

final을 필드에 사용하면 **해당 필드는 더 이상 수정이 불가능**하다는 의미를 갖는다.

## 용도

1. 클래스: 상속을 금지한다.
2. 멤버 매서드 : 오버라이딩을 금지한다.
3. 멤버 변수 : 값 변경을 금지한다.

## **final 사용법**

### **final 필드**

```
final int number = 1; //final 타입 필드 [= 초기값];

```

final 필드는 위와 같이 선언하며 final 필드의 초기값을 줄 수 있는 방법은 딱 두가지 방법밖에 없다.
첫번째는 필드 선언시에 주는 방법이 있고, 두번째는 생성자를 통해서 주는 방법이 있다.
단순 값이라면 필드 선언시에 주는 것이 가장 간단하지만 복잡한 초기화 코드가 필요하거나 객체 생성 시에 외부 데이터로 초기화를 시켜야한다면 생성자를 통해서 초기값을 부여하는 방법을 써야 한다.
생성자는 final 필드의 최종 초기화를 마쳐야 하는데 만약 초기화가 되지 않은 final 필드가 있다면 컴파일 에러가 발생한다.

### **final 객체**

```arduino
class Company{
    String name = "회사명";

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

public class Final_ex {
    public static void main(String[] args) {
    	final Company company = new Company();
    	//company = new Company(); //객체를 한번 생성했다면 재생성 불가능
    	company.setName("ex회사"); //클래스의 필드는 변경가능
    }
}

```

객체 변수에 final로 선언하면 그 변수에 다른 참조 값을 지정할 수 없다.
즉 한번 생성된 final 객체는 같은 타입으로 재생성이 불가능하다.
객체자체는 변경이 불가능하지만 객체 내부 변수는 변경 가능하다.

### **final 클래스**

```scala
//final 클래스
final class Company{
    String name = "회사명";
}

//상속 불가능
class A_Company extends Company{

}

```

클래스에 final을 사용하게되면 그 클래스는 최종상태가 되어 더이상 상속이 불가능다.
final 클래스여도 필드는 Setter함수를 통하여 변경은 가능하다.

### **final 메서드**

```scala
class Company{

    String name = "회사명";

    public final void print() {
        System.out.println("회사 이름은 :"+name+" 입니다.");
    }
}

class A_Company extends Company{

    String name = "a회사";

    //메서드 오버라이드 불가능
    public void print() {

    }
}

```

메서드에 final을 사용하게되면 상속받은 클래스에서 부모의 final 메서드를 재정의 할 수 없다.
자신이 만든 메서드를 변경할 수 없게끔 하고싶을때 사용되며 시스템의 코어부분에서 변경을 원치 않는 메서드에 많이 구현되어 있다.

### **메서드의 인자값에 final을 사용하는 경우**

```arduino
class Company{
    String name = "회사명";

    public void setName(final String name) {
    	//name = "ex회사2"; //인자값으로 받은 final변수는 변경 불가능
        this.name = name;
    }
}

public class Final_ex {
    public static void main(String[] args) {
    	final Company company = new Company();
    	company.setName("ex회사");
    }
}

```

잘 사용하지는 않지만 코딩을 좀 더 명확하게 하고 싶은 경우 메서드의 인자값에 final을 사용하시는 분들이 종종 있다고 한다. 
final 필드와 마찬가지로 인자값에 final을 사용하는 경우 final 인자값의 변경이 불가능다.

<br>

<br>

## 예제

```bash
package ch06;

import java.util.Scanner;

public class Ex01 {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);

//		System.out.printf("목표액 입력 :");
//		int  aim = scanner.nextInt();


//		바뀌지 않을 값이기에 final
		final  int aim = 1000;
		System.out.printf("목표액 : %d\n", aim );
		System.out.printf("실적 입력: ");
//		result 입력값을 받는다
		int result = sc.nextInt();
//		정수형 bonus선언
		int bonus;


//		만약에 실적에 aim값보다 크면 밑에 문장 실행
		if (result >= aim) {
//			보너스 값을 10으로 나눠서 출력
			bonus =(result - aim) / 10;
			System.out.printf("보너스 : %d", bonus);
//		실적이 aim 보다 작으면 아래 문장 실행
		}else
			System.out.println("달성 실패 ");

//		scanner함수를 닫아주는게 원칙
		sc.close();

	}

}
```
