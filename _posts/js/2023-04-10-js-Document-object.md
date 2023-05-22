---
title: "[JS] Document의 객체(object) "
categories:
  - JavaScript
tags: [JavaScript, object]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"

---

## **querySelector( )**

querySelector()는 특정 name,id,class를 제한하지 않고 css선택자를 사용하여 요소를 찾는다.

같은 id 또는 class 일 경우 스크립트의 **최상단 요소**만 로직에 포함한다.

```jsx
querySelector(#id) => id 값 id를 가진 요소를 찾습니다.
querySelector(.class) => class 값 class를 가진 요소를 찾습니다.
```

✔️ 인접한 태그들끼리의 상대적인 위치를 비교하여 가져오고 싶다면 **querySelector**를 써야한다.

예시) 1️⃣

```jsx
document.querySelector('ul li.web-class').innerHTML;
```

예시) 2️⃣

```jsx
 document.querySelector('li.web-class').innerHTML;
```

<br>
<br>


## **querySelectorAll( )**

querySelector와 사용 방법은 동일하며 선택자를 선택하여 배열과 비슷한 객체인 

**nodeList**를 반환한다. 

반환객체가 nodeList이기에 **for문** 또는 **forEach문**을 사용한다.

아래 코드와 같이 ","를 사용하면 여러 요소를 한번에 가져올 수 있다.

```jsx
querySelectorAll("#id,.class");
```



<br>
<br>



## **getElementbyId( )**

html에서 해당 아이디를 가진 태그를 선택한다.

```jsx
document.getElementById('app-root');// <div id="app-root" data-reactid="32">...</div>
```


<br>
<br>


## **getElementby..()**

- **document.getElementsByClassName(클래스)**
- **document.getElementsByName(이름)**
- **document.getElementsByTagName(태그)**

html에서 각각 해당 **클래스, 네임, 태그명**을 가진 태그를 선택한다.

여러개 선택되기 때문에 항상 배열이다.

메소드 이름도 Elements이다.

```jsx
document.getElementsByTagName('nav');// [<nav class="pTYnty2zkYzsdEoN1fhmO" data-reactid="8">…</nav>]
```


<br>

<br>



**getElementby..  vs  querySelector 비교 표** 

| getElementby.. | querySelector |
| --- | --- |
| 예시) document.getElementById('web-id').innerHTML; | 예시) document.querySelector('#web-id').innerHTML; |
| 만약에 해당 선택자에 맞는 element가 없다면 null을 반환한다. | 해당 선택자에 맞는 element 목록중에 첫번째를 반환한다. <br> querySelectorAll는 모든 element목록 (= node list)를 반환한다. <br> 해당하는 것이 없다면  null을 반환한다. |
| 처리속도는 getElementBy..가  더  빠르다. |  |
| 리턴값은 HTMLCollection (name, id, index number로 HTMLCollection의 항목(itmes)들에 접근할 수 있다) | 리턴값은 NodeList (index Number로만 NodeList의 항목(items)들에 접근할 수 있다) |

⬇️ **node 와 element의 차이점은 하단의 PS 파트 참고!**


<br>

<br>



## **createElement( )**

**document에 새로운 태그를 만들 때 사용한다.** 

만든다고 바로 생기는 게 아니라 변수를 통해 메모리에 저장된다.

만든 태그를 추가하는 메소드는 따로 있는데 추후에 업데이트 해놓겠다..!

```jsx
var div = document.createElement('div');// 메모리에 div가 생성됨
```



<br>
<br>



## **createTextNode()**

**텍스트도 하나의 요소이다**

텍스트를 따로 만들 수 있다. 여기서 **Node**는 태그와 텍스트를 가리키는 명칭이다.

역시 바로 생기는 게 아니라 변수를 통해 메모리에 저장된다

```jsx
var text = document.createTextNode('텍스트');
```


<br>
<br>



## **createDocumentFragment()**

**가짜 document를 만든다**

💡 중요

자바스크립트로 document의 태그를 조작하는 것은 매우 성능이 떨어지게 되는데. 

특히 여러 태그를 반복문을 통해 동시에 추가할 때 말이다. 

이럴 때 미리 가짜 document를 만들어서 여기에 추가를 한 후, 한 번에 document에 추가한다.

이러면 진짜 document는 한 번만 조작하면 돼서 성능에 부담이 덜하다.

**간단하게 예시를 들어보자면,**

**appendChild** 메소드가 바로 추가하는 코드입니다.

```jsx
var div = document.createElement('div');
var text = document.createTextNode('텍스트');  
var fragment = document.createDocumentFragment();
div.appendChild(text);  
fragment.appendChild(div); 
document.body.appendChild(fragment);
```

div에 text를 담고, body에는 fragment를 담았다.

직접적으로 body에 영향을 주는 것은 fragment를 추가할 때, 단 한 번이다.

만약 appendChild같은 조작을 많이 해야할 경우, 

fragment에다가 한 후에 마지막에 fragment를 추가하면 된다.



<br>
<br>



## **document.head, document.body**

각각 html의 head와 body에 접근할 수 있게 해줍니다.

- document.anchor
- document.links
- document.forms
- document.images
- document.scripts

이름처럼 각각 모든 html anchor, links, forms, images, scripts 접근할 수 있게 해준다


<br>
<br>



## **document.title**

문서의 제목에 접근 가능하다.

바꾸기도 가능하며, 문서의 제목은 바로 탭에 써 있는 글자이다!

```jsx
document.title = '여길 보세요';
```



<br>
<br>


## **PS**

❔ 

엘리먼트(element)와 노드(node)의 정확한 차이가 뭘까?

💡

W3C의 DOM(Document Object Model) 스펙에 따르면,

노드 인터페이스(Node Interface)는 DOM의 가장 기본이 되는 데이터 타입이다.

노드 인터페이스를 구현한 여러 오브젝트가 있으며, 노드 타입으로 구분할 수 있다.

예) 엘리먼트 노드, 텍스트 노드, 속성 노드 등등

정리: node는 element의상위 개념이다..!
