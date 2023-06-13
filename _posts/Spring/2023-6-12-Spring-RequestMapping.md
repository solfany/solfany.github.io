---
title: "[Spring]원격 프로그램 실행 RequesstMapping "
categories:
  - Spring
tags: [Spring, Fastcampus]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## 원격 프로그램 실행 (RequesstMapping)

우리는 client에서 오는 요청을 처리하기 위한 api url을 매핑할 때 Spring의 `@RequestMapping`이라는 어노테이션을 사용한다. Spring은 사용자의 편리를 위해 RequestMapping을 http에서 지원하는 4가지 method인 `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`과 추가적으로 `@PatchMapping`까지 여러가지 방법의 매핑 방식으로 확대하여 제공하기도 한다.

## @RequesstMapping 이란?

Spring 개발 시 특정 URL로 요청(Request)을 보내면 Controller에서 어떠한 방식으로 처리할지 정의한다.

이때 들어온 요청을 특정 method와 매핑하기 위해 사용하는 어노테이션이 바로 @RequestMapping이다.

- @RequestMapping은 Controller단에서 사용되는데, DispatcherServlet이 Controller 파일을 찾고, 논리적 주소가 매핑된 Method를 찾기 위해서는 @Controller와 @RequesetMapping이 작성되어야 한다.
- URL와 Controller의 method 매핑을 설정하는 어노테이션
- URL 이외에도 다양한 속성을 지정 가능
- URL 템플릿 기능을 이용하면 URL속의 값을 쉽게 얻을 수 있음

## 사용 이유

@RequesstMapping 작성 예시

```java
package com.fastcampus.test;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller // 1. 프로그램 등록
public class SpringTest {

    @RequesstMapping("/hello") //2. URL과 main()을 연결
    public void main() {
        System.out.println("Hello");
    }
}
```

로컬로 프로그램을 실행시킨다는 가정 하에 우리는 `http://localhost:8080/hello` 로 Hello 출력 요청을 보낸다.

여기서 알 수 있다싶이 RequestMapping은 요청이 들어왔을 시에 컨트롤러와 매핑해주고, 그 컨트롤러를 실행시켜 응답을 받는 것을 알 수 있다.

또한 실무에서 사용되는 대부분의 컨트롤러는 @RequestMapping을 사용한다. 컨트롤러의 메서드에 @RequestMapping 어노테이션을 붙이면 해당 URL이 호출될 때 이 메서드가 호출된다.
어노테이션을 기반으로 동작하므로 메서드의 이름을 임의로 지을 수 있다.

## **@RequestMapping이 받는 옵션**

이제는 @RequestMapping이 받을 수 있는 옵션에 대해서 알아보도록 하자.

RequestMapping은 기본적으로 같은 url과 모든 옵션이 같을 수 없다.

이렇게 지정하는 옵션은 handler에서 매핑하는 기준이 된다.

value, method, params, headers, consumes, produces 중에서 하나라도 달라야지 올바르게 handler가 매핑해줄 수 있다.

### **value**

value는 연결할 url을 말한다. 보통 호스트 주소와 포트 번호를 제외하고 api 설계 규약에 따라 이름을 짓는다. 다음과 같이 설정할 수 있다.

```java
@RequestMapping(value = "/example")
```

value를 제외하고 다른 옵션이 주어지지 않을 경우에는 `value =`을 생략할 수도 있다.

```java
@RequestMapping("/example")
```

[Ant pattern](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/AntPathMatcher.html)을 적용한 url mapping도 가능하다.

예를 들어, 아래와 같이 매핑하면 `/example/1`, `/example/2`, `/example/123` 전부 다 연결할 수 있다.

```java
@RequestMapping("/example/**")
```

{}사이에 변수를 넣어서 url을 매핑하는 것도 가능하다. 이렇게 매핑한 경우 메서드 인자로 `@PathVariable`을 id로 받아야만 한다.

```java
@RequestMapping("/example/{id}")
```

### **method**

RequestMethod로 명명되어 있는 아래 8가지 중 하나를 사용하는 것이 일반적이다.

```java
public enum RequestMethod {
	GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS, TRACE
}
```

