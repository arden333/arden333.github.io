---
layout: single
title: "[JS] 요소(element) 추가, 삭제하기"
categories: "JavaScript"
tags: ["append", "remove", "Javascript"]

toc: true
toc_sticky: true
---

createElement, append, appendChild, prepend, remove, removeChild 메서드를 이용해서 요소를 삽입하고 삭제하는 방법을 정리한다.

<br/>
## 새로운 요소(element) 만들기
새로운 이미지를 만들어보자. 새로운 요소를 만들 때에는 태그이름을 인수로 전달해야 한다.

```javascript
const img = document.createElement('img')
```
이러면 페이지에는 아무것도 보이지 않는다. 빈 이미지가 생성되었기 때문이다. 이미지가 있는 주소(소스)를 추가해줘야 한다. 임의의 주소를 추가해보았다.

```javascript
img.src = 'http://abc.com'
```
실제 이미지가 있는 웹페이지 주소를 입력해도 이미지는 여전히 화면에 나타나지 않는다. 이미지가 웹페이지의 어느 부분에 삽입될지 지정해주지 않았기 때문이다. 


## 삽입하기
새롭게 만든 요소를 웹페이지에 추가하는 방법은 2가지가 있다. append 또는 appendChild 메서드를 사용하는 방법이다.  
<br/>
### appendChild()
body에 이미지를 넣는다고 해보자.
```javascript
document.body.appendChild(img)
```
img 요소는 body의 가장 마지막 자식 요소로 추가된다. 

<br/>
### append()와 prepend()
append는 여러 개의 요소를 마지막에 추가할 수 있고 appendChild보다 좀 더 유연하다. 인터넷 익스플로러에서는 지원하지 않는다는 점을 참고하자.
```javascript
const p = document.querySelector('p)
p.append('I am new text') // 문단의 마지막에 해당 문구가 추가됨
```
<br/>
prepend는 append와 달리 특정 요소의 앞에 추가할 수 있다. 
```
p.prepend('I am the firtst stentence!') // 문단의 처음에 해당 문구가 추가됨
```
<br/>
### insertAdjacentElement()
추가적으로 inswertAdjacentElement 메서드를 통해서 요소를 특정 위치에 삽입할 수도 있다. 인수로는 (위치, 요소)를 전달하면 된다.
위치(position)에 입력가능한 파라미터는 다음과 같다. 
<br/>
<li>beforebegin</li>
<li>afterbegin</li>
<li>beforeend</li>
<li>afterend</li>

<br/>
## 삭제하기
특정 요소를 삭제하는 방법은 removeChild 메서드, remove 메서드를 사용하는 방법 2가지가 있다. 
<br/>
### removeChild()
메서드 이름에서도 알 수 있듯이 자식 요소를 제거하는 것이다. 따라서 이 메서드를 사용하기 위해서는 부모 요소를 선택해야 한다. 
만약 body의 자식요소인 p를 삭제하고 싶다면 body를 선택해야 하는 것이다.
```javascript
p.parentElement.removeChild(p)
```
<br/>
### remove()
remove는 removeChild보다 훨씬 사용하기 간편한 메서드이다. 삭제하고자 하는 요소에 바로 remove를 적용하면 된다.
```javascript
p.remove()
```
