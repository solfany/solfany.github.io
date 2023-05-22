---
title: "[React] props, state"
categories:
  - React
tags: [React, props, state]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---



<br>

2023년 4월 19일 

# props/state

****props 와 state는 React에서 데이터를 사용할 때 다루는 개념이다.****

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props1.png?raw=true)

[코드샌드박스 : 다운없이 코드 실습](https://codesandbox.io/s/dank-pond-pfyvq)

<br>

# props란?

**Props 란 무엇인가**

**props는 properties의 줄임말이며 컴포넌트 속성을 설정하는 요소이다.**

✔️부모 컴포넌트가 자식 컴포넌트에 값을 전달할 때 사용한다. (읽기 전용

✔️ 상위 컴포넌트가 하위 컴포넌트에 값을 전달하기 때문에 단방향 데이터 흐름을 갖는다.

✔️  부모 컴포넌트는 수정 가능하지만, 자식 컴포넌트는 읽기만 가능하다.

<br><br>


**Props 사용하기 : 단방향 데이터 흐름**

props 를 사용하려면 두 단계가 필요하다.

1️⃣ 상위 컴포넌트에서 **Props를 지정**하고, 

2️⃣ 하위 컴포넌트에서 받은 **Props값을 렌더링**해야 한다.

이 때 상위 컴포넌트에서 하위 컴포넌트로 프로퍼티가 전달되는데 이것이 **"단방향 데이터 흐름"** 이다.


<br>


**App.js**

```jsx
import React from "react";
import MyComponent from "./MyComponent";

function App() {
    return(
         <MyComponent propValue="헬로 리액트!">Bye 리액트!</MyComponent>
    );
}
export default App;
```

 **상위 컴포넌트에서 Props 지정하여 넘기기**

- App 컴포넌트가 MyComponent 컴포넌트를 포함하고 있다.
- App 컴포넌트에서 MyComponent에 props 값을 지정해준다..
- "propValue"라는 프로퍼티로 "헬로 리액트!"라는 값을 넘겨준다.
- 컴포넌트 태그 사이에 "Bye 리액트!" 라는 값을 한번 넣어준다..


<br>
<br>

**MyComponent.js**

```jsx
import React from "react";

function MyComponent(props) {
    return(
        <div>
            {props.propValue}, {props.children}
        </div>

    );
}
export default MyComponent;
```


<br>


 **하위 컴포넌트에서 받아 Props  렌더링하기**

MyComponent 컴포넌트에서 상위 컴포넌트로 부터 받은 Props 데이터를 

뷰에 렌더링한다.

- **{props.propValue}** : 상위 컴포넌트에서 props 값을 propsValue로 전달했기 때문에 {props.propValue} 로 나타낸다.
- **{props.children}**  : 리액트 컴포넌트 태그 사이에 내용을 보여주는 props 속성이다.

상위 컴포넌트에서 태그 사이에 작성한 "Bye 리액트!" 가 출력된다.

**출력화면**

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props2.png?raw=true)



<br>
<br>


# **Props 타입**

props의 자료형은 자바스크립트의 자료형을 모두 사용 가능하다.

 **문자열 타입 프로퍼티**

- 프로퍼티 타입이 문자열인 경우, 프로퍼티 값을 표현할 때는 **큰 따옴표("")**를 사용한다.

```jsx
<MyComponent name="헬로 리액트!"/>
```

<br>
<br>

**문자열 이외 타입의 프로퍼티**

- 문자열 타입 이외의 프로퍼티 값은 **중괄호({ })**를 사용한다.

```jsx
<MyComponent
	boolProp= {true}//boolean
	arrProp= {['a','b','c']}//배열
	objProp= {{name:'코딩젤리', title:'헬로리액트!'}}//객체
	funcProp= {() => { alert('알림창'); }}//함수
/>
```

---

<br>
<br>


**PropTypes : 데이터 타입 검증하기**

**propTypes는 상위 컴포넌트로부터 전달받은 데이터의 타입을 확인하는 라이브러리이다.**

상위 컴포넌트로부터 전달받은 props가 유효하지 않은 타입의 데이터가 전달되는 경우 콘솔에 에러 경고문이 출력된다.

**PropTypes 써야 하는 이유**

> 실무에서 리액트 앱이 커지는 경우 다양한 props가 쓰이게 된다.
> 

**PropTypes 사용하기 전에**

PropTypes는 원래 리액트에 내장 되어있었으나 React v15.5부터 다른 패키지로 이동했다.

propTypes를 사용하려면 [npm prop-types 라이브러리](https://www.npmjs.com/package/prop-types)를 설치하고 

컴포넌트 파일에 PropTypes 를 import 한다. 

<br>

설치 명령어 

```jsx
npm install --save prop-types
```

<br>

 PropTypes  import

```jsx
import PropTypes from 'prop-types';
```

<br>
<br>

**propTypes 사용하기**

propTypes를 사용하여 프로퍼티를 지정해보겠다. 

프로퍼티 타입 체크는  **PropType.Type명** 으로 선언 가능하다.

> 기본적으로 arry, bool, func, number, object, string 부터 React 타입인 element, 클래스 인스턴스 등 타입 체크가 가능하다.
> 

**App.js**

**상위 컴포넌트에서 name, age, isChecked 속성을 하위 컴포넌트로 전달한다.**

```jsx
<MyComponent name="코딩젤리" age={2} isChecked={false}/>
```


<br>
<br>


**MyComponent.js**

하위 컴포넌트에서 한다.

전달받은 Props의 타입을 체크!

PropType.string, PropType.bool 로 props가 해당 타입인지 체크한다. 

PropType.oneOf(['string','number']) : 해당 Props가 여러 종류 중하나가 될수 있는 타입임을 나타낸다.

전달받은 props가 string, number 중 하나에 해당하면 된다.

```jsx
import React from "react";
import PropType from 'prop-types';
function MyComponent(props) {
    return(
        <div>
            {props.name},{props.age}, {props.isChecked ? "true" : "false"}
        </div>
    );
}

MyComponent.prototype = {
    name : PropType.string,
    age : PropType.oneOf(['string','number']),
    isChecked : PropType.bool
}
export default MyComponent;
```


<br>
<br>


# 클래스형 props

✔️ 클래스형 컴포넌트는 `this.props`로 `props`를 사용할 수 있다. 

✔️  클래스 내에 static으로 defaultProps 객체를 선언하고 기본값을 설정할 수 있다. 

```jsx
class Test extends Component {
    static defaultProps = {
        text: "이것은 기본 텍스트"
    }
    render() {
        return <div>멋진 리액트 컴포넌트 {this.props.text}<br/> 자식 값 {this.props.children}</div>
    }
}

export default Test;
```

props에는 propType 객체를 이용해 컴포넌트에서 사용되는 속성의 타입을 지정할 수 있다. 

타입으로는 배열, 함수, 객체, 숫자 등이 있다. 

<br>

```jsx
class Test extends Component {
    static defaultProps = {
        text: "이것은 기본 텍스트"
    }

    static propType = {
        text: PropTypes.number
    }

    render() {
        return <div>멋진 리액트 컴포넌트 {this.props.text}<br/> 자식 값 {this.props.children}</div>
    }
}

export default Test;
```

속성의 값이 지정된 타입이 아니라면 경고창을 확인 할 수 있다. 


<br>

<br>

**기본 폴더 구조** 

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props3.png?raw=true)

다운 없이 리액트를 실행시킬 수 있는 웹 사이트에서 실행 시켜 보았다. 

폴더 구조는 위 사진처럼 구성되며, `**Fany.js**` 파일은 실습을 위한 파일로 따로 

만들었다.

<br>

**App.js**

```jsx
import React, { Component } from "react";
import "./styles.css";

//Fany.js import. 

class App extends Component {
  render() {
    return <My name="solfany" age="25" />;
  }
}
export default App;
```

Fany.js  import 하여 `**My**`컴포넌트(자식)로 render 해주고 

`**props**`값으로 `**name**` 과 `**age**`를 넣었다.


<br>


**Fany.js**

```jsx
import React, { Component } from "react";

class My extends Component {
  render() {
    return (
      <span>
        이름 : {this.props.name} 나이:{this.props.age}
      </span>
    );
  }
}
export default My;
```

Fany.js 파일을 만들어 My 컴포넌트를 만든다. 


<br>


**Class 컴포넌트에는 render() {} 함수가 꼭 필요하다.** 

그리고 jsx를 return 해줘야한다.

My(자식) 컴포넌트에서 → App(부모) 에서 보내온  → props를 받아 사용한다.



<br>


![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props4.png?raw=true)

브라우저에 보이는 결과

---



<br>
<br>


# state란?


**state는 컴포넌트 자기 자신이 가지고 있는 값이다.** 

props는 읽기 전용이기 때문에 컴포넌트 안에서 변경이 불가능하다. 

따라서 내부에서 변경이 가능한 것이 필요한데 이것이 바로 state속성이다.

state 속성은 props와 달리 내부에서 변경이 가능하다.

state는 클래스형 컴포넌트에서 사용하는 state와 함수형 컴포넌트에서 

useState메서드를 이용하는 state가 있다.

변화가 필요할 경우 setState()함수를 통해 값을 변경해줄 수 있다.



<br>
<br>


# 클래스형 컴포넌트 state

state를 변경하고 싶다면 

setState메서드를 사용해서 state를 변경한다. 

state를 초기값을 선언할 때는 constructor메서드(생성자)에서 객체로 선언하여 사용한다.

```jsx
//test.jsimport React, { Component } from "react";

class Test extends Component {
  constructor(props) {
    super(props);
    this.state = {
      text: "컴포넌트",
    };
  }

  render() {
    return (
      <div>
        <h1>{this.state.text}</h1>
        <button
          onClick={() => {
            this.setState({ text: "변경했어요!" });
          }}
        >
          변경
        </button>
      </div>
    );
  }
}

export default Test;

//app.jsimport Test from './Test';

function App() {
  return <Test></Test>
}

export default App;
```

예제에는 버튼을 클릭하면 setState메서드가 호출되어 state의 text값이 변경된다.

super메서드는 상속받은 클래스의 생성자를 호출하고

하위 클래스에서 생성자를 사용할 때 super를 호출하지 않으면 

객체가 할당되지 않아 에러가 발생한다.⚠️

setState메서드는 비동기로 작업을 처리하며, 

변경점이 있을 때마다 계속 다시 렌더링 하기에는 비용이 많이 들기 때문에 

비동기로 작업을 처리한다. 

그렇기 때문에 바로바로 업데이트가 되지 않을 수 있다.

따라서 여러 개의 setState메서드를 사용하여 최신의 값으로 state값을 사용해야 한다면 

함수를 인수로 넘겨 사용해야 한다.


<br>


```jsx
//test.jsimport React, { Component } from "react";

class Test extends Component {
  constructor(props) {
    super(props);
    this.state = {
      text: "컴포넌트",
    };
  }

  render() {
    return (
      <div>
        <h1>{this.state.text}</h1>
        <button
          onClick={() => {
            this.setState((state, props) => {
                return {
                	text: state.text + " " + props.name + " 이였어요!"
                };
            });
        }}
        >
          변경
        </button>
      </div>
    );
  }
}

export default Test;

//app.jsimport Test from './Test';

function App() {
  return <Test name="aaa"></Test>
}

export default App;
```

이렇게 setState메서드에 첫 번째 인수로 함수를 전달해주면 전달된 함수에서 

최신의 state값과 최신의 props값을 사용할 수 있으므로 여러 

setState의 작업을 수행할 때 순차적으로 값을 변경할 수 있다.

setState메서드의 두 번째 인수로 setState메서드의 작업이 끝났을 때 

호출되는 콜백 함수를 전달할 수 있다!


<br>


```jsx
render() {
    return (
      <div>
        <h1>{this.state.text}</h1>
        <button
          onClick={() => {
            this.setState((state, props) => {
                return {
                    text: state.text + " " + props.name + " 이였어요!"
                };
            },
            () => console.log("변경했어요!!"));
        }}
        >
          변경
        </button>
      </div>
    );
  }
```



<br>
<br>

# 함수형 컴포넌트 state

함수형 컴포넌트에서 state를 변경하고 싶다면 useState메서드를 사용해야 한다.

useState는 Hook에 있는 기능 중 하나이다. 

여기에서는 useState를 간단히 알아보자면 

useState메서드는 반환 값으로 state값과 state를 변경할 수 있는 함수를 반환한다.

<br>


```jsx
const [text, setText] = useState("");
```

useState메서드의 인수로는 state의 초기값이다. 

따라서 위 코드로 보면 text가 초기 state값, setText가 state를 변경해주는 함수이다.

<br>


```jsx
import React, { useState } from 'react';

const Test2 = () => {
    const [text, setText] = useState("");
    const click = () => setText("클릭1");
    const click2 = () => setText("클릭2");

    return (
        <div>
            <button onClick={click}>버튼1</button>
            <button onClick={click2}>버튼2</button>
            <h1>{text}</h1>
        </div>
    )
}

export default Test2;
```

버튼을 클릭하면 setText가 호출되며 text값이 변경되고 다시 렌더링이 된다.

클래스형 컴포넌트와 함수형 컴포넌트에서 state를 변경할 때 

state값을 직접적으로 변경해서는 안된다.

직접적으로 변경해도 값은 변경이 되나 다시 렌더링 되지 않기 때문이다.

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props5.png?raw=true)