적용 예시는 다음과 같다.

```java
@RequestMapping(method = RequestMethod.GET, value = "/example")
```

GET, POST, PUT, PATCH, DELETE 메서드에 대해서는 각각에 맞는 메서드 옵션이 적용된 어노테이션이 존재해서 다음과 같이 사용할 수 있다.

```java
@GetMapping("/example")
```

이렇게 하면 코드가 간결해지고 가독성이 좋아져 많이 사용되는 기법이다.

### **params**

params는 api url을 `/example?id=1&password=2`와 같이 전달하고 싶을 때 사용하는 것으로 params에 전달한 것과 일치하는 param이 붙으면 이 메서드로 매핑해준다.

```java
@RequestMapping(method = RequestMethod.GET, value = "/example", params = {"id", "password"})
public ResponseEntity<Example> getExample(@RequestParam("id") int paramId, @RequestParam("password") String password) {
   Example example = new Example("example" + paramId + password);
   return ResponseEntity.ok(example);
}
```

### **headers**

header의 정보를 전달해주는 옵션이다. 예를 들어 아래와 같이 content-type을 지정해준 경우

```java
@PostMapping(value = "/example/{text}", headers = "content-type=text/plain")
public ResponseEntity<Example> getExample3(@PathVariable("text") String text) {
   Example example = new Example("example" + text);
   return ResponseEntity.ok(example);
}
```

### **produces**

response의 accept-request header가 특정 옵션으로 반환될 것을 지정하는 옵션이다.

응답이 무엇인지 미리 예측하는 것이 불가능하기 때문에 같은 url로 요청이 들어왔을 때 produces 옵션으로 구분해서 실행하는 것은 불가능하다.

그리고 `@RestController`에서 ResponseEntity를 반환하는 경우에는 기본으로 `application/json`으로 값이 지정되어 있기 때문에 특정 옵션을 설정할 수 없다.

produces는 필수 옵션이 아니므로 따로 지정해주지 않아도 `application/json`으로 기본 값이 전달되거나 와일드카드로 값이 전달된다.

```java
@GetMapping(value = "/test", produces = MediaType.TEXT_PLAIN_VALUE)
public String getExample() {
    return "example";
}
```

위와 같이 사용할 수 있다.

### **consumes**

request의 content-type request header가 일치하는 것을 찾는 옵션이다.

요청에 들어오는 인자 값이 무엇인지에 따라서 같은 url, method임에도 구분이 가능하다.

하지만 `@RequestBody`와 `@ModelAttribute`의 경우 HttpMessageConverter에서 객체로 변환하는 과정을 지나며 기본 값으로 `application/json`이 지정되어 있기 때문에 특정 옵션을 줄 수 없다.

consumes는 필수 옵션이 아니므로 지정해주지 않아도 된다.

이 경우 `@RequestBody`, `@ModelAttribute`는 `application/json`이 기본 값, `@RequestParam`, `@PathVariable`은 `text/plan`이 기본 값으로 전달된다.

---

---

## 메인 메서드에 static이 빠진 이유

```java
package com.fastcampus.ch2;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

//1. 원격 호출 가능한 프로그램으로 등록
@Controller
public class Hello {
	int iv = 10;
	static int cv = 20;


	//2. URL과 메서드를 연결
	@RequestMapping("/hello")
	public void main() { //인스턴스 메서드 - iv, cv를 둘다 사용 가능

		System.out.println("Hello ");
		System.out.println(cv);	//	ok
		System.out.println(iv);	// ok
	}

	public static void main2() {  //static 메서드 - cv만 사용 가능
		System.out.println(cv);	//ok
//		System.out.println(iv);	//error

	}
}
```

메인 메서드에서 static이 안들어가있는 이유?

> 인스턴스 메서드는 객채 생성 후 호출 가능
> URL로 원격프로그램을 생성하면 Tomcat 내부에서 객체를 생성하기에 인스턴스 메서드 임에도 호출이 가능하다.
> 또한 인스턴스 메서드일 경우 static메서드와 인스턴스 모두 사용 가능하지만
> static 메서드 일 경우 인스턴스 메서드는 사용할 수 없기에 인스턴스 메서드를 사용하는 편이 더 낫다.

