---
layout: single
title: "[JS] 자바스크립트 promise의 개념과 역할"
categories: "Javascript"
tags: ["promise", "Javascript"]

toc: true
toc_sticky: true
---

## 콜백함수란?
콜백(Callback) 함수는 말하면 매개변수로 함수 객체를 전달해서 호출 함수 내에서 매개변수 함수를 실행하는 것을 말한다.
함수의 매개변수(인자)에 특정 값이나 변수를 전달하는 것이 아닌 함수를 전달해서 함수가 실행되게끔 하는 것이다.
<br/>
콜백함수를 사용하는 주요 메서드는 forEach, map, setTimeout 등이 있다.
<br/>
```javascript
setTimeout(()=>{
  console.lot(print this after 3 seconds), 3000
}
```
<br/>

### 콜백지옥
배경색을 1초마다 무지개색으로 바꾸는 코드를 작성한다고 해보자. 
<br/>
```javascript
setTimeout(() => {
    document.body.style.backgroundColor = 'red';
    setTimeout(() => {
        document.body.style.backgroundColor = 'orange';
        setTimeout(() => {
            document.body.style.backgroundColor = 'yellow';
            setTimeout(() => {
                document.body.style.backgroundColor = 'green';
                setTimeout(() => {
                    document.body.style.backgroundColor = 'blue';
                }, 1000)
            }, 1000)
        }, 1000)
    }, 1000)
}, 1000)
```
<br/>
함수가 중첩되기 때문에 가독성도 떨어지고 코드도 지나치게 길어진다. 색깔을 변경하는 함수를 별도로 정의해서 코드를 간결히 만들어보자.
<br/>
```javascript
const delayedColorChange = (newColor, delay, doNext) => {
    setTimeout(() => {
        document.body.style.backgroundColor = newColor;
        doNext && doNext();
    }, delay)
}


delayedColorChange('red', 1000, () => {
    delayedColorChange('orange', 1000, () => {
        delayedColorChange('yellow', 1000, () => {
            delayedColorChange('green', 1000, () => {
                delayedColorChange('blue', 1000, () => {

                })
            })
        })
    })
});
```
<br/>
코드는 간결해졌지만 여전히 많이 중첩되어 있다. 지금은 간단한 코드라 알아보기 쉬울 수 있지만 복잡한 코드들이 깊게 중첩되어 있다면 코드 가독성이 떨어진다.
코드를 수정하기도 어려울 것이다. 이를 콜백지옥이라고 말하기도 한다.

<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-3082151336412907"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-3082151336412907"
     data-ad-slot="3525353674"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

## promise
### promise 개념과 구문
promise는 어떤 연산 또는 비동기 연산이 최종적으로 성공했는지 실패했는지 알려주는 객체이다. promise를 사용하면 콜백지옥에서 탈출할 수 있다. 
한 단위 들여쓰기로 중첩을 최소화하며 코드를 작성하는 것이 가능하기 때문이다.

<br/>
가짜로 요청하는 promise를 만들어보자. 아래의 코드는 난수가 0.7을 초과하면 url에 접속 성공, 그렇지 않으면 접속 실패를 1초 후에 반환한다. 
promise는 다음의 3가지 상태를 가진다.

<li>pending: 이행하지도, 거부하지도 않은 초기 상태</li>
<li>resolve: 연산이 성공적으로 완료됨</li>
<li>reject: 연산이 실패함</li>
<br/>
아래의 코드에서처럼 resolve와 reject를 명시하지 않으면 fakeRequest는 계속 pending의 상태에 있다. 
<br/>
promise에 들어가는 콜백함수의 매개변수는 resolve, reject 2개가 필요하다. 연산이 성공했을 경우에 대한 것은 resolve, 연산이 실패했을 경우에 대한 것은 reject이다.
<br/>
```javascript
const fakeRequest = (url) => {
    return new Promise((resolve, reject) => {
        const rand = Math.random();
        setTimeout(() => {
            if (rand < 0.7) {
                resolve('YOUR FAKE DATA HERE');
            }
            reject('Request Error!');
        }, 1000)
    })
}
```
<br/>   
              
