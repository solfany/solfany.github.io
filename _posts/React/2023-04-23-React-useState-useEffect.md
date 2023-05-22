---
title: "[React]useState, useEffect"
categories:
  - React
tags: [React, useState, useEffect]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---




2023년 4월 23일 

<br>

# useState

**Using the State Hook**

*Hook*은 React 16.8버전에 새로 추가되었다. 

 Hook은 클래스 컴포넌트를 작성하지 않아도 state와 같은 특징들을 사용할 수 있다.
 
<br>

아래 예시를 통해 Hook을 배워보도록 하겠다. 

```jsx
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, count라 부르겠습니다.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

아래의 클래스 예시와 비교하며 Hook의 특징에 대해 배워보자

<br>



# Hook과 같은 기능을 하는 클래스 예시

React에서 클래스를 사용해봤다면, 아래의 코드는 익숙할 것이다.

```jsx
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0
        };
    }

    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                    Click me
                </button>
            </div>);
    }
}
```

위 코드에서 state는 `{ count: 0 }`이며 사용자가 `this.setState()`를 호출하는 버튼을 클릭했을 때 `state.count`를 증가시킨다. 

해당 코드로 예시를 들어 설명해보겠다. 

> counter 예시를 사용한 이유는, Hook을 잘 이해할 수 있도록 도와주는 가장 기초적인 내용이 될 수 있기 때문이다.
> 

<br>



# Hook과 함수 컴포넌트

React의 함수 컴포넌트는 이렇게 생겼다.

```jsx
const Example = (props) => {
  // 여기서 Hook을 사용할 수 있다!
  return <div />;
}
```

또는 이렇게 생겼다 !

```jsx
function Example(props) {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}
```

함수 컴포넌트를 “state가 없는 컴포넌트”로 알고 있었을 거다.

하지만 Hook은 React state를 함수 안에서 사용할 수 있게 해준다

Hook은 클래스 안에서 동작하지 않는다**.** 

하지만 클래스를 작성하지 않고 사용할 수 있다.


<br>



# Hook이란?

React의 `useState` Hook을 사용해보자

```jsx
import React, { useState } from 'react';function Example() {
  // ...
}
```

**Hook이란?** Hook은 특별한 함수이다 

예를 들어 `useState`는 state를 함수 컴포넌트 안에서 사용할 수 있게 해준다. 

**언제 Hook을 사용할까?** 

함수 컴포넌트를 사용하던 중 state를 추가하고 싶을 때 클래스 컴포넌트로 바꾸곤 했을 거다. 하지만 이제 함수 컴포넌트 안에서 Hook을 이용하여 state를 사용할 수 있다.


<br>
<br>



# state 변수 선언하기

클래스를 사용할 때, constructor 안에서 `this.state`를 `{ count: 0 }`로 설정함으로써 `count`를 `0`으로 초기화했다.

```jsx
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
    }
}
```

함수 컴포넌트는 `this`를 가질 수 없기 때문에 `this.state`를 할당하거나 읽을 수 없다.

대신, `useState` Hook을 직접 컴포넌트에 호출합니다.

```jsx
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, 이것을 count라 부르겠다. 
const [count, setCount] = useState(0);
```


<br>


**`useState`를 호출하는 것은 무엇을 하는 걸까?**

 바로 “state 변수”를 선언할 수 있다.  

위에 선언한 변수는 `count`라고 부르지만 `banana`처럼 아무 이름으로 지어도 된다. 

`useState`는 클래스 컴포넌트의 `this.state`가 제공하는 기능과 똑같다.

 일반적으로 일반 변수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 사라지지 않는다. 



<br>

**`useState`의 인자로 무엇을 넘겨주어야 할까?**

 `useState()`Hook의 인자로 넘겨주는 값은 state의 초기 값이다.

함수 컴포넌트의 state는 클래스와 달리 객체일 필요는 없고, 숫자 타입과 문자 타입을 가질 수 있습니다. 위의 예시는 사용자가 버튼을 얼마나 많이 클릭했는지 알기를 원하므로 `0`을 해당 state의 초기 값으로 선언했다. 

(2개의 다른 변수를 저장하기를 원한다면 `useState()`를 두 번 호출해야 한다. )


<br>


**`useState`는 무엇을 반환할까?**

 state 변수, 해당 변수를 갱신할 수 있는 함수 이 두 가지 쌍을 반환한다.  

이것이 바로 `const [count, setCount] = useState()`라고 쓰는 이유이다. 

클래스 컴포넌트의 `this.state.count`와 `this.setState`와 유사히다.

 

이제 useState를 이용하여 많은 것을 만들 수 있다.

```jsx
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, 이것을 count라 부르겠습니다.  const [count, setCount] = useState(0);
```

count라고 부르는 state 변수를 선언하고 0으로 초기화한다. 

React는 해당 변수를 리렌더링할 때 기억하고, 가장 최근에 갱신된 값을 제공한다. 

count 변수의 값을 갱신하려면 setCount를 호출하면 된다.

<br>

> 주의
> 
> 
> 왜 `createState`가 아닌, `useState`로 이름을 지었을까?
> 
> 컴포넌트가 렌더링할 때 오직 한 번만 생성되기 때문에 “Create”라는 이름은 꽤 정확하지 않을 수 있다.
> 
>  컴포넌트가 다음 렌더링을 하는 동안 `useState`는 현재 state를 준다.
> 
>  Hook 이름이 항상 `use`로 시작하는 이유도 있습니다. 
> 

<br>
<br>

# state 가져오기

클래스 컴포넌트는 count를 보여주기 위해 this.state.count를 사용한다. 

```jsx
  <p>You clicked {this.state.count} times</p>
