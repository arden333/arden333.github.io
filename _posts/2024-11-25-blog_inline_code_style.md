---
layout: single
title: "[blog] 인라인 코드 색상 변경"
categories: "blog"
tags: ["인라인 코드", "blog"]

toc: true
toc_sticky: true
---
## 인라인 코드
인라인 코드는 코드 블록과 달리 텍스트 중간에 코드를 넣을 때 이렇게 `코드`가 구분되도록 표시하는 것을 의미한다.

<br/>
Minimal mistakes테마, 특히 default 테마의 경우 검은색 글자에 옅은 회색 배경이어서 인라인 코드가 잘 구분되지 않았다.
필자는 인라인 코드를 본래 용도인 코드를 입력하는 것 외에도 특정 문구를 강조할 때도 사용하고 싶었기 때문에 색상을 변경하기로 했다.

## 인라인 코드 색상 변경 방법
Miminal mistakes의 기본 테마 중 어두운 계열은 테마는 `_sass/minimal-mistakes/skins/현재 사용중인 테마명.scss`에 들어가서 `$code-background-color` 값을
변경해주면 쉽게 인라인 코드 배경색을 바꿀 수 있다.

<br/> 그러나 문제는, default 테마는 이 속성 자체가 없다. 그래서 추가를 하고 값도 설정해봤지만 오류만 뜨고 적용되지 않았다. 그래서 다음의 방법을 시도해보았다.
먼저, `_sass/minimal-mistakes/_pages.scss`로 들어간다. 그리고 Ctrl+F를 해서 'pre'를 찾자. 그러면 아래의 코드가 보일 것이다. 

<br/>
<img width="523" alt="기본코드" src="https://github.com/user-attachments/assets/57498641-5668-4721-bb56-a2d8003a23d2">
<br/>
이 코드에 인라인 코드로 표현되었으면 하는 글자색과 배경색을 지정해주면 된다.
<br/>
필자는 다음의 코드를 추가 및 변경 해주었다. 색상은 사용자가 원하는 색으로 변경하면 된다.
<br/>
```css
color:#548779; // 추가
background: #dbefe3; // 변경
```
<br/>

그리고 git commit, push를 하면 `인라인 코드`가 이렇게 적용된다.
