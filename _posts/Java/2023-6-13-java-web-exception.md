---
title: "[Java] exception 처리하기"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)


## **exception 처리하기 - 이론편**
<aside style="background-color: #d4e4e9; font-size: 0.4rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
코딩을 하다보면 꼼꼼함의 중요성을 간과할 때가 많다. <br>
새로운 기능, 새로운 기술은 정말 재미있고 시간가는 줄 모르고 할 때가 많다. <br>
하지만 이러한 새로운 것들을 실제로 시스템에 적용하기 위해서는 기본이 탄탄해야 한다. 해야함을 알면서도 프로그래밍을 하다보면 까먹게 되는 게 있다. <br>
재미가 없더라도 반드시 해야하는 것이 2가지 있다. 바로 validation과 exception 처리이다. 반드시 이 2개는 코딩을 하면서 습관으로 가지시는걸 추천 한다. 

</aside>

오늘은 exception에 대해서 알아보도록 하겠다.

### exception

exception은 **로직이 실행되는 중(Runtime)에 원하지 않는 이벤트가 발생하거나 예상하지 않은 이벤트가 일어났을때의 처리**를 말한다.

exception은 우리가 일반적으로 생각할 수 있는 **시스템에서 발생하는 error와는 다르다는 사실**을 알아야 한다.
**error**는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류로 **개발자가 미리 예측해서 처리할 수 없다.** 하지만 **exception**은 **충분히 예상할 수 있는 범위** 내에 있으며 예외를 구분하고 이에 따른 처리 방법을 명확히 적용하는것이 중요하다.

### exception의 종류

exception 역시 class의 종류 중 하나이다.

모든 Exception과 Error 클래스는 Throwable 클래스를 상속받고 있으며, Throwable은 최상위 클래스 Object를 상속받고 있다. 
계층적 구조를 보면 아래 이미지가 나옵니다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/3a222528-c23c-41eb-8e18-b6ca1d181770)


Exception의 계층 구조

Throwable을 상속받고 있는 **Error는 시스템 레벨의 심각한 수준의 에러**를 말한다. 그리고 **Exception은 개발자가 예상할 수 있으며 처리할 수 있는 수준의 에러**이다.  

그리고 Exception을 바로 상속받는 IOException과 같은 checked-exception이 존재하며 RuntimeException이 Exception을 상속받고 있다. 
그리고 RuntimeException을 상속받는 NullpointException과 같은 unchcked-exception이 존재한다.

그렇다면 checked-exception과 unchecked-exception은 어떤 차이가 있을까?🤔


### checked-exception과 unchecked-exception

**java의 exception에는 2가지 종류의 exception이 존재한다. checked와 unchecked입니다.**

1. checked : **checked exception은 컴파일 타임에 exception 처리를 하는지 체크되어지는 exception**이다. 
그래서 반드시 exception 처리가 필요로 한다. 
예를 들어 해당 exception에는 FileNotFoundException 또는 IOException 등이 있다. 
만약 `new FileRader("<filename>")`으로 파일을 연 후 `fileInput.readLine()`로 파일을 읽는다면 IOException 처리를 해주지 않으면 컴파일이 이루어 지지 않습니다.

<br>

2. unchecked : **unchecked exception은 컴파일 타임에 체크되어지지 않는 exception**이다. 
따라서 exception 처리가 되어있지 않더라도 컴파일타임에 정상처리되어 실행되어지게 된다. 따라서 exception 처리가 강제되어지지는 않는다.

<br>

<aside style="background-color: #d4e4e9; font-size: 0.4rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
Error와 RuntimeException를 상속 받은 exception은 unchecked exception이며 나머지는 모두 checked exception이다. 
</aside>

<br>

추가로 우리가 직접 exception을 만든다면 어떤 상황에서 checked와 un-checked exception을 쓰면 좋을까?

[oracle docs](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)를 참고하면 아래와 같은 문구가 있다.

