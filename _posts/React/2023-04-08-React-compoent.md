---
title: "[React] 컴포넌트 만들기"
categories:
  - React
tags: [React, inflearn]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---


![https://velcdn.com](https://d585tldpucybw.cloudfront.net/sfimages/default-source/blogs/templates/social/reactt-light_1200x628.png?sfvrsn=43eb5f2a_2)

2023년 4월 6일 

<br><br>


## 컴포넌트(Compoent)

컴포넌트는 재사용이 가능한 React 엘리먼트를 반환하는 하나의 구성 요소이다.. 즉 리액트에서 뷰를 표현하는 하나의 구성요소이다.




<br><br>

## 리액트 컴포넌트의 종류

리액트의 컴포넌트는 함수형 컴포넌트, 클래스형 컴포넌트가 존재한다

함수형 컴포넌트 -  JavaScript에서 사용하는 함수를 이용해 만든 컴포넌트

클래스형 컴포넌트 - ES6에서부터 지원하는 class 문법을 이용해 만든 컴포넌트

```jsx
import React, { Component, compoent } from 'react';
import './App.css';

// 컴포넌트 이름 One1 
class One1 extends Component{
  render(){
      return(
				//하나의 최상위 태그
        <header>
          <h1>WEB</h1>
          world wide web!        
          </header>
      );
    }
  }

  class One2 extends Component{
    render(){
      return(
        <nav>
        <ul>
            <li>TOC컴포넌트 입니다. </li>
        </ul>
    </nav>
      );
    }
  }

  class One3 extends Component{
  render(){
    return(
      <article>
      <h2> HTML </h2>
      Content 컴포넌트 입니다.
    </article>
    );
  }
}

class One4 extends Component{
  render(){
    return(
      <article>
      <h2> CSS </h2>
      one4 컴포넌트 입니다.
    </article>
    );
  }
}

// 위에서 만든 컴포넌트를 사용
class App extends Component {
  render(){
    return(
    <div className="App">
      <One1></One1>
      <One2></One2>
      <One1></One1>
      <One3></One3>
      <One4></One4>

    </div>
    );
  }  
}

export default App;
```

<br><br>


## **컴포넌트 만드는 방법**

`import React, { Component, compoent } from 'react';`   최상단 선언

`class` 변수명 `extends Component{`    컴포넌트 변수명 선언

```jsx
import React, { Component, compoent } from 'react';   최상단 선언

class` 변수명 `extends Component{    컴포넌트 변수명 선언
render(){
      return(
        <header>      최상위 태그 입력
          <h1> 들어갈 내용</h1>
          들어갈 내용       
          </header>
      );
    }
  }
```

<br><br>

## 만든 컴포넌트 사용 방법


```jsx
class App extends Component {
  render(){
    return(
    <div className="App">
      <One1></One1>   // 컴포넌트 변수 명
      <One2></One2>
      <One1></One1>
      <One3></One3>
      <One4></One4>

    </div>
    );
  }  
}

export default App;
```



## 정리

> 하나의 틀이라고 생각하면 된다.
> 
> 
> 하나의 최상의 태그만 사용해야 한다.

