---
title: "[Java] StringTokenizer"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)
### **StringTokenizer**



<aside style="background-color: #d4e4e9; font-size: 0.4rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
⚡ StringTokenizer 클래스는 문자열을 우리가 지정한 구분자로 문자열을 쪼개주는 클래스이다. 그렇게 쪼개어진 문자열을 우리는 토큰(token)이라고 부른다.
</aside>


StringTokenizer를 사용하기 위해서는 **java.util.StringTokenizer**를 import해야한다. 사용법은 굉장히 쉽다. 
사용하는 메소드도 몇개 없다. 자주 사용하는 메소드 설명과 예제를 통해 이 클래스를 어떻게 사용하는지 살펴보자.

**생성자(Constructor)**

| 생성자 | 설명 |
| --- | --- |
| public StringTokenizer(String str); | 절달된 매개변수 str을 기본(default) delim으로 분리한다. 기본 delimiter는 공백 문자들인 " \t\n\r\t"이다. |
| public StringTokenizer(String str,String delim); | 특정 delim으로 문자열을 분리한다. |
| public StringTokenizer(String str,String delim,boolean returnDelims); | str을 특정 delim으로 분리시키는데 그 delim까지 token으로 포함할지를 결정한다. 그 매개변수가 returnDelims로 true일시 포함, false일땐 포함하지 않는다. |

**int countTokens()**

남아있는 token의 개수를 반환한다. 전체 token의 갯수가 아닌 현재 남아있는 token 개수이다.

**boolean hasMoreElements(), boolean hasMoreTokens()**

다음의 token을 반환한다. StringTokenizer는 내부적으로 어떤 위치의 토큰을 사용하였는지 기억하고 있고 그 위치를 다음으로 옮긴다. 두가지 메소드는 모두 같은 값을 반환한다.

**Object nextElement(), String nextToken()**

이 두가지 메소드는 다음의 토큰을 반환한다. 두가지 메소드는 같은 객체를 반환하는데 반환형은 다르네요. nextElement는 Object를, nextToken은 String을 반환하고 있다.

### **예제**

이제 몇가지 예제를 통해서 더 자세히 알아보도록 합시다.

**0) String 클래스에 있는 split 메소드 이용**

```java
public static void main(String[] ar){
	String str="this string includes default delims";
	System.out.println(str);
	System.out.println();

	System.out.println("==========using split method============");
	String []tokens=str.split(" ");

	for(int i=0;i<tokens.length;i++){
		System.out.println(tokens[i]);
	}
}
```

String클래스의 메소드인 split 메소드를 사용하여 StringTokenizer를 흉내낼 수 있다. split이 반환하는 값은 String 배열이다.

this string includes default delims

---

**1) Default Delim을 이용**

```java
public static void main(String[] ar){
	String str="this string\tincludes\ndefault delims";
	StringTokenizer stk=new StringTokenizer(str);
	System.out.println(str);
	System.out.println();

	System.out.println("total tokens:"+stk.countTokens());
	System.out.println("================tokens==================");
	while(stk.hasMoreTokens()){
		System.out.println(stk.nextToken());
	}
	System.out.println("total tokens:"+stk.countTokens());
}
```

코드의 while문을 보면 토큰이 있는지 확인한 후 있다면 다음 토큰을 가져온다. 이렇게 하나씩 토큰을 소비한다고 보면되는데, 이런 패턴이 StringTokenizer를 사용하는 가장 일반적인 사용방법이다.

**실행결과**

default delims

total tokens:5

this

includes

delims

---

**2) 특정 delim을 이용**

```java
public static void main(String[] ar){
	String str="this-=string-includes=delims";
	StringTokenizer stk=new StringTokenizer(str,"-=");
	System.out.println(str);
	System.out.println();

	System.out.println("total tokens:"+stk.countTokens());
	System.out.println("================tokens==================");
	while(stk.hasMoreTokens()){
		System.out.println(stk.nextToken());
	}
	System.out.println("total tokens:"+stk.countTokens());
}
```

특정 delim으로 문자열을 분리하는 예제이다. 여기서는 "-"와 "="으로 분리를 했다.

**실행결과**

================tokens==================

string

delims

---

2-1) String의 split과 비교

```java
public static void main(String[] ar){
	String str="this-=string-includes=delims";
	System.out.println(str);
	System.out.println();

	String[] tokens=str.split("-=");
	System.out.println("total tokens:"+tokens.length);
	System.out.println("================tokens==================");

	for(int i=0;i<tokens.length;i++){
		System.out.println(tokens[i]);
	}

}
```

split을 이용하면 조금 다른 결과가 나온다. split은 정확히 "-="으로 문자를 쪼개기 때문에 "this**-=**string-includes=delims"에서 빨간 부분을 기준으로 쪼개는 거다. 결과를 확인해보자.

**실행결과**

================tokens==================

string-includes=delims

---

**3) delim까지 포함**

```java
public static void main(String[] ar){
	String str="this-string-includes=delims";
	StringTokenizer stk=new StringTokenizer(str,"-=",true);
	System.out.println(str);
	System.out.println();

	System.out.println("total tokens:"+stk.countTokens());
	System.out.println("================tokens==================");
	while(stk.hasMoreTokens()){
		System.out.println(stk.nextToken());
	}
	System.out.println("total tokens:"+stk.countTokens());
}

```

위의 예제의 생성자에서 세번째 인자를 true로 전달했을때의 예제이다. 이때 "-"와 "="를 토큰으로 포함하게 된다. 이 예제에서 true를 전달하지 않고 false로 전달한다면 위의 예제와 같은 결과가 나오게 된다.

**실행결과**

================tokens==================

- 
- 

=

total tokens:0

---


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}