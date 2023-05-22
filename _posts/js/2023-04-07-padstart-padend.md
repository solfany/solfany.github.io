---
title: "[JS] padStart,  padEnd"
categories : 
  - JavaScript
tags: [JavaScript, nomadcoders]
author_profile: true
toc_label: "목록"
toc_icon: "bars"
---




## **padStart와 padEnd 사용하기**

2023년 4월 7일 

# PAD

✔️ padStart와 padEnd 함수는 ES8(ES2017)에 새롭게 추가된 기능이다. pad는 좌우에 특정한 문자열로 채우는 기능이다. 좀더 자세히 얘기하면 첫번째 파라미터인 maxLength를 받아 문자열의 길이가 maxLength보다 작을 경우 나머지를 특정한 문자열로 채워주는 기능이다. 이때 두번째 문자열을 넘겨주지 않으면 빈 공백으로 문자열을 채운다.

```jsx
String.prototype.padStart(maxLength, ?fillString);
String.prototype.padEnd(maxLength, ?fillString);
```

## 숫자 앞에 0 붙이기

✔️시계의 초 단위를 표시 할때 01, 02 처럼 숫자 앞에 0을 붙여서 표현한다. 

padStart가 나오기 전에는 이러한 기능을 만들기 위해서 로직을 구현하였지만 이제는 간편하게 작업할 수 있다.

2자리수를 표현하기 위해 padStart(자리수(조건), 조건을 채우지 못하면 대체할 문자)로 사용할 수 있다.

```jsx
const number = 1;  //한자리 수 
const result = String(number).padStrt(2, 0); //두자리 수(조건) 미만이라면 두자리 문자열이 될 때 까지 앞에 0을 붙이겠다.

console.log(result);
// 01 
```

## 아이디를 *로 표시하기

✔️아이디의 앞부분 일부만 표시를 하고 나머지는 *로 표시 하는 기능도 자주 사용하였다. padEnd를 이용하면 간편하게 기능을 구현할 수 있다.

```jsx
const id = '아이디입니다'
const temp = id.slice(0, 3);
const result = temp.padEnd(id.length, '*');

console.log(result);
// 아이디***
```
