---
layout: single
title: "[JS] 속성(Attribute)값 가져오고 설정하기"
categories: "JavaScript"
tags: ["Attribute", "Javascript"]

toc: true
toc_sticky: true
---

자바스크립트로 html 태그의 속성에 접근하고 수정, 추가하는 방법에 대해 정리하였다.


   
<br/>
## 속성에 접근하기
아래의 id와 속성을 가진 이미지가 있다고 하자.
```html
<img id='banner' src='https://images.unsplash.com'>
```
<br/>   
이미지의 id에 접근하기 위해서는 먼저 객체를 선택한 후 '.속성명'을 붙여주면 된다.
```javascript
image = document.querySelector('#banner')

//id에 접근
image.id //'banner'

// 소스 주소에 접근
image.src // 'https://images.unsplash.com'
```
<br/>
getAttribute를 통해 접근할 수도 있다.
```javascript
image.getAttribute('id')
image.getAttribute('src')
```
<br/>
## 속성값 설정하기
setAttribute를 사용해서 속성값을 설정해줄 수도 있다. 인수는 (속성명, 값)으로 전달한다.
```javascript
image.setAttribute('alt', 'Chikens')
```

<br/>
## 속성값 수정하기
```javascript
image.setAttribute('alt', 'Monkeys')
image.alt = 'Monkeys'
```
