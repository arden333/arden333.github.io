---
layout: single
title: "[JS] function 함수"
categories: "JavaScript"
tags: ["함수", "JavaScript"]

toc: true
toc_sticky: true
---


## 함수(function)
함수는 하나의 코드 덩어리로, 간단한 방법으로 코드를 재사용할 수 있게 하는 방법을 의미한다.   
functions allows us to write reusable and modular code!


자바스크립트에서의 함수 구문은 다음과 같다.

```javascript
function funcName(){
// do something
}
```

함수를 정의한 후 실행하기 위해서는 함수이름만 적어주면 된다.

```javascript
funcName();
```


## 인수(argument)
함수에 특정한 input을 전달할 수도 있다. 이 값을 인수(argument)라고 한다. 인수는 숫자, 텍스트, 배열, 함수 등을 받을 수 있다.   
누군가에게 인사를 하는 함수를 만들어보자.

```javascript
function greet(firstName){
  console.log(`Hi, ${firstName})
}
```

인수에 해당하는 fristName에 Eric을 입력할 경우, 출력값은 'Hi, Eric'이 된다.

2개 이상의 인수를 사용하려면 ',' 사용해서 구분해준다.
   
```javascript
repeat(str, num) {
  let result = '';
  for (i=0; i<num; i++){
    result += str;
  }
}
```

repeat(*,5)를 실행할 경우 '*****'를 출력한다.


## 반환값(return)
console.log()로 출력한 값은 변수로 저장할 수 없다(unidentified로 나옴). 함수의 반환값을 사용하기 위해서는 return을 사용해야 한다. 
즉, 함수 밖으로 값을 보낼 수 있는 것이다.

```javascript
function add(x,y) {
  let sum = x + y;
  return sum;
}

result = function(3,5)
// 8
```


## 중첩 함수
함수를 중첩할 경우에는 함수 내에서 중첩된 함수를 실행해줘야 한다. 중첩된 함수를 자식함수, 그것을 포괄하고 있는 함수를 부모함수라고 한다면 부모함수내에서 자식함수를 실행해줘야 한다는 의미이다.

```javascript
function BankRobbery() { //부모함수
  const heroes = ['ironman', 'spiderman', 'thor']
  function cryForHelp() { //자식함수
    for (let hero of heroes) {
      console.log(`PLEASE HELP US, ${hero.toUpperCase()}`)
    }
  }
cryForHelp(); //자식함수 실행
}
```


## 함수표현식(Function expression)
함수를 다른 표현방식으로 정의할 수도 있다. 정의하는 구문은 달라도 실행하는 구문은 '함수명()'으로 동일하다.

```javascript
//기존방식
function add(x,y){
  return x+y;
}

//다른 방식
const add = function (x,y){
  return x+y;
}
```



## 메서드와 함수의 차이
모든 메서드는 함수이지만 모든 함수가 메서드인 것은 아니다. 메서드는 '.함수명()'의 형태이며 특정 객체에 종속되어 있다. 메서드는 객체에 속성으로 추가된 함수이다.

간단한 수학계산식을 메서드로 만들어보자.
```javascript
myMath = {
  PI: 3.14,
  square: function(num) { // 줄여서 square(num)만 써도 됨
    return num*num;
  },
  cube: function(num) {
    return num**3;
  }
}

//메서드 사용
myMyth.PI //3.14
myMyth.square(2) //4
myMath.cube(2) //8
```



## 함수를 인수로 받는 메서드
### map
배열의 각 요소를 순회하며 함수를 실행한다. 함수를 먼저 정의한 후 인수에 그 함수를 입력할 수도 있디만 대부분의 경우에는 인수를 넣는 자리에서 바로 함수를 정의한다. 

배열의 각 요소를 2배로 만들어보자.

```javascript
const numbers = [1,2,3,4,5]

const doubles = numbers.map(function(num){
  return num*2;
}
```


## arrow function
arrow function은 기존의 함수정의 구문을 좀 더 간결하게 작성하는 방식이다. 이는 꽤 최신기능으로, 인터넷 익스플로러에서는 지원하지 않는다. arrow function은 인수에 함수를 전달할 때 사용하면 구문이 간결해지기 때문에 유용하다.

```javascript
//기존방식
const sum = function(x, y) {
  return x+y;
}

//arrow function 방식
const add = (x, y) => {
  return x+y;
}

//인수가 1개일 경우는 괄호를 생략 가능
const squre = x => {
  return x*x;
}

//인수가 없을 경우는 빈 괄호 입력
const rollDice = () => {
  return Math.Floor(Math.random()*6) + 1;
}

//인수에 함수를 전달할 때 사용할 경우
const goodMovies = movies.filter(m => m.scores > 90)
```

함수 정의를 더 짧은 구문으로 할 수도 있다. 중괄호{} 대신 소괄호()를 쓰고, return을 생략하는 것이다. 간단한 함수라면 한 줄의 코드로도 작성 가능하다. 단, 소괄호 안에는 하나의 표현식만 있어야 한다. 2개의 이상의 표현식이 있다면 어느 것을 반환해야할지 알 수 없기 때문이다.  
   
```javascript
const rollDice = () => (
  Math.Floor(Math.random()*6 + 1; // () 사용, return 생략
)

const add = (x,y) => a,b; () 생략, 한 줄로 작성
```
