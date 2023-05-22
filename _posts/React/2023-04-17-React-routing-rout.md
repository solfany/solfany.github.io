---
title: "[React] Routing"
categories:
  - React
tags: [React, Routing]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---


## **Routing**

**Nested Routing과 Routing은
모두 React Router 라이브러리에서 제공하는 기능으로,
React 애플리케이션에서 다른 URL 경로에 대한 렌더링을 처리하는 방법을 제공한다.** 

<br>


**Routing은 간단히 말해 URL 경로와 컴포넌트를 매핑하는 것이다.**

💡 예를 들어,
/home 경로에 대한 렌더링을 처리하는 컴포넌트를 정의하여,
/home 경로에 접속할 때 이 컴포넌트를 렌더링하도록 지정할 수 있다. 

**Routing은 이와 같이 URL 경로와 컴포넌트를 일대일로 매핑하는 방식을 제공합니다.**


- 다른 주소에 다른 화면을 보여주는 것을 라우팅이라고 한다.
- 리액트 자체에 이 기능이 내장되어 있지 않기 때문에 라이브러리를 사용하여 작업을 진행
- 리액트 라우팅 라이브러리는 react-router, reach-routh, Next.js 등이 있고 가장 많이 사용하는 것이  react-router이다.
<br>
<br>

## Nested Routing

반면에, Nested Routing은 Routing을 중첩하여,
URL 경로와 컴포넌트를 계층적으로 매핑하는 방식이다.

💡 예를 들어, 

/home/users 경로에 대한 렌더링을 처리하는 컴포넌트를 정의하여,
/home/users 경로에 접속할 때 이 컴포넌트를 렌더링하도록 지정할 수 있다. 

이때,
/home 경로에 대한 렌더링을 처리하는 컴포넌트와 /home/users 경로에 대한 렌더링을 처리하는 

컴포넌트를 중첩하여, 계층적으로 매핑한다.



<br>
<br>



## React Router란?

React Router는 위에서 살펴본 SPA의 라우팅 문제를 해결하기 위해서 거의 표준처럼 사용되고 있는 네비게이션 라이브러리이다.

React Router를 사용하면 앱에서 발생하는 

라우팅이 `location`나 `history`와 같은 브라우저 내장 API와 완벽하게 연동이 된다.

따라서 SPA에서 제공하는 다이나믹한 사용자 경험을 그대로 살리면서도 기존 웹사이트에서 가능하던 브라우저 상의 매끈한 라우팅을 제공할 수 있다. 




<br>
<br>


## React Router 설치

React Router는 Web 용과 Native 용이 존재한다. 

아래와 같은 명령어를 입력하여

 Web 용 `react-router-dom`을 React 애플리케이션 프로젝트에 설치해준다.

`$ npm i react-router-dom`


<br>
<br>


## React Router 핵심 컴포넌트

React Router를 이해하는데 핵심이 되는 3가지 컴포넌트 대해서 먼저 짚고 넘어가가겠다.


<br>
<br>


✔️ Link 컴포넌트

HTML의 `<a>` 태그와 유사한 기능을 하는 컴포넌트라고 생각하시면 이해가 쉽다. 

`<a>` 태그는 `href` 속성을 통해 이동할 경로를 지정하는 반면에

`<Link>` 컴포넌트는 `to` prop을 통해서 이동할 경로를 지정해준다.

```jsx
<Link to="/home">Home</Link>
```

> **예를 들어, 위의 코드는 브라우저에서 클릭이 가능한 `About`으로 랜더링되고,**
> 
> 
>  **`About`를 클릭하면 주소창의 경로가 `<도메인 네임>/about`으로 갱신됩니다. 일반적으로 화면 상단이나 좌측에 위치한 네비게이션 바를 구현할 때 주로 사용하게되는 컴포넌트이다.** 
> 



<br>
<br>


## ✔️ Route 컴포넌트

`<Route>` 컴포넌트는 현재 주소창의 경로와 매치될 경우 

