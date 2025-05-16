# 📝정리 내용

- 모던 자바스크립트

## 💡 처음 알게 된 사실

### JavaScript vs ECMAScript

- Javascript ≠ ECMAScript
1. JS는 프로그래밍 언어, ECMAScript는 프로그래밍 언어의 표준(결과물 vs 설명서)
2. ECMAScript는 JS 표준화를 위해 만들어졌지만 JScript나 ActionScript 등도 준수
3. JS는 ECMAScript 기반이지만 다른 **부가적 기능**도 존재
    1. 특히 HTML 코드 제어에 사용하는 **DOM**의 문법은 ECMAScript에 표준화된 문법이 아닌 WebIDL에서 표준화된 기술

### Symbol

- 기본형 데이터 타입 중 하나
- 코드 내 유일한 값을 가진 변수명 생성 시 사용

```jsx
const symbolA = Symbol('this is a user');
const symbolB = Symbol('this is Symbol');

console.log(symbolA === symbolB); // false

symbolA === 'this is user'; // false
symbolA === 'user'; // false
symbolA === 'Symbol'; // false
symbolA === true; // false
symbolA === false; // false
symbolA === 123; // false
symbolA === 0; // false
```

### BigInt

- 아주 **큰** 정수 표현에 사용
- JS의 숫자형 값에는 9천조 정도의 정수 표현 한계 존재(한계 초과 시 연산에 미세한 **오류**)
- 암호 작업이나 계산기 관련 작업 시 사용

```jsx
console.log(9007199254740993n); // 9007199254740993n
console.log(BigInt('9007199254740993')); // 9007199254740993n
```

- 문자열로 넘겨주지 않고 그대로 사용 시 안전한 최대 정수로 처리
- 소수 표현에 사용 불가

```jsx
1.5n; // SyntaxError
// 소수점 아래는 버리고 정수 형태로 리턴
10n / 6n; // 1n
5n / 2n; // 2n
// BigInt 타입끼리만 연산 O
3n * 2; // TypeError
3n * 2n; // 6n
Number(3n) * 2; // 6
```

- 큰 범위의 정수 **안전**하게 **사용** O / 제한 사항으로 활용 잘 X

### Arguments

- 함수 내부에서 **자동**으로 **생성**되는 arguments **객체**

```jsx
function printArg() {
	for (const arg of arguments) {
		console.log(arg);
	}
	console.log('------------');
}

printArg('y');
printArg('y','u','j', 'i');
```

- parameter의 이름이나 변수를 arguments로 지으면 X
- 불규칙하게 arguments 전달되는 상황에서 유연한 사용 O
- 단점
    - arguments 객체가 유사 배열이기 때문에 배열 메소드 사용 X
    - arguments 전체를 다룸 → 마지막 두 개만 다루려면 인덱싱으로 세분화 과정 필요

### Rest parameter

- arguments의 단점 보완
- 배열 메소드 사용 O

```jsx
function printArg(...args) {
	for (const arg of args) {
		console.log(arg);
	}
	console.log(args.splice(0, 2));
	console.log('------------');
}

printArg('y');
printArg('y','u','j', 'i');
```

- 일반 파라미터와 동시 사용 O(반드시 가장 마지막에 작성)

```jsx
function printArg(first, second, ...others) { 
	console.log('레이스 결과');
	console.log(`우승: ${first}`);
	console.log(`준우승: ${second}`);
	for (const arg of others) {
		console.log(`참가자: ${arg}`);
	}
}

printArg('y','u','j', 'i', 'n');
```

## 📌 기억할 것

### Typeof 연산자

- 키워드 사이에 공백을 두고 작성하거나 괄호로 감싸서 사용 O

```jsx
typeof []; // object
typeof(NaN); // number
```

- null이 리턴되는 것이 아닌 obj 리턴

```jsx
typeof null; // obj
```

- 함수는 obj?

```jsx
function sayHi() {
	console.log('Hi!?');
}

typeof sayHi; // function
```

⇒ `typeof` 연산자를 함수에 사용하면 function이 리턴

### Boolean 값

