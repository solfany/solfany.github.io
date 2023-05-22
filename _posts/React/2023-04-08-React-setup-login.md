---
title: "[React] 개발환경 세팅하기"
categories:
  - React
tags: [React, inflearn]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"

---


## 개발환경 세팅 

2023년 4월 8일 


![https://velcdn.com](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https:%2F%2Fblog.kakaocdn.net%2Fdn%2FtvpzA%2FbtraptSGN85%2F5KmvX2kurFktBs9KVL6XNk%2Fimg.png)


## react 설치 방법

**1. [node.js](https://nodejs.org/en, "node.js 홈페이지") 홈페이지 접속 후 프로그램 다운로드**
>좌측 LTS 버전 (안전성)  우측 Current(가장 최신 버전) <br>
나의 경우 최신 버전은 필요없을 것 같아서 안전한  LTS 버전을 사용했다. 
>
<br>

**2. node.js를 다운 받았으면 프로젝트 폴더를 만들기**
그 후 vscode로 이동해서 만든 폴더의 터미널을 열어준 뒤 리액트 라이브러리를 불러올 명령어를 입력한다. (cmd 환경에서도 세팅 가능)

<br>

**3. 리액트 파일 생성 방법**
```jsx
npx create-react-app my-app //(my app)은 프로젝트 폴더명
cd my-app	//c드라이브로 이동
npm start	//다운로드한 파일을 3000포트대로 연다.
```


✔️ 초기생성된 파일에 > App.js 를 들어가면 웹 창에 보여지는 부분을 작성할 수 있도록 되어 있음

  > auto import / ES7 React/Redux/GraphQL/React-Native snippets (vscode 확장팩명)
  > 

✔️  확장 파일을 다운로드 받으면 rfce라는 단축키를 입력하면 자동으로 사용 가능한 기본 파트가 생성된다.

<br>
<br>


## mac os, 맥m1에서의 react 설치 방법

✔️ 기존과 같이 리액트 파일 다운로드 후 vscode 좌측 상단에 있는 버튼을 눌러 터미널을 열고 npx create-react-app [파일 명] 입력 

✔️ 여기서 중요한 점은 파일 우 클릭 후 [통합터미널] 열기가 아닌 vs code내에서 터미널을 열어야 한다. 

> mac os는 window운영 체제와 다른 점이 많아서 개발환경 세팅하는데 고생을 많이 했다 😢
> 

<br>
<br>

## 배포하기

`npm run build` 해당 명령어로 새로운 파일을 만들어 해당 파일로 배포가 가능하다. 

✔️  해당 명령어를 터미널에 입력하면 새로운 파일이 생기는데,  <br>
    해당 파일은 불필요한 파일들을 제외 후 꼭 필요한 문서들만 남겨두어 프로그램이 가벼워진다.


<br>
<br>


## 작업 완료 후 종료 시키는 방법

`ctrl + c` > yes 하면 터미널 작업을 끝냄
`ctrl + c` * 2 = 터미널 작업을 끝냄


<br>
<br>


## tip

✔️  localhost :3000 / [test html] 을 입력하면 파일이 이동한다.  

(test.html은 내가 임의로 정한 파일 명임을 참고)

<br>
<br>

## 정리

> 왠지 라이브 서버에서 작업하는 듯한 재미를 느꼈다.
> 
> 
> 실시간으로 변경되는 모습 보는 것이 흥미로웠고,  
> 
> 프론트와 백의 데이터들이 융합되는 과정이 굉장히 어렵다고 들었지만 
> 
> 앞으로가 기대되는 리액트 인 것 같다. 
>
