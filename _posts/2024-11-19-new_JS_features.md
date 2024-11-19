---
layout: single
title: "[JS] 자바스크립트의 매개변수, 스프레드, 구조분해할당"
categories: "JavaScript"
tags: ["매개변수", "스프레드", "구조분해할당", "JavaScript"]

toc: true
toc_sticky: true
---

자바스크립트에서의 최신 기능들인 default parameter, spread, destructure에 대한 내용이다. 
<br/>
## default parameter
함수에서 인수를 입력하지 않아도 기본값이 정해지도록 설정하는 것을 의미한다. 이 때 인수의 순서가 중요한데, 기본값이 있는 인수는 기본값이 없는 인수 다음에 반드시 와야한다. 


```javascript
//정육면체 주사위 굴리기
function rollDice(numSide=6) {
  Math.Floor(Math.random() * numSide) + 1
}

//dafault parameter의 순서는 맨 뒤!
function greet(name, msg='Hi',) {
  console.log(`${msg}, ${name}`)
}
```

<br/>
## 스프레드(spread)
스프레드 연산자(...)를 이용해서 배열을 펼쳐 각 요소에 접근 가능하게 하는 것을 의미한다. 

아래에서 보듯이 max()메서드에 각 숫자를 인수로 전달할 때는 최대값 5가 제대로 나오지만, 배열로 전달하면 값이 제대로 나오지 않는다. 

```javascript
Math.max(1,3,5) // 5

Math.max([1,3,5]) // undefined
```
이 때, 스프레드 연산자(...)를 사용할 수 있다. 배열이 아니더라도 반복가능한 객체라면 각 요소가 분리될 수 있다.

```javascript
num = [1,3,5]
Math.max(...num)

console.log(...'hello')
//h e l l o
```

<br/>
스프레드는 객체를 변형시키지 않고 복사할 때 유용하게 사용된다. 특히 라이브러리나 react 도구로 작업할 때 유용하다. 스프레드를 이용해 객체를 쉽게 복사하고 합칠 수 있다.

```javascript
const cat = ['A','B','C']
const dog = ['a','b','c']

const catDog = [...cat, ...dog] /// ['A','B','C','a','b','c']
```
<br/>
딕셔너리형 타입에도 스프레드를 활용해 복사하고 속성을 추가할 수 있다.

```javascript
const dataFromForm = {
  email: 'abc@gmail.com',
  password: 'aabbcc',
  username: 'derik'
}

// 속성을 추가해 새 변수 생성하기
const newUserInfo = {...dataFromForm, id:123, isAdmin: false}
```
   
<br/>
## 구조분해할당(destructure)
구조분해할당은 객체, 배열의 요소를 분해해서 그 값들을 각각의 변수로 할당하는 표현식을 의미한다. 객체, 배열의 순서대로 변수가 할당된다.
<br/>
### 배열 분해
```javascript
const raceResults = ['Emily', 'George', 'Suzy']

const [gold, silver, bronze] = raceResults;
gold; // Emily
silver; // George
bronze; // Suzy

const [gold, ...everyoneElse] = raceResults;
gold; // Emily
everyoneElse; // ['Geroge', 'Suzy']
```
<br/>
### 객체 분해
```javascript
const user = {
  firstName: Harvey,
  lastName: Kim,
  city: NewYork,
  born: 1984
  email: abc@gmail.com,
  age: 40
}

// 변수로 만들고 싶은 항목 key로 꺼내기(변수명이 곧 key)
const {firstName, email, city} = user;

firstName; // Harvey
email; // abc@gmail.com
city; // NewYork

// 변수명 새롭게 정의하고 싶다면 콜론 사용

const {born: birthYear} = user;

birthYear; // 1984
```

<br/>
### 매개변수 분해
```javascript
const user = {
  firstName: Harvey,
  lastName: Kim,
  city: NewYork,
  born: 1984
  email: abc@gmail.com,
  age: 40
}

function fullName(user) {
  const {firstName, lastName} = user;
  return `${firstName} ${lastName}`
}

// 매개변수 분해를 사용사면 더 간결한 코드로 구현 가능
function fullName({firstName, lastNmae}) {
  return `${firstName} ${lastName}`
}

fullName(user) // 'Harvey Kim'
```