보여줄 컴포넌트를 지정하는데 사용된다. 

`path` prop을 통해서 매치시킬 경로를 지정하고, 

`component` prop을 통해서 매치되었을 때 보여줄 컴포넌트를 할당한다.

```jsx
<Route path="/home" component={Home} />
```

> **예를 들어, 위의 코드는 현재 주소창의 경로가 `/about`일 경우 `About`라는 컴포넌트를 보여준다.**
> 
> 
> **일반적으로 현재 주소창의 URL 경로에 따라 특정 컨텐츠를 보여주거나 숨기기 위해서 사용될 수 있다.** 
> 




<br>
<br>



## ✔️ Router 컴포넌트

`<Router>` 컴포넌트는 위에 나온 `<Route>`와 `<Link>` 컴포넌트가 함께 유기적으로 동작하도록 묶어주는데 사용한다. 

다시 말해, `<Route>`와 `<Link>` 컴포넌트는 

DOM 트리 상에서 항상 `<Router>`를 공통 상위 컴포넌트로 가져야한다.

```jsx
<Router>
  ...
  <Link />
  <Link />
  ...
  <Route />
  <Route />
  ...
</Router>
```

> 즉, 전체적으로 React Router를 사용하는 애플리케이션은 이와 같은 구조를 가지게 된다.
> 
> 
> 실제 프로젝트에서는 위 컴포넌트들이 여러 파일에 걸쳐서 흩어져 있을 수도 있겠지만, 
> 
> 이 큰 그림을 염두해두고 코드를 읽다보면 어렵지 않게 라우팅 흐름을 파악할 수 있을 것이다.
> 



<br>
<br>



## ✔️ React Router로 라우팅 구현

자 그럼, 처음에 직접 구현했던 라우팅을 React Router를 이용해서 재구현 해보겠다. 

> **먼저 설치한 `react-router-dom` 패키지로 부터 3가지 핵심 컴포넌트를 import해야한다.**
> 
> 
> 예시는 아래와 같다. 
> 

```jsx
import { Link, Route, BrowserRouter as Router } from "react-router-dom";
```

<br>

사실 React Router가 제공하는 `<Router>` 컴포넌트가 여러 종류가 있는데, 

여기서는 대게 일반적은 라우팅을 위해 사용되는 `<BrowserRouter>`를 사용하였다. 
<br>

1️⃣ 먼저, 헤더 부분을 `<Link>` 컴포넌트를 사용해서 리팩토링 한다.

2️⃣ `to` prop에 해당 메뉴 클릭 시 이동해야할 경로를 지정한다.

```jsx
<header>
  <Link to="/">
    <button>Home</button>
  </Link>
  <Link to="/about">
    <button>About</button>
  </Link>
  <Link to="/users">
    <button>Users</button>
  </Link>
</header>
```

3️⃣ 다음, 메인 부분을 `<Route>` 컴포넌트를 사용해서 리팩토링 한다.

4️⃣ `path` prop에 매치 시 비교될 경로를 지정하고, 

`component` prop에 매치 시 보여줄 컴포넌트를 할당한다.

<br>

여기서 `/` 경로를 사용하는 `<Route>` 컴포넌트에만 `exact` prop이 사용된 이유는,

React Router의 디폴트 매칭 규칙 때문이다. 

React Router는 `path` prop의 경로와 현재 브라우저의 

주소창의 URL 경로 (`location.pathname`)와 비교를 하는데

현재 URL 경로 값이 `<Route>`의 `path` porp 값과 전체가 아닌 

앞부분만 일치해도 매치되는 것으로 간주한다.

따라서 `path`가 `/`일 경우, `/` 뿐만 아니라 `/`로 시작하는 모든 URL 경로, 

사실 상 가능한 모든 경우의 수의 경로와 매치가 된다.
<br>


그렇기 때문에, `exact` prop이 없으면, 의도치 않게 `Home` 컴포넌트가 URL 경로와 상관없이 