[버튼 1] 눌렀을 때

![Untitled](https://github.com/solfany/solfany.github.io/blob/master/blog/props-state-img/props6.png?raw=true)

[버튼 2] 눌렀을 때

<br>
<br>


**State 예제**

app.js

```jsx
import React, { Component } from 'react';
import Counter from './Counter';

class App extends Component {
  render() {
    return <Counter />;
  }
}
export default App;

```

Counter 컴포넌트를 import 하고 render 함


<br>

counter.js

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  };

  handleIncrease = () => {
    this.setState({
      number: this.state.number + 1
    });
  };
  handleDecrease = () => {
    this.setState({
      number: this.state.number - 1
    });
  };
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>Count</h1>
        <h2>값 : {number}</h2>
        <button onClick={this.handleIncrease}>Plus</button>
        <button onClick={this.handleDecrease}>Minus</button>
      </div>
    );
  }
}

export default Counter;

```

**위와 같이 화살표 함수(arrow function)를 사용한 이유는** 

**일반적인 function handleIncrease() {} 사용했을 경우 this가 뭔지 모르게된다.**


<br>


![https://blog.kakaocdn.net/dn/2KIVY/btqDY2LZMy4/ZyYickV6HyIcxJGjd7zyZ1/img.png](https://blog.kakaocdn.net/dn/2KIVY/btqDY2LZMy4/ZyYickV6HyIcxJGjd7zyZ1/img.png)


<br>


해결 방법은 아래와 같다.

```jsx
class Counter extends Component {
  state = {
    number: 0
  };

