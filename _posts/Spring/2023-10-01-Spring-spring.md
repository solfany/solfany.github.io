---
title: "[Spring Boot] spring mvc "
categories:
  - Spring
tags: [Java, Spring, MVC 패턴]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## MVC 패턴 사용하는 이유

사용자가 보는 페이지, 데이터 처리, 그리고 이 2가지를 중간에서 제어하는 컨트롤

이 3가지로 구성되는 하나의 애플리케이션을 만들면 각각 맡은 바에만 집중을 할 수 있게 된다.

공장에서도 하나의 역할들만 담당을 해서 처리를 해서 효율적이게 되는 것 처럼

서로 분리되어 각자의 역할에 집중할 수 있게끔하여 개발을 하고 그렇게 어플을 만든다면,

유지보수성, 애플리케이션의 확장성, 그리고 유연성이 증가하고, 중복코딩이라는 문제점 또한 사라지게 되는 것이다.

### MVC 패턴 - 모델

어플리케이션 정보, 데이터를 나타낸다.

데잍베이스, 처음 정의하는 상수, 초기화값, 변수 등을 뜻한다.

이러한 DATA 정보들을 가공을 책임지는 컴포넌트들을 말한다.

1. 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
   화면 안에 네모박스에 글자가 표현된다면, 네모박스의 화면 위치 정보, 크기 정보, 글자내용, 위치, 포멧 정보 등을 가지고 있어야한다.
2. 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다.
   데이터 변경이 일어낫을 때 모델에서 화면 UI 를 직접 조정해서 수정할 수 있도록 뷰를 참조하는 내부 속성값을 가지면 안 된다.
3. 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야한다.
   모델의 속성중 텍스트 정보가 변경이 된다면, 이벤트를 발생시켜 누군가에서 전달해야하며, 누구낙 모델을 변경하도록 요청하는 이벤트를 보냈을 때 이를 수신하는 처리 방법을 구해야한다.

모델 : 애프리케이션의 정보, 데이터를 나타내며, 시ㅣㄹ제 기능을 처리한 후 결과를 컨트롤러에 반환한다.

## 뷰의 역할

```java
public void actionPerformed(ActionEvent e)
```

액션 리스너를 통해 버튼을 눌렀을 때 콘솔창이 뜨게 만든다.

즉, 사용자에게 보여지는 화면을 구현하는게 뷰 의 역할.

여기서 발생한 이벤트와 입력 데이터들을 컨트롤러에 전달한다.

## 컨트롤러의 역할

```java
public void addTitle(String title, List moviesList){
  try{
      model.addTitle(title, moviesList);
    }catch(Exception e){
    e.pirintStackTrace();
    }
}
```

뷰에서 받은 내용을 가지고 모델 메소드를 호출한다.

- 이벤트에 대해서 적당한 모델을 선택한다.

## 모델의 역할

DATA 정보들의 가공을 책임지는 컴포넌트들을 말한다.

```java
public void addTitle(String title, List movieList){

movieListadd(title);
}
```

실질적으로 영화 제목을 저장하고, 삭제하고 파일을 저장하는 실질적인 클래스

상대경로에 파일이 생성되고 저장한 값들이 출력된다.

- 실제 기능을 처리한 후 결과 컨트롤러에 반환한다.
