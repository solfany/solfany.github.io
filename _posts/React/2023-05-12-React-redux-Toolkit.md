---
title: "[React]Redux Toolkit"
categories:
  - React
tags: [React, Redux]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---
  
  

# 다운로드

```jsx
npm install @reduxjs/toolkit
```
 <br>
  
```jsx
import { configureStore } from '@reduxjs/toolkit';
import { counterReducer } from './reducer';
export const store = configureStore({ reducer: counterReducer });
```
 <br>
   
   
> `@reduxjs/toolkit은 Redux`의 공식 도구 모음으로,
Redux 애플리케이션 개발을 더 쉽고 효율적으로 만들기 위해 고안되었다고 한다.
> 
   
   
툴킷은 일반적인 Redux 사용 사례를 단순화하고, 상용구 코드를 줄이며,
더 간결한 코드를 작성할 수 있도록 도와준다.
 <br>
 <br>

# Redux Toolkit이란?[](https://ko.redux.js.org/redux-toolkit/overview/#redux-toolkit%EC%9D%B4-%EB%AD%90%EC%A3%A0)

**[Redux Toolkit](https://redux-toolkit.js.org/)**은 효율적인 Redux 개발을 위한 저희의 견해를 반영한,     

이것만으로도 작동하는 도구 모음이다. 

Redux Toolkit은 Redux 로직을 작성하기 위한 표준 방식이 되도록 만들어졌다.

이 안에는 저장소 준비, 리듀서 정의, 불변 업데이트 로직, 액션 생산자나 액션 타입을 직접 작성하지 않고도 전체 상태 "조각"을 만들어내는 기능까지 대부분의 Redux 사용 방법에 해당하는 유틸리티 함수들이 들어 있다.

거기다가 비동기 로직을 위한 Redux Thunk와 셀렉터 작성을 위한 Reselect 등의 널리 사용되는 애드온을 포함하고 있어 이들을 제대로 사용할 수 있게 해준다.

 <br>
 <br>

# 설치[](https://ko.redux.js.org/redux-toolkit/overview/#%EC%84%A4%EC%B9%98)

Redux Toolkit은 NPM 패키지로 번들러나 Node 앱에서 사용할 수 있다.

```
# NPM
npm install @reduxjs/toolkit

# Yarn
yarn add @reduxjs/toolkit

```

터미널에 해당 명령어 입력 후 다운로드 

 <br>

**코드 상단에 import 하기**

```jsx
import { configureStore } from '@reduxjs/toolkit';

import { counterReducer } from './reducer';
```

 <br>
 <br>

# 목적[](https://ko.redux.js.org/redux-toolkit/overview/#%EB%AA%A9%EC%A0%81)

Redux 코어 라이브러리는 의도적으로 특정한 방향을 배제하고 만들어졌다.

이를 통해 저장소 준비나 상태 보관, 리듀서 작성과 같은 모든 것들을 우리들이 결정 지을 수 있다.

이렇게 융통성을 주는 것은 어떤 경우에는 좋지만, 항상 필요한 것은 아니다.

쓸만한 기본 동작을 가져다가 바로 쓸 수 있는 간단한 방법이 있으면 좋을 때도 있기 마련이다. 

아니면 커다란 애플리케이션을 만들다 보니 비슷한 코드를 계속 작성하게 되었고, 직접 쓰는 양을 줄이고 싶을 수도 있다.

 <br>

💡 **Redux Toolkit**은 Redux에 대해 흔히 우려하는 세 가지를 해결하기 위해 만들어졌다.

- "저장소를 설정하는 것이 너무 복잡하다"
- "쓸만하게 되려면 너무 많은 패키지들을 더 설치해야 한다"
- "보일러플레이트 코드를 너무 많이 필요로 한다"

모든 경우를 해결할 수야 없지만, [create-react-app](https://github.com/facebook/create-react-app)와 [apollo-boost](https://www.apollographql.com/blog/announcement/frontend/zero-config-graphql-state-management/)처럼 대부분의 경우를 다뤄주고 내려야 하는 결정을 줄여주는 공식 도구를 제공하기로 했다.

 <br>
 <br>


# 왜 Redux Toolkit을 사용해야 할까?[](https://ko.redux.js.org/redux-toolkit/overview/#%EC%99%9C-redux-toolkit%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%98%EB%82%98%EC%9A%94)

**Redux Toolkit**은 저희가 추천하는 모범 사례를 통해 기본 동작을 제공하고, 실수를 줄여주고, 더 간단한 코드를 작성하게 해 준다.

이를 통해 좋은 Redux 앱을 쉽고 빠르게 개발할 수 있게 도와준다.

경험이나 기술 수준과 상관 없이 Redux Toolkit은 **모든 Redux 사용자에게 도움이 되며,**

새 프로젝트를 시작할 때 함께해도 되고, 기존 프로젝트를 점차 옮겨가도 된다.
 <br>

물론  **Redux를 사용하기 위해 Redux Toolkit이 *필수적인* 것은 아니다**. 

다른 Redux를 감싸주는 라이브러리를 사용했거나, 모든 로직을 "손수" 작성한 앱들도 많이 있다. 
다른 방식으로 하고 싶으면 해도 상관 없다.

하지만, **[모든 Redux 앱에 Redux Toolkit을 사용하기를 *강력히* 권장](https://ko.redux.js.org/style-guide/#use-redux-toolkit-for-writing-redux-logic)한다고 한다.**

결론적으로 새 프로젝트에 Redux를 처음 사용하려는 사용자이든, 기존 앱을 더 간단하게 만드려는 경험자이든, **Redux Toolkit 사용은 여러분의 코드를 더 좋고 유지보수하기 쉽게 만들어준다고 한다.** 
 <br>
 <br>

# 포함된 것들[](https://ko.redux.js.org/redux-toolkit/overview/#%ED%8F%AC%ED%95%A8%EB%90%9C-%EA%B2%83%EB%93%A4)

Redux Toolkit에 포함된 것들은:

- `[configureStore()](https://redux-toolkit.js.org/api/configureStore)`: `createStore`를 감싸서 쓸만한 기본값들과 단순화된 설정을 제공.
    
    사용자의 리듀서 조각들을 자동으로 합쳐주고, 기본 제공되는 `redux-thunk`를 포함해서 사용자가 지정한 미들웨어들을 더해주고, Redux DevTools 확장을 사용할 수 있게 한다.
    

- `[createReducer()](https://redux-toolkit.js.org/api/createReducer)`: switch 문을 작성하는 대신, 액션 타입과 리듀서 함수를 연결해주는 목록을 작성하도록 한다. 여기에 더해 `[immer` 라이브러리](https://github.com/immerjs/immer)를 자동으로 사용해서, `state.todos[3].completed = true`와 같은 변이 코드를 통해 간편하게 불변 업데이트를 할 수 있도록 한다.
- `[createAction()](https://redux-toolkit.js.org/api/createAction)`: 주어진 액션 타입 문자열을 이용해 액션 생산자 함수를 만들어준다. 함수 자체에 `toString()` 정의가 포함되어 있어서, 타입 상수가 필요한 곳에 사용할 수 있다.
- `[createSlice()](https://redux-toolkit.js.org/api/createSlice)`: 조각 이름과 상태 초기값, 리듀서 함수들로 이루어진 객체를 받아 그에 맞는 액션 생산자와 액션 타입을 포함하는 리듀서 조각을 자동으로 만들어준다.
- `[createAsyncThunk](https://redux-toolkit.js.org/api/createAsyncThunk)`: 액션 타입 문자열과 프로미스를 반환하는 함수를 받아, `pending/fulfilled/rejected` 액션 타입을 디스패치해주는 thunk를 생성해준다.
- `[createEntityAdapter](https://redux-toolkit.js.org/api/createEntityAdapter)`: 저장소 내에 정규화된 데이터를 다루기 위한 리듀서와 셀렉터를 만들어준다.
- `[createSelector` 유틸리티](https://redux-toolkit.js.org/api/createSelector)를 [Reselect](https://github.com/reduxjs/reselect) 라이브러리에서 다시 익스포트해서 쓰기 쉽게 해줍니다.

Redux Toolkit에는 새로운 **[RTK Query 데이터 패치 API](https://redux-toolkit.js.org/rtk-query/overview)**도 포함되어 있습니다. RTK Query는 Redux에서 데이터를 가져오고 캐싱하기 위한 강력한 도구이다. 이 API는 웹 애플리케이션에서 데이터를 불러오는 일반적인 경우에 패치와 캐시 로직을 직접 작성해야 할 필요를 없애준다

 <br>
 <br>

# 주요기능

@reduxjs/toolkit의 주요 기능은 다음과 같다.

`**configureStore`: Redux 스토어를 설정하고 생성하는 함수이다.**
이 함수는 여러 `middleware`를 자동으로 설정하고,
개발 모드에서 `Redux DevTools`와 함께 작동한다.

`**createSlice`: 리듀서와 액션을 동시에 생성하는 함수이다.** 
이 함수는 액션 타입과 리듀서 로직을 결합하여 코드를 줄이고 관리가 쉬운 구조를 만들어 준다.

`**createAction`: 액션 생성자를 만드는 함수이다.**
이 함수를 사용하면 액션 타입과 payload를 자동으로 생성할 수 있다.

`**createReducer`: 리듀서를 만드는 함수이다.**
이 함수는 Immer 라이브러리를 사용하여 불변성을 처리하기 쉽게 해주고,
리듀서 코드를 더 간결하게 만들어 준다.

`**createAsyncThunk`: 비동기 작업을 처리하는 Thunk 함수를 생성하는 함수이다.**
이 함수는 요청 상태(pending, fulfilled, rejected)에 따른 액션을 자동으로 발행한다.

# 장점

**@reduxjs/toolkit**을 사용하면,
Redux 애플리케이션 개발에 필요한 상용구 코드를 대폭 줄이고,
코드 가독성과 유지 관리를 개선할 수 있다.
이 툴킷은 현재 Redux 개발의 기본이 되며, 공식 문서에서도 권장된다.
 <br>
 <br>

# 문서[](https://ko.redux.js.org/redux-toolkit/overview/#%EB%AC%B8%EC%84%9C)

Redux Toolkit의 문서는 **[https://redux-toolkit.js.org](https://redux-toolkit.js.org/)**에서 확인할수 있다

