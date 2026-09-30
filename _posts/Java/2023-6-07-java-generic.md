---
title: "[Java] 제네릭(Generic)"
categories:
  - Java
tags: [Java]
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)

## 제네릭(Generic)이란?

자바에서 “제네릭” 은 다양한 타입의 객체를 다루는 메서드나 컬렉션 클래스에 컴파일 시 타입 체크를 해주는 기능이다.
제네릭을 사용하면, 클래스나 메서드 내부에서 사용할 데이터 타입을 외부에서 지정 할 수 있게 되어 코드의 재사용성을 높이고 타입 안정성을 확보한다.

```java
List<String> list = new ArrayList<String<();
```

List 변수에는 String 객체만 추가 할 수 있으며, 다른 타입의 객체를 추가하려고 하면 컴파일 오류가 발생한다.

제네릭을 사용하면 프로그램의 타입 안정성을 보장 하게 된다.

![img](https://blog.kakaocdn.net/dn/b61TxD/btrFKavUCz5/4Rr4z8CUU5ycitPC7tmmuk/img.png)

ArrayList 내부

자바에서 ArrayList<Integer>와 같이 <> 꺽쇠 안에 클래스 타입이 명시되어있는 것을 확인할 수 있다.
위의 사진은 ArrayList의 내부이다. ArrayList<E>처럼 'E'라고 표시된 것을 확인할 수 있다.

```java
ArrayList<Integer> list = new ArrayList<Integer>();
ArrayList<String> list2 = new ArrayList<String>();
```

위와 같이 ArrayList에 저장할 타입을 Integer, String 등으로 지정할 수 있다.

이처럼 데이터의 타입을 일반화(Generalize)하는 것을 제네릭(Generic)이라고 할 수 있다. 이러한 제네릭은 클래스나 메서드에서 사용할 내부 데이터 타입을 컴파일 시에 미리 지정할 수 있다. 따라서 컴파일 시에 미리 타입 검사(Type Check)를 수행할 수 있다.

이러한 타입 검사를 컴파일 시에 수행하면 다음과 같은 장점을 얻을 수 있다.

1. 클래스나 메서드 내부에서 사용되는 객체의 타입 안정성을 높일 수 있다.

2. 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있다.

3. 타입에 대해 유연성과 안정성을 확보한다.

4. 런타임 환경에 영향을 주지 않는 전처리 기술이다.

JDK 1.5 이전에서는 여러 타입을 사용하는 대부분의 클래스나 메서드에서 인수나 반환 값으로 Object 타입을 사용했다.

```java
List v = new ArrayList();
v.add("test");// A String that cannot be cast to an Integer
Integer i = (Integer)v.get(0);// Run time error
```

위와 같은 코드는 런 타임 에러를 발생시킨다. List에 String을 저장해놓고 Integer로 타입 변환하는 오류가 런타임에 잡히는 것이다.

```java
List<String> v = new ArrayList<String>();
v.add("test");
Integer i = (Integer)v.get(0);// (type error)  compilation-time error
```

하지만 위와 같이 제네릭을 이용하면 컴파일 에러를 발생시켜 컴파일 시에 오류를 잡아낼 수 있다. 런 타임 에러보다 컴파일 에러가 훨씬 디버깅이 쉽기 때문에 이점이 많다.

또한, Object 객체를 이용하면 다시 원하는 타입으로 타입 변환을 해야 하기 때문에 이에 따른 성능 저하, 오류 발생 가능성 등이 존재한다. 따라서 제네릭을 사용하면 컴파일 시에 타입이 정해 지므로, 타입 검사나 타입 변환과 같은 작업을 생략할 수 있게 된다.

```java
class Sample<T>{

// 데이터 타입 Tprivate T data;

// 파라미터로 T를 받는다public void setData(T data){
    	this.data = data;
    }

// return 타입 : Tpublic T getData(){
    	return data;
    }

}
```

제네릭을 이용하여 위와 같이 제네릭 클래스와 메서드를 선언할 수 있다. 'T'를 타입 변수라고 하며, 임의의 참조형 타입을 의미한다. 'T'는 예시일 뿐 다른 문자를 사용할 수도 있다.

위와 같이 선언된 제네릭 클래스를 생성할 때는 타입 변수 자리에 사용할 실제 타입을 명시하면 된다.

```java
Sample<Integer> sample = new Sample<Integer>();

sample.setData(2);

Integer ret = sample.getData();
```

이렇게 타입 변수를 지정하면, 'T' 자리에 Integer가 들어간다고 생각하면 이해하기 편하다.

## 제네릭 사용 이유?
> 타입을 유연하게 처리하며, 잘못된 타입 사용으로 발생할 수 있는 런타임 타입 에러를 컴파일 과정에 검출한다.

자바 컴파일러는 코드에서 잘못 사용된 타입 때문에 발생하는 문제점을 제거하기 위해 제네릭 코드에 대해 강한 타입 체크를 한다.\
**실행 시 타입 에러가 나는것보다는 컴파일 시에 미리 타입을 강하게 체크해서 에러를 사전에 방지**하는 것이 좋다.
또한 제네릭 코드를 사용하면 타입을 국한하기 때문에 요소를 찾아올 때 타입 변환을 할 필요가 없어 프로그램 성능이 향상되는 효과를 얻을 수 있다.

1. 타입의 안정성, 코드의 간결화
     구체적인 데이터 타입을 인스턴스에 따라 지정 가능 중복 제거와 타입의 안정성을 동시에 추구할 수 있다.
2. 복수의 제네릭
     class Person<T,S>
3. 기본 데이터 타입과 제네릭
     참조 데이터 타입에서만 사용할 수 있다. (wrapper) 클래스를 사용해야한다.
4. 제네릭의 생략
     매개변수의 데이터 타입을 알고 있으면 생략해도 된다.
5. 메서드에 적용
     클래스 뿐만 아니라 메서드에서도 쓸 수 있다.
6. 제네릭의 제한 (extends)
     class Persin<T extends Info> {}

## 제네릭 사용법
- **클래스, 인터페이스 또는 메서드에 선언**할 수 있다.
- **동시에 여러 타입을 선언**할 수 있다.
- **와일드 카드를 이용하여 타입에 대하여 유연한 처리**를 가능하게 한다.
- 제네릭 선언 및 정의시에 타입의 상속 관계를 지정할 수 있다.

제네릭 타입은 타입을 파라미터로 가지는 클래스와 인터페이스를 말한다.

제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 < > 부호가 붙고 사이에 타입 파라미터가 위치한다.

```java
public class MyClass<T>
public interface MyInterface<T>
```

타입 파라미터는 **정해진 규칙은 없지만 일반적으로 대문자 알파벳 한 글자로 표현 한**다.

**자주 사용하는 타입인자**

| 타입인자 | 설명    |
| -------- | ------- |
| `<T>` | Type    |
| `<E>` | Element |
| `<K>` | Key     |
| `<N>` | Number  |
| `<V>` | Value   |
| `<R>` | Result  |

## 제네릭 클래스

```java
class ExClassGeneric<T> {
    private T t;

    public void setT(T t) {
        this.t = t;
    }

    public T getT() {
        return t;
    }
}
```

위와 같이 클래스를 설계할 때 구체적인 타입을 명시하지 않고 타입 파라미터로 넣어두었다가 실제 설계한 클래스가 사용되어 질 때

```java
ExClassGeneric exGeneric = new ExClassGeneric<>(); 
```

이런식으로 구체적인 타입을 지정하면서 사용하면 타입 변환을 최소화 시킬 수 있다.

## 제네릭 인터페이스

```java
interface ExInterfaceGeneric<T> {
    T example();
}

class ExGeneric implements ExInterfaceGeneric<String> {

    @Override
    public String example() {
        return null;
    }
}
```

인터페이스도 위와 같이 클래스처럼 제네릭으로 설정해두고 활용할 수 있다.

## 멀티 타입 파라미터 사용

```java
class ExMultiTypeGeneric<K, V> implements Map.Entry<K,V>{

    private K key;
    private V value;

    @Override
    public K getKey() {
        return this.key;
    }

    @Override
    public V getValue() {
        return this.value;
    }

    @Override
    public V setValue(V value) {
        this.value = value;
        return value;
    }
}
```

타입은 두개 이상의 멀티 타입 파라미터를 사용할 수 있고 이 경우 각 타입 파라미터를 콤마로 구분한다.

## 제네릭 메서드

```java
class People<T,M>{
    private T name;
    private M age;

    People(T name, M age){
        this.name = name;
        this.age = age;
    }

    public T getName() {
        return name;
    }
    public void setName(T name) {
        this.name = name;
    }
    public M getAge() {
        return age;
    }
    public void setAge(M age) {
        this.age = age;
    }

//Generic Mothodpublic static<T,V> boolean compare(People<T,V>p1, People<T,V>p2) {
        boolean nameCompare = p1.getName().equals(p2.getName());
        boolean ageCompare =p1.getAge().equals(p2.getAge());
        return nameCompare && ageCompare;
    }
}

public class ExGeneric {
    public static void main(String []args){
//타입 파라미터 지정
        People<String,Integer> p1 = new People<String,Integer>("Jack",20);
//타입 파라미터 추정
        People<String,Integer> p2 = new People("Steve",30);
//GenericMothod 호출boolean result = p1.compare(p1,p2);
        System.out.println(result);
    }
}
```

제네릭 메서드를 정의할때는 리턴타입이 무엇인지와는 상관없이 내가 제네릭 메서드라는 것을 컴파일러에게 알려줘야한다.
그러기 위해서 리턴타입을 정의하기 전에 제네릭 타입에 대한 정의를 반드시 명시해야한다.

그리고 중요한 점이 제네릭 클래스가 아닌 일반 클래스
내부에도 제네릭 메서드를 정의할 수 있 다.
👇🏻
그 말은, 클래스에 지정된 타입 파라미터와 제네릭 메서드에 정의된
타입 파라미터는 상관이 없다는 것이다.

> 즉, 제네릭 클래스에 를 사용하고, 같은 클래스의 제네릭 메서드에도  같은 이름을 가진 타입파라미터를 사용하더라도 둘은 전혀 상관이 없다.

## 제네릭 와일드카드

```php
public class Calc {
    public void printList(List<?> list) {
       for (Object obj : list) {
    	   System.out.println(obj + " ");
       }
    }

    public int sum(List<? extends Number> list) {
      int sum = 0;
      for (Number i : list) {
    	  sum += i.doubleValue();
      }
      return sum;
    }

   public List<? super Integer> addList(List<? super Integer> list) {
      for (int i = 1; i < 5; i++) {
    	 list.add(i);
      }
      return list;
    }
}
```

와일드카드 타입에는 총 세가지의 형태가 있으며 물음표(?)라는 키워드로 표현한다.

- 제네릭타입<?> : 타입 파라미터를 대치하는 것으로 모든 클래스나 인터페이스타입이 올 수 있다.
- 제네릭타입<? extends 상위타입> : 와일드카드의 범위를 특정 객체의 하위 클래스만 올 수 있다.
- 제네릭타입<? super 하위타입> : 와일드카드의 범위를 특정 객체의 상위 클래스만 올 수 있다.

---

## 예제

```java
package ch10;

interface MyFunction<T>{
//	인수에서 전달하는 변수 타입에 따라 String이 될 수도 있고 Integer가 될 수도 있다.
//	이런 대문자 변수들을 랩처 클래스라고 하며
//	랩퍼 클래스 변수는 자체로 클래스가 다. (이미 정의 되어있기 때문에 별도의 선언은 불필)
	void print(T x);
}

public class EX_11 {
	public static void main(String[] args) {
//여기서 변수 타입은 String
// toString 매소드를 통해 객체에 저장된 값을 출력할 수 있다.

		MyFunction<String> f1 = (x) -> System.out.println(x.toString());
		f1.print("ABC");

//		여기서 Integer 로 서로 다르지만 변수 타입을 제네릭 변수로 받기 때문에 문제없다.
//		toString 매소드는 문자열만 출력 가능하기 때문에
//		Integer 변수의 경우 별도의 작업을 거쳐야 출력이 가능하다.
//		랩퍼 객체로 변환은 parseInt()를 활용한다.(UnBoxing)
		MyFunction<Integer>f2 = (x) -> System.out.println(x.toString());
		f2.print(Integer.valueOf(100));

	}
}
```

> 제네릭은 타입인가요?
> 제네릭은 자바에서 데이터 타입을 파라미터화(parameterize) 할 수 있는 방법을 제공하는 프로그래밍 기법이다.
> 그 자체로 타입은 아니지만, 클래스나 인터페이스, 메서드로 정의할 때 사용하는 매개변수를 가리킨다.
