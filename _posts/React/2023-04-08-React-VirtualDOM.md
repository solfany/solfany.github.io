---
title: "[React] 구조와 Virtual DOM"
categories:
  - React
tags: [React, Virtual DOM]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---



React 애플리케이션은 크게 두 부분으로 나눌 수 있다.

컴포넌트 계층 구조와 Virtual DOM으로 나눌 수 있다. 

<br>


## 컴포넌트 계층 구조

React 애플리케이션은 컴포넌트 계층 구조로 구성된다.

즉, 각 컴포넌트는 다른 컴포넌트를 포함할 수 있으며, 이를 통해 복잡한 UI를 구성할 수 있다.

이러한 컴포넌트 계층 구조는 데이터의 단방향 흐름을 유지하면서, 컴포넌트 간에 데이터를 전달하고, 재사용성을 높이고, 유지보수를 용이하게 한다. 

**React 애플리케이션의 핵심은 컴포넌트이다.** 
React 애플리케이션은 여러 개의 컴포넌트로 이루어져 있으며, 

각 컴포넌트는 각자의 역할을 수행한다.  



<br>

✔️  props 는 부모 컴포넌트로부터 전달받은 값이다. 

✔️ state 는 컴포넌트 내부에서 관리되는 값이다. 

<br>

"props"와 "state"의 값이 변경되면, React는 자동으로 변경된 값에 따라 렌더링을 업데이트한다. 
React 컴포넌트는 “props"와 "state"라는 두 가지 개념을 사용하여 동적으로 렌더링된다.


<br>
<br>


## Virtual DOM

React 애플리케이션은 Virtual DOM을 사용하여 UI를 렌더링한다. 
Virtual DOM은 React가 컴포넌트의 상태 변화를 감지하고,
변경된 부분만 실제 DOM에 반영하는 데 사용되는 **가상의 DOM** 이다.

💡 React는 실제 DOM을 조작하는 것보다 Virtual DOM을 조작하는 것이 훨씬 빠르고 효율적이기 때문에, 애플리케이션의 성능을 높일 수 있다.

💡 또한, Virtual DOM을 사용하면 개발자가 직접 DOM을 조작하지 않고,
React에게 UI 렌더링을 위한 코드를 작성하면 되기 때문에, 코드의 가독성과 유지보수성도 높아진다.

💡 React는 Virtual DOM과 실제 DOM 사이에서 자동으로 변환 작업을 수행하여,
최종적으로 변경된 부분만 실제 DOM에 반영된다.



<br>
<br>



## React의 Virtual DOM 의 작동 방식

React의 Virtual DOM은 다음과 같은 방식으로 동작한다.  

<br>

✔️ **컴포넌트 상태 변화**
React 컴포넌트의 상태가 변화하면, React는 이를 감지한다.

✔️ **Virtual DOM 생성**
React는 이전 상태와 현재 상태를 비교하여 변경된 부분을 식별하고, Virtual DOM을 생성한다.

✔️ **Virtual DOM 비교**
React는 이전 Virtual DOM과 새로운 Virtual DOM을 비교하여 변경된 부분을 찾는다.

✔️ **변경된 부분 실제 DOM에 반영**
React는 변경된 부분만을 실제 DOM에 반영한다.   

<br>

이를 통해, 불필요한 DOM 조작을 최소화하고, 성능을 향상시킨다.


<br>
<br>


## PS

이러한 방식으로 React는 사용자 인터페이스를 효율적으로 렌더링하면서도,
최소한의 DOM 조작으로 성능을 최적화할 수 있다! 

또한, React는 이벤트 처리와 데이터 흐름 등을 다루기 위한 다양한 기능과 생태계를 제공한다.
React는 하나의 라이브러리일 뿐만 아니라, 다양한 생태계와 함께하는 프레임워크로 발전하면서,
개발자들이 더욱 효율적으로 UI 개발을 할 수 있게 도와주었다 🐰