<img src="https://github.com/user-attachments/assets/2a559f1e-434d-4155-8110-e223d37b38d0" width="50%" height="50%">


- 0과 빈 문자열이 `false` 값이라고 []과 {}이 `false`라고 오해할 수 있지만 둘 다 `true` 값
- 헷갈리는 경우 `Boolean()`에 값을 넣어 확인

### &&와 || 연산자

- &&연산자는 왼쪽이 **truthy** 값이면 **오른쪽** 반환
- || 연산자는 왼쪽이 truthy 값이면 왼쪽 반환

```jsx
console.log(null && undefined); // null
console.log(0 || true); // true
console.log('0' && NaN); // NaN
console.log({} || 123); // {}
// ✅ && 연산자는 TRUE면 오른쪽 (츄오)
```

- &&와 || 연산자 동시 사용 시 **&&** 연산자가 우선순위 ⬆

```jsx
console.log(true || (false && false)); // true
console.log((true || false) && false); // false

console.log('Codeit' || (NaN && false)); // Codeit
console.log(('Codeit' || NaN) && false); // false
```

→ 다양한 연산자들을 **복합**적으로 **사용** 시 **소괄호**로 의도에 맞게 표기하는 습관 들이기.

### NULL 병합 연산자 ??

- **??**: **`null` / `undefined`**일 때만 **오른쪽** 값을 반환
- 즉, `0`, `false`, `""`은 그대로 유지

```jsx
const width1 = null || 150;
const width2 = null ?? 150;

console.log(width1); // 150
console.log(width2); // 150

const title1 = 0 || 'codeit';
const title2 = 0 ?? 'codeit';

console.log(title1); // codeit
console.log(title2); // 0
```

- null과 undefined 값일 때 `||`과 **동일**하게 동작하지만 그 이외의 값인 falsy 값에서는 **다름**

### 함수

- 함수 안에 선언된 함수는 밖에서 선언 X
- 조건문, 반복문과 같은 코드 블록에서 사용 시 전역적으로 사용 O
- **함수 표현식**: 함수가 값처럼 사용되는 경우(꼭 변수에 넣지 않더라도)

```jsx
function jeon() {
	console.log('Hi');
}

// var: 함수 스코프 | let/const: 블록 스코프
const yujin = function() { 
	console.log('WRUD');
}
```

- 선언식 vs 표현식
    - **함수 선언식**: 함수 호출 시 자유로운 위치에서 호출 O
    - **함수 표현식**: 반드시 선언 이후에 호출할 수 있어 가독성⬆ / 변수의 스코프도 사용 가능

### 즉시 실행 함수

- 함수 선언 순간 즉시 실행 → **초기화** / 일회성 기능에 활용

```jsx
(function (x, y) {
  console.log(x + y);
})(3, 5);
```

- 이름을 지어주더라도 외부에서 **재사용 X**

### 값으로서 함수

- JS에서 함수가 객체 타입으로 평가됨

```jsx
const yujin = {
	name: 'yujin',
	age: '25',
	sayHi: function(name) {
		console.log(`Hi! ${name}`);
	}
}
yujin.sayHi('Javascript');

const myArr = [
	'yujin',
	2025,
	function(name) {
		console.log(`Hi! ${name}`);
	},
];
myArr[3]('function');
```

- **콜백 함수**: 함수에 파라미터로 전달되는 함수
- 고차 함수: 함수를 리턴하는 함수
- 일급 함수: 변수나 다른 데이터 구조에 할당되고 파라미터로 전달되기도, 리턴 값이 되기도 하는 함수

### Parameter

- 파라미터가 존재하는 함수에 파라미터 미전달 → undefined

```jsx
function yujin(name = 'Yujin') { // 기본값
	console.log(`Hi! My name is ${name}!`);
}

yujin();
```

- 두 번째 파라미터에 값 전달할 때 첫 아규먼트는 undefined 선언하면 기본 값이 출력됨

```jsx
function yujin(name = 'Yujin', interest) { // 기본값
	console.log(`Hi! My name is ${name}!`);
	console.log(`I like ${interest}!`);
}

yujin(undefined, 'game'); // Yujin, game
```

- null을 전달한다고 기본값 사용 X

###