### then과 catch 메서드
그렇게 만들어진 promise 객체는 비동기 작업이 완료된 이후에 다음 작업을 연결시켜 진행 할 수 있다.
작업 결과에 따라 `.then()` 과 `.catch()` 메서드 연쇄을 통해 성공과 실패에 대한 후속 처리를 진행 할 수 있다.
객체 내부에서 resolve 상태이면 then 메서드로 연결되고, reject 상태이면 catch 메서드로 연결된다.

<br/>
<img src='https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png' alt='promise'>
<br/>
<br/> 
```javascript
fakeRequest('/dogs/1')
    .then((data) => {
        console.log("DONE WITH REQUEST!")
        console.log('data is:', data) // data is: YOUR FAKE DATA HERE 출력됨
    })
    .catch((err) => {
        console.log("OH NO!", err) // OH NO! Request Error! 출력됨
    })
```
<br/>
그러면 다시 처음으로 돌아가 배경색을 무지개 색으로 1초마다 바꾸는 코드로 돌아가보자. 여기에 promise를 적용하면 훨씬 간결한 코드로 바꿀 수 있다.
색을 변경하는 코드에서는 reject가 필요없기 때문에 코드는 더욱 간결해진다.
<br/>
```javascript
const delayedColorChange = (color, delay) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            document.body.style.backgroundColor = color;
            resolve();
        }, delay)
    })
}


delayedColorChange('red', 1000)
    .then(() => delayedColorChange('orange', 1000))
    .then(() => delayedColorChange('yellow', 1000))
    .then(() => delayedColorChange('green', 1000))
    .then(() => delayedColorChange('blue', 1000))
    .then(() => delayedColorChange('indigo', 1000))
    .then(() => delayedColorChange('violet', 1000))
```
<br/>

<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-3082151336412907"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-3082151336412907"
     data-ad-slot="3525353674"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

## 비동기(async), 대기(await) 키워드
### 비동기(async)
async 키워드를 함수 앞에 선언하면 return을 사용하지 않아도 항상 promise를 반환한다. 즉, `return new Promise` 를 생략하고 간단한 코드를 작성할 수 있는 것이다.
<br />
```javascript
const sing = async () => {
  return 'LA LA LA'
}
```
<br />
위의 코드에서는 항상 resolve인 상태이다. async 키워드를 사용한 구문에서는 별도의 reject를 표현하는 구문이 없다. 대신, 오류를 발생하게 하면 reject 상태가 된다.

<br/>
```javascript
const sing = async () => {
  throw 'It's a problem.'
  return 'LA LA LA'
}

sing
  .then(data => {
    console.log('resolved', data)
  })
  .catch(err => {
    console.log('rejected', err)
  })
```
<br/>
throw를 통해 에러를 생성하면 연산이 완료된 상태, 거절된 상태에 대해 모두 `then, catch` 메서드를 통해 연쇄작업이 가능해진다. 

### 대기(await)
await는 promise가 값을 반환할 때까지 기다리기 위해 비동기 함수의 실행을 일시적으로 정지시킨다. await는 비동기 함수에서만 사용된다.

<br/>
배경색을 1초마다 무지개색으로 바꾸는 코드에 async와 await를 적용해보자.
<br/>
```javascript
async function rainbow(){
  await delayedColorChange('red', 1000)
  await delayedColorChange('orange', 1000)
  await delayedColorChange('yellow', 1000)
  await delayedColorChange('green', 1000)
  await delayedColorChange('blue', 1000)
  await delayedColorChange('indigo', 1000)
}
```
<br/>

<br/>
**참고**   
[mdn - Promsie](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)   
[자바스크립트 Promise 개념과 사용하는 이유](https://velog.io/@dongjun187/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Promise-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)
