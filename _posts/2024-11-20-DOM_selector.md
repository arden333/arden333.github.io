---
layout: single
title: "DOM과 selector"
categories: "JavaScript"
tags: ["DOM", "Selector", "Javascript"]

toc: true
toc_sticky: true
---
 
## DOM
DOM(Document Object Model, 문서객체모델)은 웹페이지를 구성하는 javascript 객체들의 집합이다. 
하나의 페이지를 만들면 자동으로 생성되며, 페이지의 콘텐츠를 나타내는 객체 모음집과 같다. 

```javascript

//HTML의 document 조회
documnet

//javascript 객체만 있는 document 조회
console.dir(document)
```

<img width="1003" alt="스크린샷 2024-11-20 오전 11 01 56" src="https://github.com/user-attachments/assets/593af791-fbc6-4ff1-aa29-514de4b4fc29">


## Selecting
### getElementId, getElementsTagName, getElementsClassName
이름에서 알 수 있듯이 id, tag name, class name으로 특성 요소를 찾아 반환하는 기능을 한다. 
주의할 것은 tag name과 class name은 복수의 값을 찾기 때문에 element's', s가 붙는다. 

```javascript
document.getElementId('name')

document.getElementsTagName('p')
//HTMLCollection(개수) 
```

   <br/>
### querySelector
자바스크립트 DOM에 비교적 새롭게 추가된 메서드로 훨씬 유용하다. 이 querySelector를 이용해서 id, tag name, class namedms 물론, CSS 스타일, 속성 등 원하는
요소를 선택할 수 있다. 

```javascript
document.querySelector('p') //처음에 일치하는 1개만 반환
document.querySelectorAll('p') //일치하는 요소 모두 반환

document.querySelctor(#name) //id가 있다면 '#id명'형태로 입력

document.querySelector('.class') //class명을 입력하려면 '.class명'으로 입력
```

   <br/>
querySelector로 선택한 후 텍스트 내용을 수정하고 싶다면 innerText, textContent, innerHTML 메서드를 사용하면 된다.

```html
<h1> Pickles are <span>delicious</span></h1>
```
이 H1의 내용 중 delicious를 disgusting으로 자바스크립트를 이용해 바꿔보자. 
```javascript
document.querySelector('span').innerText = 'disgusting'
```

   <br/>
innerText, textContent, innerHTML의 차이점을 간략히 정리하자면 다음과 같다.
   
<li> <b>innerText</b>: element 속성으로 사용자에게 보여지는 내용을 수정한다. html 코드에서 style=display:none을 하면 해당 내용이 숨겨진다.</li>
<li> <b>textContext</b>: node 속성이며, style 태그와 상관없이 모든 내용이 보여진다. vs code를 통해 코드를 작성했다면 프로그램 내의 줄바꿈, 띄어쓰기까지 표시된다.</li>
<li> <b>innerHTML</b>: html 태그를 읽고 수정할 수 있다. 수정내용을 "< i >abc< /i >"로 설정할 경우 innerText는 그대로 '< i >abc< /i >'를 반환하지만 innerHTML은 기울임체가 적용된 <i>abc</i>가 출력된다.</li>
