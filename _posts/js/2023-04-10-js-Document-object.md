---
title: "[JS] DOM 요소 선택과 생성"
categories:
  - JavaScript
tags: [JavaScript, object]
---

## querySelector(): 첫 번째 요소 선택

CSS 선택자에 일치하는 첫 번째 요소를 반환한다. 일치하는 요소가 없으면 `null`을 반환한다.

```javascript
const byId = document.querySelector('#app-root');
const byClass = document.querySelector('.web-class');
const nested = document.querySelector('ul li.web-class');
```

## querySelectorAll(): 여러 요소 선택

선택자에 일치하는 요소를 정적인 `NodeList`로 반환한다. 선택 이후 DOM이 바뀌어도 이 목록은 자동으로 갱신되지 않는다. 결과가 없으면 빈 `NodeList`다.

```javascript
const elements = document.querySelectorAll('#app-root, .web-class');
elements.forEach((element) => {
  console.log(element.textContent);
});
```

## getElementById(): ID로 선택

ID에 해당하는 요소 하나를 반환하며, 없으면 `null`을 반환한다. 메서드 이름은 대소문자를 구분한다.

```javascript
const root = document.getElementById('app-root');
```

## 여러 요소를 반환하는 메서드

| 메서드 | 선택 기준 | 반환값 |
| --- | --- | --- |
| `getElementsByClassName()` | 클래스 이름 | 동적인 `HTMLCollection` |
| `getElementsByTagName()` | 태그 이름 | 동적인 `HTMLCollection` |
| `getElementsByName()` | `name` 속성 | 동적인 `NodeList` |
| `querySelectorAll()` | CSS 선택자 | 정적인 `NodeList` |

이 목록들은 배열 자체가 아니다. 배열 메서드가 필요하면 `Array.from()`으로 변환할 수 있다.

```javascript
const paragraphs = Array.from(document.getElementsByTagName('p'));
```

## 요소와 텍스트 노드 생성

`createElement()`는 요소를, `createTextNode()`는 텍스트 노드를 생성한다. 생성한 노드는 `appendChild()` 등으로 문서에 추가해야 화면에 나타난다.

```javascript
const div = document.createElement('div');
const text = document.createTextNode('개발 기록');
div.appendChild(text);
document.body.appendChild(div);
```

## DocumentFragment

`DocumentFragment`는 여러 노드를 임시로 모아 두는 문서 조각이다. 문서에 추가할 때는 조각 자체가 아니라 그 안의 자식 노드들이 삽입된다.

```javascript
const fragment = document.createDocumentFragment();
const div = document.createElement('div');
div.textContent = '개발 기록';
fragment.appendChild(div);
document.body.appendChild(fragment);
```

## 문서 정보 접근

- `document.head`, `document.body`: 문서의 `head`, `body` 요소
- `document.links`, `document.forms`, `document.images`, `document.scripts`: 문서에 포함된 해당 요소들의 목록
- `document.title`: 브라우저 탭에 표시되는 문서 제목

```javascript
document.title = '개발 기록';
```

## 노드와 요소의 차이

노드(Node)는 DOM의 기본 단위다. 요소(Element)는 노드의 한 종류이며, 텍스트와 주석도 각각 노드다.

## 참고

- [MDN: querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [MDN: getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [MDN: getElementsByName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName)