```

반면 함수 컴포넌트는 `count`를 직접 사용할 수 있다. 

```jsx
  <p>You clicked {count} times</p>
```

<br>
<br>

# state 갱신하기

클래스 컴포넌트는 `count`를 갱신하기 위해 `this.setState()`를 호출합니다.

```jsx
  <button onClick={() => this.setState({ count: this.state.count + 1 })}>    
		Click me
  </button>
```

반면 함수 컴포넌트는 `setCount`와 `count` 변수를 가지고 있으므로 `this`를 호출하지 않아도 된다.

```jsx
  <button onClick={() => setCount(count + 1)}>    
		Click me
  </button>
```

<br>
<br>


# 요약

**아래 코드를 한 줄 한 줄 살펴보고**, 얼마나 이해했는지 체크해봅시다.

```jsx
import React, { useState } from "react";
// Hook 을 React에서 가져온다 
function Example() {
  const [count, setCount] = useState(0);
// useState Hook 을 이용하면 state와 state를 갱신할 수 있는 함수가 만들어진다. 
// 그리고 useState 의 인자 값으로 0을 넘겨주면 count 값을 0으로 초기화 할 수 있다. 
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
// 사용자가 버튼을 클릭하면 setCount함수를 호출하여 state변수를 갱신한다. 
react는 새로운 count변수를 Exaple 컴포넌트에 넘기며 해당 component를 리렌더링 한다.
    </div>
  );
}
```

위의 주석을 통해 useState의 흐름을 기재해두었다.

<br>
<br>

# 팁: 대괄호가 의미하는 것은 무엇일까?

대괄호를 이용하여 state 변수를 선언하는 것을 보았을 것이다. 

```jsx
  const [count, setCount] = useState(0);
```

대괄호 왼쪽의 state 변수는 사용하고 싶은 이름으로 선언할 수 있습니다.

```jsx
  const [fruit, setFruit] = useState('banana');
```

위 자바스크립트 문법은 “배열 구조 분해”라고 하고, 

`fruit`과 `setFruit`, 총 2개의 값을 만들고 있다.  

즉, `useState`를 사용하면 `fruit`이라는 첫 번째 값과 `setFruit`라는 두 번째 값을 반환한다.  

아래의 코드와 같은 효과를 낼 수 있다.

```jsx
  var fruitStateVariable = useState('banana'); // 두 개의 아이템이 있는 쌍을 반환
  var fruit = fruitStateVariable[0]; // 첫 번째 아이템
  var setFruit = fruitStateVariable[1]; // 두 번째 아이템