> If a client can reasonably be expected to recover from an exception, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception.
> 

즉, 만약 클라이언트가 exception이 발생했을때 적절히 회복할 수 있을 것 같은 exception에 대해서는 checked exception을 쓰고, 그렇지 않다면 unchecked exception을 사용하는것을 oracle docs에서는 추천하고 있다.

### JVM의 exception handling

```arduino
class ExceptionThrown
{
    static int divideByZero(int a, int b){

        int i = a/b;

        return i;
    }

    static int computeDivision(int a, int b) {

        int res =0;

        try {
        res = divideByZero(a,b);
        } catch (NumberFormatException ex) {
        System.out.println("exception in computeDivision");
        }
        return res;
    }

    public static void main(String args[]){

        int a = 1;
        int b = 0;

        try {
            int i = computeDivision(a,b);
        } catch (ArithmeticException ex) {
            System.out.println("exception in main catch");
        }
    }
}
```

 위 코드는 main -> computeDivision -> divideByZero 으로 호출을 하게 되고 divideByZero 메서드에서 0으로 나누기 때문에 RuntimeException 중 하나인 `ArithmeticException`이 발생하게됩니다. 하지만 해당 method에는 처리할 수 있는 catch가 존재하지 않기 때문에 이전 메서드인 computeDivision 메서드로 돌아가 적절한 exception 처리가 있는지 확인하며 해당 메서드에도 없는것을 확인한 후 main으로 넘어와 적절한 exception 처리가 이루어지며 결과적으로 출력되는 결과는 `exception in main catch`가 된다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/c0e049cc-b6ff-44ef-94c4-c980d4066009)

Exception Chaining 구조

이러한 프로세스는 JVM의 기본 Exception Handling을 따른다.

메서드에서 Exception이 발생하면 해당 메서드는 **Exception Object(exception의 이름과 설명, 프로그램의 현재 상태, exception 발생 위치의 메서드 리스트[call stack]를 포함)**를 생성하고 JVM에 넘긴다. 

<aside style="background-color: #d4e4e9; font-size: 0.4rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
이러한 과정을 `Exception을 던진다(throwing an Exception)`라고 표현한다.
</aside>

<br>

그리고 아래와 같은 프로세스로 exception이 처리된다.

<br>


1. **call stack을 순회**하며 적절한 exception handler(try-catch)를 찾는다.
2. 만약 적절한 exception handler를 찾았다면 해당 handler로 exception을 넘긴다.
    - 적절한 exception handler란 던져진 exception과 매칭되는 exception이다.
3. 하지만 모든 call stack을 찾아도 적절한 handler를 찾지 못했다면 default exception handler가 실행된다.
    - default exception handler는 exception 정보를 노출하며 해당 thread를 중지시킨다.

### exception이 발생했을 때 어떻게 처리할 수 있을까요?

exception을 처리하는 방법은 3가지 정도로 나타낼 수 있다.

1. 예외복구
    - 다른 작업 흐름 유도
2. 예외처리 회피
    - 처리하지 않고 호출 한 쪽으로 throw
3. 예외전환
    - 명확한 의미의 예외로 전환 후 throw

<aside style="background-color: #d4e4e9; font-size: 0.4rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
java에서는 `try`, `catch`, `throw`, `throws`, `finally`의 5가지 키워드로 exception 처리를 구현할 수 있습니다. 
</aside>
<br>

만약 `try` 블럭 안에서 exception이 발생하면 해당 exception은 JVM에 던져진다. 그리고 `catch` 블럭을 사용하면 해당 exception을 처리할 수 있다. 
수동으로 exception을 발생시키기 위해서는 `throw` 키워드를 이용할 수 있다. 호출 한 쪽으로 exception을 위임하기 위해서는 `thorws` 키워드를 사용할 수 있다. try - catch에서 반드시 실행시켜야하는 코드가 있다면 `finally` 블럭에 작성하면 된다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}