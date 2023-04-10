---
title: "[Java] Unhandled exception type IOException 에러 발생 해결하기"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![image](https://github.com/solfany/solfany.github.io/assets/123814718/20775dd8-de4d-47b2-8187-0878688831f8)


<aside style="background-color: #f7dce0; font-size: 0.6rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">
[Java] Unhandled exception type IOException 에러 발생
</aside>



백준 알고리즘 자바 문제를 푸는 도중 해당 에러에 직면했다. 아마 예외 처리 때문인 것 같은데 
원인이 뭘까? 알아보자
<br>

```java
package backjoon;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class N11021 {
	public static void main(String[] args) {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); //입력 
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out)); //출력 
		
		int N = Integer.parseInt(br.readLine());
		
		StringTokenizer T;   // 문자열 나누는  입력 
	}		
}
```
위의 코드에서 해당 에러가 발생했다. 


## 헤결 방법

```java
package backjoon;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class N11021 {
	public static void main(String[] args)throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); //입력 
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out)); //출력 
		
		int N = Integer.parseInt(br.readLine());
		
		StringTokenizer T;   // 문자열 나누는  입력 

	}		

}
```

[예외 처리 발생 원인 ](https://www.notion.so/c57aa34516ae4fa898fe7b91ab38aafb?pvs=21)

여기서 주어진 코드는 **`throws IOException`** 을 사용하여 **`main`** 메서드에서 발생할 수 있는 **`IOException`** 을 처리하지 않고 상위 메서드(이 경우 JVM)에 전달하도록 지시한다 만약 이를 생략하면, **`main`** 메서드 내에서 발생 가능한 **`IOException`** 에 대한 처리가 없다는 의미로 컴파일 오류가 발생한다

1. **예외를 현재 위치에서 처리(try-catch)**: **`try-catch`** 블록을 사용하여 예외 발생 시 적절한 처리를 진행한다
    
    ```java
    javaCopy code
    public static void main(String[] args) {
        try {
            // 코드 내용
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    ```
    
2. **예외를 상위 메서드로 전달(throws)**: 메서드 선언부에 **`throws`** 키워드를 사용하여 해당 예외를 처리할 의무를 호출한 메서드나 호출자에게 전달한다
    
    ```java
    javaCopy code
    public static void main(String[] args) throws IOException {
        // 코드 내용
    }
    
    ```
    

예외 처리를 하기 위한 두 가지 주요 방법은 다음과 같다. 🤔

만약 **`throws IOException`**을 작성하지 않으면, 해당 메서드(**`main`** 메서드) 안에서 I/O 관련 작업을 수행할 때 발생할 수 있는 예외 상황에 대해 처리를 해주지 않은 것으로 판단된다. 이렇게 처리되지 않은 예외는 컴파일 오류를 발생시킨다..

**`throws IOException`** 은 예외 처리를 위한 문법이다. **`IOException`** 은 입력/출력 작업 중 발생할 수 있는 예외이다. 여기서 **`BufferedReader`**, **`BufferedWriter`**, **`InputStreamReader`**, **`OutputStreamWriter`** 등은 Java의 I/O 관련 클래스이므로, 이들 클래스의 메서드는 **`IOException`** 을 발생시킬 가능성이있다. 
<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}