```

`useState`를 이용하여 변수를 선언하면 2개의 아이템 쌍이 들어있는 배열로 만들어진다. 

첫 번째 아이템은 현재 변수를 의미하고, 두 번째 아이템은 해당 변수를 갱신해주는 함수이다. 

배열 구조 분해라는 특별한 방법으로 변수를 선언해주었기 때문에 

`[0]`이나 `[1]`로 배열에 접근하는 것은 좋지 않을 수 있다. 



<br>
<br>


# 팁: 여러 개의 state 변수를 사용하기

`[something, setSomething]`의 쌍처럼 state 변수를 선언하는 것은 유용합니다. 왜냐하면 여러 개의 변수를 선언할 때 각각 다른 이름을 줄 수 있기 때문입니다.

```jsx
function ExampleWithManyStates() {
  // 여러 개의 state를 선언할 수 있습니다!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
```

위의 코드는 `age`, `fruit`, `todos`라는 지역 변수를 가지며 개별적으로 갱신할 수 있다.

```jsx
  function handleOrangeClick() {
    // this.setState({ fruit: 'orange' })와 같은 효과를 냅니다.
    setFruit('orange');
  }
```

여러 개의 state 변수를 **사용하지 않아도 됩니다.** state 변수는 객체와 배열을 잘 가지고 있을 수 있으므로 서로 연관있는 데이터를 묶을 수 있다.

하지만 클래스 컴포넌트의 `this.setState`와 달리 

state를 갱신하는 것은 병합하는 것이 아니라 *대체*하는 것이다.



<br>
<br>

# useEffect

**Using the Effect Hook**

*Hooks*는 React 16.8버전에 새로 추가되었다. 

Hook은 클래스 컴포넌트를 작성하지 않아도 state와 같은 특징들을 사용할 수 있다.

*Effect Hook*을 사용하면 함수 컴포넌트에서 side effect를 수행할 수 있습니다.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount, componentDidUpdate와 같은 방식으로
  useEffect(() => {
    // 브라우저 API를 이용하여 문서 타이틀을 업데이트합니다.
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

데이터 가져오기, 구독(subscription) 설정하기, 수동으로 React 컴포넌트의 DOM을 수정하는 것까지 이 모든 것이 side effects이다.

 이런 기능들(operations)을 side effect(혹은 effect)라 부르는 것이 익숙하지 않을 수도 있지만, 

아마도 이전에 만들었던 컴포넌트에서 위의 기능들을 구현해보았을 것이다.

React 컴포넌트에는 일반적으로 두 종류의 side effects가 있다. 

정리(clean-up)가 필요한 것과 그렇지 않은 것. 이 둘을 어떻게 구분해야 할지 자세하게 알아보자.

<br>
<br>

# 정리(Clean-up)를 이용하지 않는 Effects

**React가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있다.** 

네트워크 리퀘스트, DOM 수동 조작, 로깅 등은 정리(clean-up)가 필요 없는 경우들입니다. 이러한 예들은 실행 이후 신경 쓸 것이 없기 때문이다. 

class와 hook이 이러한 side effects를 어떻게 다르게 구현하는지 비교해보자.



<br>
<br>


**Class를 사용하는 예시**

React의 class 컴포넌트에서 `render` 메서드 그 자체는 side effect를 발생시키지 않는다.

이때는 아직 이른 시기로서 이러한 effect를 수행하는 것은 React가 DOM을 업데이트하고 난 *이후이다*.

React class에서 side effect를 

`componentDidMount`와 `componentDidUpdate`에 두는 것이 바로 이 때문이다. 

예시로 돌아와서 React가 DOM을 바꾸고 난 뒤 문서 타이틀을 업데이트하는 React counter 클래스 컴포넌트를 보자

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }
  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

이제 `useEffect` Hook에서 같은 기능을 어떻게 구현하는지 보겠다.



<br>
<br>


**Hook을 이용하는 예시**

아래의 코드는 위에서 이미 보았던 것이지만 이번에는 좀 더 자세히 살펴보겠습니다.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```


<br>
<br>

**`useEffect`가 하는 일은 무엇일까?**

useEffect Hook을 이용하여 우리는 React에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야하는 지를 말한다. React는 우리가 넘긴 함수를 기억했다가(이 함수를 ‘effect’라고 부릅니다) DOM 업데이트를 수행한 이후에 불러낼 것이다.  위의 경우에는 effect를 통해 문서 타이틀을 지정하지만, 이 외에도 데이터를 가져오거나 다른 명령형(imperative) API를 불러내는 일도 할 수 있다.


<br>
<br>


**`useEffect`를 컴포넌트 안에서 불러내는 이유는 무엇일까?**

 `useEffect`를 컴포넌트 내부에 둠으로써 effect를 통해 `count` state 변수(또는 그 어떤 prop에도)에 접근할 수 있게 된다.  함수 범위 안에 존재하기 때문에 특별한 API 없이도 값을 얻을 수 있다.

Hook은 자바스크립트의 클로저를 이용하여 React에 한정된 API를 고안하는 것보다 자바스크립트가 이미 가지고 있는 방법을 이용하여 문제를 해결한다.


<br>
<br>


**`useEffect`는 렌더링 이후에 매번 수행되는 걸까?** 

네, 기본적으로 첫번째 렌더링*과* 이후의 모든 업데이트에서 수행된다.

 마운팅과 업데이트라는 방식으로 생각하는 대신 effect를 렌더링 이후에 발생하는 것으로 생각하는 것이 더 쉬울 것이다.  React는 effect가 수행되는 시점에 이미 DOM이 업데이트되었음을 보장한다. 


<br>
<br>

**상세한 설명**

effect에 대해 좀 더 알아보았으니 아래의 코드들을 더 쉽게 이해할 수 있을 것입니다.

```jsx
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
}
```

`count` state 변수를 선언한 뒤 React에게 effect를 사용함을 말하고 있다. 

`useEffect` Hook에 함수를 전달하고 있는데 이 함수가 바로 effect입니다. 

이 effect 내부에서 `document.title`이라는 브라우저 API를 이용하여 문서 타이틀을 지정한다.

같은 함수 내부에 있기 때문에 최신의 `count`를 바로 얻을 수 있다.

컴포넌트를 렌더링할 때 React는 우리가 이용한 effect를 기억하였다가 DOM을 업데이트한 이후에 실행한다. 

이는 맨 첫 번째 렌더링은 물론 그 이후의 모든 렌더링에 똑같이 적용된다.

숙련된 자바스크립트 개발자라면 `useEffect`에 전달된 함수가 모든 렌더링에서 다르다는 것을 알아챘을지도 모른다.

이는 의도된 것으로서, `count` 값이 제대로 업데이트 되는지에 대한 걱정 없이 effect 내부에서 그 값을 읽을 수 있게 하는 부분이기도 하다. 

리렌더링하는 때마다 모두 이전과 *다른* effect로 교체하여 전달한다.

 이 점이 렌더링의 결과의 한 부분이 되게 만드는 점인데, 각각의 effect는 특정한 렌더링에 속한다.

> 팁
> 
> 
> `componentDidMount` 혹은 `componentDidUpdate`와는 달리 `useEffect`에서 사용되는 effect는 브라우저가 화면을 업데이트하는 것을 차단하지 않는다. 이를 통해 애플리케이션의 반응성을 향상해준다. 대부분의 effect는 동기적으로 실행될 필요가 없다. 흔하지는 않지만 (레이아웃의 측정과 같은) 동기적 실행이 필요한 경우에는 `useEffect`와 동일한 API를 사용하는 `[useLayoutEffect](https://ko.reactjs.org/docs/hooks-reference.html#uselayouteffect)`라는 별도의 Hook이 존재한다.
> 

<br>
<br>


# 정리(clean-up)를 이용하는 Effects

위에서 정리(clean-up)가 필요하지 않은 side effect를 보았지만, 정리(clean-up)가 필요한 effect도 있다. 외부 데이터에 **구독(subscription)을 설정해야 하는 경우**를 생각해보겠다. 이런 경우에 메모리 누수가 발생하지 않도록 정리(clean-up)하는 것은 매우 중요하다. class와 Hook을 사용하는 두 경우를 비교해보겠다.



<br>
<br>


**Class를 사용하는 예시**


React class에서는 흔히 `componentDidMount`에 구독(subscription)을 설정한 뒤 `componentWillUnmount`에서 이를 정리(clean-up)한다.

친구의 온라인 상태를 구독할 수 있는 ChatAPI 모듈의 예를 들어보겠다. 

다음은 class를 이용하여 상태를 구독(subscribe)하고 보여주는 코드이다.

```jsx
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

`componentDidMount`와 `componentWillUnmount`가 어떻게 대칭을 이루고 있는지를 보자

두 개의 메서드 내에 개념상 똑같은 effect에 대한 코드가 있음에도 불구하고 

생명주기 메서드는 이를 분리하게 만든다.


<br>
<br>

**Hook을 이용하는 예시**

이제 이 컴포넌트를 Hook을 이용하여 구현해봅시다.

정리(clean-up)의 실행을 위해 별개의 effect가 필요하다고 생각할 수도 있다. 

하지만 구독(subscription)의 추가와 제거를 위한 코드는 결합도가 높기 때문에 useEffect는 이를 함께 다루도록 고안되었다. 

effect가 함수를 반환하면 React는 그 함수를 정리가 필요한 때에 실행시킬 것이다.

```jsx
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // effect 이후에 어떻게 정리(clean-up)할 것인지 표시합니다.
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

<br>
<br>

**effect에서 함수를 반환하는 이유는 무엇일까?** 

이는 effect를 위한 추가적인 정리(clean-up) 메커니즘이다.

모든 effect는 정리를 위한 함수를 반환할 수 있다. 

이 점이 구독(subscription)의 추가와 제거를 위한 로직을 가까이 묶어둘 수 있게 한다. 

구독(subscription)의 추가와 제거가 모두 하나의 effect를 구성하는 것이다.


<br>
<br>

**React가 effect를 정리(clean-up)하는 시점은 정확히 언제일까?** 

React는 컴포넌트가 마운트 해제되는 때에 정리(clean-up)를 실행한다. 

하지만 위의 예시에서 보았듯이 effect는 한번이 아니라 렌더링이 실행되는 때마다 실행됩니다. 

React가 다음 차례의 effect를 실행하기 전에 이전의 렌더링에서 파생된 effect 또한 정리하는 이유가 바로 이 때문이다. 

> 주의
> 
> 
> effect에서 반드시 유명함수(named function)를 반환해야 하는 것은 아니다.. 목적을 분명히 하기 위해 `정리(clean-up)`라고 부르고 있지만 화살표 함수를 반환하거나 다른 이름으로 불러도 무방하다.
> 



<br>
<br>

# 요약

`useEffect`가 컴포넌트의 렌더링 이후에 다양한 side effects를 표현할 수 있음을 위에서 배웠다.

effect에 정리(clean-up)가 필요한 경우에는 함수를 반환한다.

```jsx
useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

정리(clean-up)가 필요없는 경우에는 어떤 것도 반환하지 않는다.

```
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

이처럼 effect Hook은 두 가지 경우를 한 개의 API로 통합한다.

---


<br>
<br>

# 정리

useState, useEffect란

state는 렌더링을 일으킬 수 있는 변수이다. setState는 state의 값을 변경할 때 사용하는 함수이다. 

useState는 state의 초기값을 정할 수 있고, return 값으로 state, setState를 돌려주는 hook이다.

setState 함수 사용 시 이전 state 값을 사용하고 싶으면 prevState를 이용하면 된다.

 useEffect는 **리액트에서 기본적으로 제공해주는 함수**
로써, useEffect함수가 포함된 컴포넌트가 처음 마운트되거나 컴포넌트가 리렌더링 될 때, 또는 선언된 변수의 값이 변경되거나 redux store의 값이 변경될 때 실행할 구문들을 정의해놓은 함수이다.
