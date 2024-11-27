---
layout: single
title: "[JS] 자바스크립트가 싱글스레드인데 비동기식 처리가 가능한 이유"
categories: "Javascript"
tags: ["싱글스레드", "Javascript"]

toc: true
toc_sticky: true
---

## 스레드(thread)란?
프로세스가 할당 받은 자원을 이용하는 실행의 단위이며, 작업에 따라 프로세스 내에 여러 개의 스레드가 생길 수 있다. 
예를 들어, 브라우저를 하나의 프로세스라고 가정하면 블로그 작성하는 탭이 첫번째 스레드, 유튜브 영상을 틀어놓은 탭이 두번째 스레드가 된다. 
각각의 스레드는 독립적인 작업을 수행해야하기 때문에 고유한 스레드 ID, 프로그램 카운터, 레지스터 집합, 스택을 갖고 있다.

### 싱글 스레드(single thread)
싱글 스레드는 한번에 하나의 일을 수행하는 것을 의미한다. 자바스크립트는 싱글 스레드로, 한 번에 최대 한 줄의 코드, 즉 하나의 일만 처리할 수 있다.
멀티태스킹이 불가능하다는 의미이다. 

<img src='https://velog.velcdn.com/images%2Fgil0127%2Fpost%2Fe77bf094-c662-48ac-ad2e-530d9bd0f781%2Fsingle.gif' alt='싱글스레드'>
<br/>
<img src='https://velog.velcdn.com/images%2Fgil0127%2Fpost%2F813ea794-6eef-40b4-8042-09a8551082fd%2Fmulti.gif' alt='멀티스레드'>

## 싱글 스레드로 여러 요청을 처리하는 방법
<br/>
그러나 자바스크립트는 싱글 스레드가 아닌 듯이 작동하는 것처럼 보이는데 그 이면을 알아보자.
<br/>
```javascript
console.log('I print first') // 1번
setTimeout(() => {
  console.log('I pring after 3 seconds);
}, 3000) // 2번
console.log('I print second') // 3번
```
<br/>
위의 코드에서 출력은 1번 - 3번 - 2번 순서로 출력된다. 
그러면 2번 코드가 실행되는 동안 3번 코드가 출력되는 것인데, 그럼 동시에 코드가 진행되는 것은 아닌가?
결론부터 말하자면 `아니다`

<br/>
2번 코드가 실제로 작동하는 방식은 web API로 함수를 인식하고 브라우저에 setTimeout을 전달한다. 
그러면 3초동안 시간을 세고 있는 일은 자바스크립트가 아닌 브라우저가 한다.
브라우저에게 일을 넘겨주고 자바스크립트는 3번 코드를 실행하는 것이다.
3초 후 브라우저에서 응답이 오면 자바스크립트가 2번 코드를 실행한다. 그러므로 자바스크립트는 한 번에 한 가지 일만 하는 것이다. 

<br/>
즉, 자바스크립트는 비동기작업을 통해 여러 요청들을 처리할 수 있는데, 그 과정을 다음의 그림을 통해 설명할 수 있다.
<br/>
<img src='https://velog.velcdn.com/images/devmag/post/13d45ece-3979-47af-9761-d182d04f6a0c/image.png' alt='비동기작업'>
<br/>
<img src='https://github.com/user-attachments/assets/395b1f5e-b440-47de-909a-d54f63583c0a' alt='작동과정'>
<br/>
1. 모든 코드는 먼저 call stack에 쌓인다. 1번 코드는 call stack에서 바로 실행된 후 제거된다.
2. 다음으로 setTimeout이 call stack에 쌓인다. 그러나 이는 web API에서 함수를 인식하고 브라우저에서 타이머를 생성한다. 그래서 스택에서 바로 제거되지 않고 web API에서 정해진 시간동안 처리된다.
3. 자바스크립트는 다음 코드인 3번 코드를 실행한다. call stack에서 실행한 후 제거한다.
4. 3초 후 처리 끝난 2번 코드는 task queue로 콜백을 전달한다.
5. Event Loop가 call stack에 스택이 없는 것을 확인하면, setTimeout의 콜백함수를 호출시킨다.
6. 3번 코드의 실행결과가 출력된다.
<br/>

**참조**
<li>[싱글스레드 vs 멀티스레드](https://velog.io/@gil0127/%EC%8B%B1%EA%B8%80%EC%8A%A4%EB%A0%88%EB%93%9CSingle-thread-vs-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C-Multi-thread-t5gv4udj)</li>
<li>[자바스크립트는 싱글 스레드인가?](https://velog.io/@devmag/Javascript-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%8B%B1%EA%B8%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%B8%EA%B0%80)</li>