  constructor(props) {
    super(props);
    this.handleIncrease = this.handleIncrease.bind(this);
  }
  handleIncrease() {
    console.log(this)
    this.setState({
      number: this.state.number + 1
    });
  }
```

![https://blog.kakaocdn.net/dn/oRIaa/btqDUR0blLU/qL6qkiBq0StsHoPczGDi01/img.png](https://blog.kakaocdn.net/dn/oRIaa/btqDUR0blLU/qL6qkiBq0StsHoPczGDi01/img.png)

handleIncrease 메서드 바인딩 후 this 값

<br>


**메서드를 바인딩하거나 state를 초기화하는 작업이 없다면, 굳이 컴포넌트에 생성자를 구현하지 않아도 된다.**

하지만 화살표 함수를 사용하지 않았기 때문에 this를 찾지 못함 이런 경우 생성자를 구현하여 컴포넌트가 마운트 되기 전에 handleIncrease 메서드를 바인딩 해줘야한다.

constructor 는 컴포넌트가 생성될 때마다 자동으로 생성되는 함수로  컴포넌트가 마운트되기 전에 호출된다.

React.Component를 상속한 컴포넌트의 생성자를 구현할 땐 그 안에 super(props)를 호출해야한다. 그렇지 않으면 this.props가 생성자 내에서 정의되지 않아 버그로 이어질 수 있다.

constructor 안에서 this.props에 접근하고 싶을 땐 super(props) 를 부르면 된다.



<br>
<br>




# 정리 💡

> props는 읽기 전용이고 단방향 성질을 가지고 있다,
> 
> 
> 부모 컴포넌트가 자식 컴포넌트에 값을 전달할 때 사용한다
> 
> 따라서 내부에서 변경이 가능한 것이 필요한데 이것이 바로 state속성이다.
> 
> state 속성은 props와 달리 내부에서 변경이 가능하다.
> 
> state는 클래스형 컴포넌트에서 사용하는 state와 함수형 컴포넌트에서
> 
> useState메서드를 이용하는 state가 있다.
> 
> 변화가 필요할 경우 setState()함수를 통해 값을 변경해줄 수 있다.
>
