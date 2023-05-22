---
title: "[React] Styled Components"
categories:
  - React
tags: [React, Components]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---



## Component 란?

✔️ **React에서 UI(User Interface)를 구성하는 빌딩 블록(Building Block)이다.** 

컴포넌트는 UI를 구성하는 작은 단위의 모듈이며,
각 컴포넌트는 독립적으로 작동하면서 화면에 보여지는 UI 요소를 담당한다.

예를 들어, 웹 애플리케이션의 로그인 페이지를 구성하는 경우, 

입력 폼, 로그인 버튼, 회원 가입 버튼 등의 UI 요소는 각각 하나의 컴포넌트로 작성할 수 있다.
이렇게 작성된 컴포넌트들은 결합하여 로그인 페이지를 완성하게 된다.

React에서 컴포넌트는 클래스 형태로 작성할 수도 있고,
함수 형태로 작성할 수도 있는데

 클래스 컴포넌트는 `React.Component` 클래스를 상속받아 작성하며,
 함수 컴포넌트는 `function` 키워드를 사용하여 작성하게 된다. 

 <br>
 <br>


## Styled Components 란?

React 애플리케이션에서 CSS 스타일을 작성하고 관리하기 위한 방법 중 하나이다. 


 <br>
 <br>


## Styled Components 사용 방법

**CSS 스타일을 작성하는 대신에 React 컴포넌트를 작성한다.**

이때, Styled Components는 템플릿 리터럴을 사용하여 CSS 스타일을 작성한다.

예를 들어, 다음과 같이 styled.div 함수를 사용하여 div 요소를 스타일링할 수 있다.

```jsx
import styled from 'styled-components';
const StyledDiv = styled.div`
  color: red;
  font-size: 16px;
`;
function MyComponent() {
  return (
    <StyledDiv>Hello, World!</StyledDiv>
  );
}
```

위의 코드에서 `StyledDiv`는 div 요소를 스타일링하는 React 컴포넌트이다

`styled.div` 함수를 호출하면,
템플릿 리터럴 안에 CSS 스타일을 작성할 수 있다.

<HTML 태그/>를 React 컴포넌트로 래핑하여 사용한다. 

**이때, 템플릿 리터럴 안에는 Javascript 표현식을 사용할 수 있으며,
이를 통해 동적으로 스타일을 지정할 수도 있다.**


 <br>
 <br>

## Styled Components 사용시 장점

✔️ CSS 스타일을 전역으로 관리하는 것보다
컴포넌트별로 관리하는 것이 더욱 쉽고 간편하다!

✔️ CSS 스타일이 컴포넌트의 스코프 안에서 유지되므로, 

CSS 스타일 간의 충돌 문제를 방지할 수 있다! 

✔️ 또한, React의 가상 DOM(Virtual DOM)을 사용하여
효율적으로 UI를 업데이트할 수 있기 때문에,
React는 대규모 애플리케이션 개발에 매우 적합하다.

✔️ CSS 클래스 이름이나 ID를 사용하는 대신,
JSX의 컴포넌트 이름을 사용하여 스타일을 적용할 수 있다.

React 컴포넌트를 정의하는 동시에 CSS 스타일을 작성할 수 있으며,
이를 통해 코드의 1️⃣**가독성**과 2️⃣**유지보수성**을 높일 수 있다.