정확히 말하자면, 인스턴스 메서드와 static 메서드는 클래스의 변수에 접근할 때 다른 규칙을 따른다

인스턴스 메서드는 객체의 인스턴스를 생성한 후에 호출되는 메서드이며, 해당 클래스의 인스턴스 변수에 직접 접근할 수 있다.

인스턴스 메서드 내에서는 인스턴스 변수와 static 변수 모두에 접근이 가능하다.

그래서 **`main()`** 메서드에서 **`iv`**와 **`cv`** 모두에 접근할 수 있었다.

반면에 static 메서드는 객체의 인스턴스 없이 호출되는 메서드이기 때문에 인스턴스 변수에 직접 접근할 수 없다.

static 메서드에서는 오직 static 변수에만 접근할 수 있다.

따라서 **`main2()`** 메서드에서는 **`cv`** 변수에는 접근할 수 있지만 **`iv`** 변수에는 접근할 수 없다.

요약하자면:

- 인스턴스 메서드는 인스턴스 변수와 static 변수에 모두 접근할 수 있다.
- static 메서드는 static 변수에만 접근할 수 있고, 인스턴스 변수에는 직접 접근할 수 없다.

따라서, 변수를 사용할 수 있는지 여부는 해당 메서드가 인스턴스 메서드인지 static 메서드인지에 따라 달라진다.

## private 으로 변수 호출이 가능할까?

```java
package com.fastcampus.ch2;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

//1. 원격 호출 가능한 프로그램으로 등록
@Controller
public class Hello {
	int iv = 10;
	static int cv = 20;


	//2. URL과 메서드를 연결
	@RequestMapping("/hello")
	private void main() { //인스턴스 메서드 - iv, cv를 둘다 사용 가능

		System.out.println("Hello ");
		System.out.println(cv);	//	ok
		System.out.println(iv);	// ok
	}

	public static void main2() {  //static 메서드 - cv만 사용 가능
		System.out.println(cv);	//ok
//		System.out.println(iv);	//error

	}
}
```

> 가능하다.
> `@RequestMapping("/hello")` : 해당 메서드들을 외부에서 호출 가능하게 하겠다. 라는 뜻.
> 즉, URL과 외부 메서드들을 연결했기 때문에 가능하다.
> 또한 접근제어자와 상관없이 호출 가능하다.

## 외부 메서드에서 호출이 가능한가

```java
package com.fastcampus.ch2;

public class Main {
	public static void main(String[]arge) {
		Hello hello = new Hello();
		hello.main();
	}
}
```

> 불가능하다.
> "`The method main() from the type Hello is not visible`" Error - Private 라서
> 외부 호출이 불가 하다!

하지만 hello 파일에서는 호출이 가능하지 않았나? 👇🏻
Reflection API 를 사용 했기 때문이다

>

**Reflection API란?**
클래스 정보를 얻고 다룰 수 있는 강력한 기능 제공
java.lang.reflect 패키지 제공

## private 메서드를 호출해보자

```java
package com.fastcampus.ch2;

import java.lang.reflect.Method;

public class Main {
	public static void main(String[]arge)throws Exception {
//		Hello hello = new Hello();
//		hello.main();

		// Reflection API - 클래스 정보를 얻고 다룰 수 있는 강력한 기능 제공
		// java.lang.reflect 패키지 제공
		// Hello 클래스의 Class객체 (클래스 정보를 담고 있는 객체)를 얻어온다.
		Class helloClass = Class.forName("Com,fastcapus.ch2.Hello");

		//class 객체가 가진 정보로 객체 생성
		Hello hello = (Hello)helloClass.newInstance(); //반환타입이 obj이기 때문에 형변환해줘야 한다.
		Method main = helloClass.getDeclaredMethod("main"); //main 메서드 정보 가져옴
		main.setAccessible(true); //private 인 main()을 호출 가능하게 한다.

		main.invoke(hello); //hello.main()

	}
}
```

> spring 에서 Reflection API를 자주 쓴다고 하니 기억해두자!
