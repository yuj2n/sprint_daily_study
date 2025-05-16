# 📝정리 내용

### 위클리 페이퍼 5주차

[sprint_weekly_paper/Topic/week5.md at main · yuj2n/sprint_weekly_paper](https://github.com/yuj2n/sprint_weekly_paper/blob/main/Topic/week5.md)

```markdown
# 📖Weekly Paper - Week 5

# 🔍Q1.
- 🇶1. 자바스크립트 this에 대해 설명해 주세요.
> this는 JavaScript에서 실행 문맥(Execution Context)에 따라 달라지는 특별한 키워드입니다. this의 값은 함수가 호출되는 방식에 따라 결정됩니다.

## 1. 기본적인 this의 동작
```js
console.log(this); // 브라우저에서는 window, Node.js에서는 global 객체
```

## 2. 객체의 메서드에서 this
```js
const obj = {
  name: "JavaScript",
  getName: function () {
    console.log(this.name);
  }
};
obj.getName(); // "JavaScript"
this는 메서드를 호출한 객체(obj)를 가리킵니다.
```

## 3. 단독 함수 호출 시 this
```js
function showThis() {
  console.log(this);
}
showThis(); // 브라우저에서는 window, 'use strict'에서는 undefined
```
- 일반 함수에서 this는 전역 객체(window 또는 globalThis)를 가리킵니다.
- strict 모드 ('use strict')에서는 undefined가 됩니다.

## 4. 생성자 함수에서 this
```js
function Person(name) {
  this.name = name;
}
const p = new Person("John");
console.log(p.name); // "John"
```
- new 키워드를 사용하면 this는 새로운 객체를 가리킵니다.

## 5. 화살표 함수에서 this
```js
const obj = {
  name: "JavaScript",
  getName: () => {
    console.log(this.name);
  }
};
obj.getName(); // undefined (화살표 함수는 `this`를 바인딩하지 않음)
```

- 화살표 함수는 this를 자신의 스코프에서 찾지 않고, 상위 스코프의 this를 사용합니다.

## 6. call, apply, bind를 사용한 this 변경
```js
function greet() {
  console.log(this.name);
}

const user = { name: "Alice" };

greet.call(user);  // "Alice"
greet.apply(user); // "Alice"

const boundGreet = greet.bind(user);
boundGreet(); // "Alice"
```

- call, apply, bind를 사용하면 임의의 객체를 this로 설정할 수 있습니다.

# 🔍Q2.
- 🇶2. 렉시컬 스코프(Lexical Scope)에 대해 설명해 주세요.
> **렉시컬 스코프(Lexical Scope, 정적 스코프)**란 함수가 선언된 위치에 따라 스코프(범위)가 결정되는 방식을 의미합니다.

## 1. 렉시컬 스코프의 개념
```js
function outer() {
  const name = "JavaScript";
  
  function inner() {
    console.log(name); // outer 스코프의 name 접근 가능
  }

  inner();
}
outer(); // "JavaScript"
```

- inner() 함수 내부에서 name을 찾을 때, 자신의 스코프에 없으면 바깥 스코프(outer 스코프)에서 찾습니다.
- 함수가 선언된 위치(렉시컬 환경)에서 스코프가 결정됩니다.

## 2. this와의 차이점
- 렉시컬 스코프는 "함수가 어디서 선언되었는지"에 따라 결정됩니다.
- this는 "함수가 어떻게 호출되었는지"에 따라 결정됩니다.

## 3. let, const와 블록 스코프
```js
if (true) {
  let a = 10;
}
console.log(a); // ReferenceError: a is not defined
```

- let과 const는 블록 스코프(block scope)를 따르므로, 블록 {} 내부에서만 접근 가능합니다.

## 4. var와 함수 스코프
```js
if (true) {
  var b = 20;
}
console.log(b); // 20 (var는 함수 스코프를 가지므로 if 블록 바깥에서도 접근 가능)
```

- var는 **함수 스코프(function scope)**를 가지므로 블록을 무시하고 접근할 수 있습니다.

## 5. 클로저(Closure)와 렉시컬 스코프
```js
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
```

- inner 함수는 outer 함수의 스코프에 접근할 수 있기 때문에 count를 유지합니다.
- 이를 **클로저(Closure)**라고 합니다.

------------

📌 정리
- 렉시컬 스코프는 함수가 선언된 위치에 따라 스코프가 결정됩니다.
- this는 호출 방식에 따라 동적으로 결정됩니다.
- 클로저는 렉시컬 스코프를 활용하여 외부 함수의 변수에 접근하는 함수입니다
```