항상 보여지게 된다.


하지만 `exact` prop을 붙여주면 URL 경로 값이 

`<Route>`의 `path` 값과 완벽히 전체가 일치해야 매치되는 것으로 처리를 해준다.

```jsx
<main>
  <Route exact path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/users" component={NotFound} />
</main>
```

<br>


마지막으로 `<Router>` 컴포넌트로 위에서 작성한 모든 `<Link>` 컴포넌트와 `<Route>` 컴포넌트를 함께 감싸주기만 하면 끝이다.

```jsx
import React from "react";
import { Link, Route, BrowserRouter as Router } from "react-router-dom";
import Home from "./Home";
import About from "./About";
import NotFound from "./NotFound";

function App() {
  return (
    <Router>
      <header>
        <Link to="/">
          <button>Home</button>
        </Link>
        <Link to="/about">
          <button>About</button>
        </Link>
        <Link to="/users">
          <button>Users</button>
        </Link>
      </header>
      <hr />
      <main>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/users" component={NotFound} />
      </main>
    </Router>
  );
}
```

이제 브라우저에서 네이게이션 메뉴를 클릭해보면 브라우저의 주소가 현재 페이지에 맞게 갱신이 되는 것을 확인할 수 있을 것이다. 

뿐만 아니라, 뒤로 가기, 앞으로 가기, 새로 고침 버튼들도 일반 웹사이트를 서핑하듯이 작동하는 것을 확인할 수 있을 것이다.



<br>
<br>



## 404 페이지 처리

SPA를 개발할 때도 많은 경우, 브라우저에 잘못된 경로가 입력되었을 때, 

특정한 404 페이지를 보여줘야야 한다. 

이럴 경우, React Router에서 제공하는 

또 다른 컴포넌트인 `<Switch>` 로 모든 `<Route>` 컴포넌트로 묶어줘야 한다. 

`<Switch>` 컴포넌트를 사용하면 그 하위에 있는 `<Route>` 컴포넌트 중에 매치되는 

제일 첫번째 컴포넌트만 보여주고, 그 이후에 나오는 Route 컴포넌트는 매치되더라도 무시된다.

(따라서 <Route> 컴포넌트의 순서가  중요한 이유가 된다) 

그 다음에 path prop이 없는 <Route> 컴포넌트를 하나 추가해주면, 이 <Route>는 모든 경로에 매치가 가능해지고, 여기에 404 컴포넌트를 할당해줄 수 있습니다. 그러면, 자연스럽게 위에 나온 <Route> 중에 매치되는 것이 없었을 경우, 제일 아래까지 내려올 것이고, 이 마지막 <Route> 컴포넌트가 매치되어 404 페이지가 보여질 것입니다.

```jsx
<main>
  <Switch>
    <Route exact path="/" component={Home} />
    <Route path="/about" component={About} />
    <Route component={NotFound} />
  </Switch>
</main>
```
  
  

<br>
<br>

  



  

  
## react-router-dom 설치

React-Router는 웹과 앱용이 있다 . 

아래와 같이 입력하여 Web용 react-router-dom을 설치할 수 있다. 

- react-router : 웹&앱
- react-router-dom : 웹
- yarn add react-router-dom  : 웹
  
  
```jsx
npm i react-router-dom
// 또는
yarn add react-router-dom
```
  
    
**react-router-dom**

- 리액트의 네이게이션 라이브러리이다.
- React-Router를 사용하면 앱에서 발생하는 라우팅이 location이나 history와 같은 브라우저 내장 API와 완벽하게 연동이 된다.

  

<br>
<br>

## 정리

즉, Nested Routing은 Routing을 **<<중첩>>**하여,
URL 경로와 컴포넌트를 계층적으로 매핑하는 방식을 제공하는 반면,
Routing은 URL 경로와 컴포넌트를 일대일로 매핑하는 방식을 제공합니다.
