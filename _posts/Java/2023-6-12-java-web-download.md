---
title: "[Java] Web Image Download"
categories:
  - Java
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/blog-main/1.png?raw=true)

## 이미지 다운 받기

```java
package ch15;

import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.URL;

public class WebImageDownload {

    public static void main(String[] args) {
        String website = "http://www.gstatic.com/webp/gallery/1.sm.jpg";
        System.out.println(website + " 사이트에서 이미지를 다운로드합니다.");
        URL url;
        byte[] buffer = new byte[2048];

        try {
            url = new URL(website);
            try (InputStream in = url.openStream();
                 FileOutputStream out = new FileOutputStream("test.jpg")) {
                int length;
                while ((length = in.read(buffer)) != -1) {
                    System.out.println(length + "바이트 크기만큼 읽었습니다!");
                    out.write(buffer, 0, length);
                }
                System.out.println("이미지 다운로드가 완료되었습니다.");
            } catch (Exception e) {
                System.out.println("입출력 예외: " + e.getMessage());
            }
        } catch (Exception e) {
            System.out.println("URL 예외: " + e.getMessage());
        }
    }
}
```

설정한 주소에서 이미지 파일을 다운로드 하는 코드이다.

## 코드 분석

이 코드는 특정 웹 주소(URL)에서 이미지를 다운로드하여 로컬 파일 시스템에 저장하는 Java 프로그램이다.
코드를 자세히 살펴보겠다.

1. **필요한 패키지와 클래스를 임포트한다.**

```java
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.URL;
```

- **`java.io.FileOutputStream`**: 파일에 데이터를 쓰기 위한 출력 스트림
- **`java.io.InputStream`**: 모든 바이트 입력 스트림의 슈퍼 클래스
- **`java.net.URL`**: URL을 나타내는 클래스

1. **`WebImageDownload` 클래스를 정의한다.**
2. **메인 메서드를 정의한다.**

```java
public static void main(String[] args) { ... }
```

- 메인 메서드에서 프로그램이 시작된다.

1. **이미지 다운로드를 위한 웹사이트 URL을 정의한다.**

```java
String website = "http://www.gstatic.com/webp/gallery/1.sm.jpg";
```

- 해당 URL에서 이미지를 다운로드하게 된다.

1. **버퍼를 정의한다.**

```java
byte[] buffer = new byte[2048];
```

- 2KB 크기의 버퍼를 사용하여 이미지를 작은 덩어리로 읽게 된다.

1. **URL 객체를 생성한다.**

```java
url = new URL(website);
```

- 위에서 정의한 문자열 URL을 이용해 **`URL`** 객체를 생성한다.

1. **입출력 스트림을 사용하여 이미지를 다운로드하고 파일로 저장한다.**

```java
try (InputStream in = url.openStream();
     FileOutputStream out = new FileOutputStream("test.jpg")) {
    int length;
    while ((length = in.read(buffer)) != -1) {
        System.out.println(length + "바이트 크기만큼 읽었습니다!");
        out.write(buffer, 0, length);
    }
    System.out.println("이미지 다운로드가 완료되었습니다.");
}
```

- **`url.openStream()`**은 URL에서 데이터를 읽기 위한 입력 스트림을 연다.
- **`FileOutputStream`**은 지정된 파일 이름("test.jpg")으로 출력 스트림을 연다.
- **`in.read(buffer)`**를 사용하여 버퍼 크기만큼 데이터를 읽고, 읽은 바이트의 길이를 반환합니다. 데이터가 더 이상 없으면 -1을 반환하게 된다.
- **`out.write(buffer, 0, length)`**를 사용하여 파일에 데이터를 쓰는 동안 버퍼의 데이터를 사용한다.

1. **예외 처리**

- URL과 관련된 예외를 처리하는 외부 try-catch 블록과 입출력 관련 예외를 처리하는 내부 try-catch 블록이 있는데 해당 블록에서 예외를 다루게 된다.

결론적으로, 위의 과정을 거친 후 지정된 URL에서 이미지를 다운로드하여 "test.jpg"라는 로컬 파일로 저장하게 된다.

## 콘솔 출력 결과

![스크린샷 2023-06-21 오전 11.04.49.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0a9e8be-a727-435b-bd14-27b7669bd498/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-06-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.04.49.png)

## 다운 받은 이미지

![스크린샷 2023-06-21 오전 11.15.55.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f1190e7-7aec-4cd3-9135-2aa736ba0625/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-06-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.15.55.png)
