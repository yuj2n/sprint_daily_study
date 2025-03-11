# 📝정리 내용

- 프로그래밍과 데이터 in JavaScript

## 💡 처음 알게 된 사실

### toFixed()

```jsx
let int = 62.99999;
int.toFixed(); // 63;
Math.round(int); // 63;
```

### Immutable(불가변성)

```jsx
// 배열은 mutable
let myArray = ['C', 'o', 'd', 'e', 'i', 't'];
myArray[0] = 'B';
console.log(myArray);

// 문자열은 immutable
let myString = 'Codeit';
myString[0] = 'B';
console.log(myString);
// ["B", "o", "d", "e", "i", "t"]
// **Codeit**
```

- 변수에 할당된 문자열을 바꾸고 싶다면 새 문자열 지정해주어야 함.
- 문자열이 가진 메소드들은 모두 본래 문자열 수정 X → 문자열에 splice() 사용 X

📖 배열과 문자열은 비슷해서 for .. of문이 둘 다 사용되지만 자료형도 다르고 **가변성**의 차이 존재

### 참조형 복사

```jsx
function cloneObj(obj) { // 참조형 복사 함수
	let temp = {};
	for (let key in obj) {
		temp[key] = obj[key];
	}
	return temp;
}

let course1 = {
	title: "책",
	language: "js",
	prerequisite: []
};

let course2 = cloneObj(course1); 
```

- let course2 = `Object.assign`(course1);로도 복사 O
- `course1.prerequisite` === `course2.prerequisite`;
- 선이수과목 프로퍼티가 배열이기 때문에 주소값이 복사

## 📌 기억할 것

### 참조형

![image.png](attachment:932c98cd-8293-4859-a412-57dd02011e5d:image.png)

```jsx
let x = 3;
let y = x;
y=5;
// x = 3, y = 5
```

```jsx
let x = { name: '전유진' }
let y = x; 
y.birth = 2017; // x === y
```

- JS에서 변수에 객체 값을 할당한 경우에는 변수와 객체 사이에 길이 열림

→ 변수 값을 다른 변수에 할당하면 길이 하나 더 생겨 y의 값을 **수정**하면 x에도 **반영**됨.

### 변수와 상수

- 변수로 선언했지만  동작할 때에는 상수로 쓰이는 경우 많음

```jsx
const myName = "유진";
const MY_NAME = "전유진";
```

- 상수는 대문자, 여러 단어는 _로

```jsx
const x = { name: "전유진" };
x.birth = 2017;
```

- 객체의 프로퍼티나 배열의 요소들이 변경되는 경우는 변수의 주소값을 변경하는 것이 아니기 때문에 **변수 값** 충분히 **변화 가능(재할당 X)**

### Var의 문제

1. 중복 선언 가능

```jsx
var myVariable = 'codeit';
console.log(myVariable);
var myVariable = 'Codeit!';
console.log(myVariable); 
// codeit / Codeit!
```

1. 함수 스코프

```jsx
{ // x에 접근 O
  var x = 3;
}
function myFunction() { // func만 접근 X
  var y = 4;
}
```

- { }안에는 밖에서 접근 불가한 let, const와 달리
- `if, for, while, switch` 등 다양한 상황에서 선언한 변수가 자칫, 전역변수의 역할 O

1. 호이스팅(Hoisting)

```jsx
console.log(myVariable);
var myVariable;
// undefined
```

- `let, const`는 선언 이전 사용 X
- `var`는 호이스팅으로 변수 선언이 끌어올려지며, 함수도 호이스팅이 적용되어 선언 전 호출해도 동작 → 코드 흐름에 **부정적** 영향