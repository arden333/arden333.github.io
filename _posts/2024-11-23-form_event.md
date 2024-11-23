---
layout: single
title: "[JS] form 이벤트와 preventDefault"
categories: "JavaScript"
tags: ["form 이벤트", "Javascript"]

toc: true
toc_sticky: true
---

## form event
일반적으로 form은 action 속성에 지정된 주소로 form을 제출하고, 그 페이지로 이동하도록 되어있다. 그것이 기본값(default)이다.

<br/>
```html
<form action="/shelter" id="shelter">

<input type="text"></input>
<button>submit></button>

</form>
```
위의 form은 제출 버튼을 누르는 순간 '/shelter'주소로 보내지며, 페이지 또한 '/shelter'로 이동한다. 
<br/> 

## preventDefault 메서드
싱글 페이지로 앱을 구성하는 경우라면 페이지가 이동되어서는 안 된다. form을 제출하고 난 뒤에도 페이지의 이동 없이 한 페이지 내에 사용자가 머물러야 한다.
이렇게 만드려면 form의 default값이 발동하지 않도록 막아야 한다. 이 때, preventDefault 메서드를 사용하면 된다.

<br/>
```javascript
const form = document.querySelector('#shelter')

form.addEventListener = ('submit', function(e) {
  e.preventDefault();
}
```
