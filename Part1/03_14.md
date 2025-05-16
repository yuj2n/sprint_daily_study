# 📝정리 내용

- 모던 자바스크립트

## 💡 처음 알게 된 사실

### Spread 구문

- 하나로 묶여있는 값을 각각의 개별 값으로 펼침

```jsx
const person = ['yujin', 25];
const newPerson = [...person, 'web'];

newPerson.push('front');

console.log(person); !== console.log(newPerson);
```

- 함수 호출 시 argument로 활용

```jsx
const intro = (name, age, job) => {
	console.log(`저는 ${name}입니다.`);
	console.log(`${age}살이고,`);
	console.log(`직업은 ${job}입니다.`);
}
// 배열을 argument로 사용 O
const myArr = ['전유진', 25, 'frontend'];
intro(...myArr);
```

- 주의할 점: spread 구문 자체 ≠ 값

```jsx
const latte = {
  esspresso: '30ml',
  milk: '150ml'
};

const cafeMocha = {
  ...latte,
  chocolate: '20ml',
}

[...latte]; // Error

(function (...args) {
  for (const arg of args) {
    console.log(arg);
  }
})(...cafeMocha); // Error
```

- 배열 → 새 배열 생성 O / 함수의 argument 사용 O
- 객체 → 새 배열 생성 X / 함수의 argument 사용 X(객체 표현의 **중괄호** 안에서 **활용!**)

### Optional Chaining

- `?`: 중첩 객체 프로퍼티 접근 시 `null`/`undefined`로 인한 에러 방지를 간결하게

```jsx
function printCatName(user) {
// ?.: 안전하게 접근, ??: 기본값 설정  
console.log(user.cat?.name ?? '함께 지내는 고양이가 없습니다.');
}

const user2 = {
  name: 'Young',
}

printCatName(user2); // 함께 지내는 고양이가 없습니다.
```

### 💡차이점

| 연산자 | 역할 | 예제 |
| --- | --- | --- |
| `?.` (Optional Chaining) | 객체 속성 안전 접근 | `obj?.property` |
| `??` (Nullish Coalescing) | `null`/`undefined` 기본값 설정 | `value ?? default` |

### Computed Property Name

✅ 객체 속성 이름을 동적으로 지정 가능

✅ 변수, 표현식, 함수 반환값을 속성 이름으로 사용 가능

✅ 객체를 보다 유연하게 정의할 수 있음
👉 즉, 정적인 속성 이름만 쓰는 게 아니라, 동적으로 속성을 생성할 때 유용! 🎯

### forEach

- 단순히 배열의 반복 작업이 필요한 경우

```jsx
const firstNames = ['유진','동주','춘필'];
const lastNames = ['전','문','김'];

firstNames.forEach((firstNames, i) => {
	console.log(`${lastNames[i]}${firstName}님`);
});
```

> arr은 ['유진','동주','춘필'].forEach(...)와 같이 직접 배열에 접근하는 경우 사용
> 

### map

- 반복 작업을 통해 새 배열이 필요한 경우

```jsx
const firstNames = ['유진','동주','춘필'];
const lastNames = ['전','문','김'];

const fullNames = firstNames.map((firstNames, i) => lastNames[i] + firstName);
console.log(fullNames); // ["전유진", "문동주", "김춘필"]
```

> forEach()문은 리턴 값이 없기 때문에 변수에 담으면 undefined 반환
> 

📌주의할 점

- 최대 반복 횟수 = 메소드 처음 호출 시 요소의 개수

```jsx
const members = ['유진','동주','춘필'];

members.forEach((member) => {
	console.log(`${memeber}님!`);
	members.push('ㅎㅇ');
});

console.log(members); // ["유진", "동주", "춘필", "ㅎㅇ", "ㅎㅇ", "ㅎㅇ"]
```

- 주의해야 하는 경우

```jsx
const members = ['유진','동주','춘필', '매드'];

members.forEach((member) => {
	console.log(`${memeber}님!`);
	members.pop();
});

console.log(members); // ["유진", "동주"]
```

### 모던한 표기법

```jsx
const propertyName = 'birth';
const getJob = () => 'job';

const codeit = {
  ['topic' + 'name']: 'Modern JavaScript',
  [propertyName]: 2017,
  [getJob()]: '프로그래밍 강사',
};

console.log(codeit);

```

### Destructuring

- event 객체에 target 프로퍼티가 있기 때문에 생략 가능

```jsx
const btn = document.querySelector('#btn');

btn.addEventListener('click', ({ target }) => {
	// event.target.classList.toggle('checked');
	target.classList.toggle('checked');
});	
```

## 📌 기억할 것

### Arrow Function

- ()는 파라미터가 1개일 때 생략 O
- {}는 return문이 1개일 때 생략 O
- {}안의 리턴 값이 객체인 경우 생략 X

```jsx
const getTwice = num => num * 2;
// 객체인 경우 ()로 감싸면 O
const getYujin = () => ({ name: 'Yujin', });
```

- 단점(일반 함수와의 차이)
    - **arguments** 객체 존재 X  → rest parameter로 대체 / 함수 선언식 또는 표현식 사용
    - **this** 사용 시 선언 직전 값과 같기 때문에 window 객체를 가리킴 → 객체에 **메소드** 작성 시 일반 함수 사용 권장

### This

- 함수 내부에서 주로 사용
- 객체의 메소드 생성 시 중요

```jsx
const user = {
  firstName: 'Tess',
  lastName: 'Jang',
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`;
  },
};

console.log(user.getFullName()); // getFullName 안에서의 this는 getFullName을 호출한 user객체가 담긴다!
```

### 표현식

- 하나의 값이 되는 코드

```jsx
// 표현식인 문장
title = 'JavaScript'; // JavaScript
sayHi(); // sayHi 함수의 리턴 값
console.log('hi'); // undefined

// 표현식이 아닌 문장
console.log(if (x < 5) {
  console.log('x는 5보다 작다');
} else {
  console.log('x는 5보다 크다');
});

const someloop = for (let i = 0; i < 5; i++) {
  console.log(i);
};
```

- 일반적으로 표현식인 문장은 세미콜론 첨부 O
- 표현식이 아닌 문장은 문장 자체의 코드 블록(중괄호)으로 그 문장의 범위가 구분

### 구조 분해(배열)

- ex1

```jsx
const name = ['전','유','진'];

const [first, second, third, fourth] = name;
// 전 유 진 undefined
```

- ex2

```jsx
let first = '유';
let second = '진';

[first, second] = [second, first];
```

### 구조 분해(객체)

- ex1

```jsx
const person = {
	name:'yujin',
	age: 25,
	job: 'frontend',
	'serial-num': 'ABCDEFUCK',
};

const { name: called, ...rest } = person;
console.log(called);
console.log(rest);
```

- -으로 연결되어 변수로 사용할 수 없는 이름 → 새 이름 필수

```jsx
const person = {
	name:'yujin',
	age: 25,
	job: 'frontend',
	'serial-no': 'ABCDEFUCK',
};

const propertyName = 'name';
const { [propertyName]: called, 'serial-no': serialNo } = person;
console.log(called);
console.log(serialNo);
```

📚 []로 computed property name 활용 O

### Filter

- 모든 조건에 맞는 요소들을 **배열**로 반환

```jsx
const users = [
  { name: "철수", age: 25 },
  { name: "영희", age: 30 },
  { name: "민수", age: 25 }
];

const filteredUsers = users.filter(user => user.age === 25);
console.log(filteredUsers); // [ { name: "철수", age: 25 },{ name: "민수", age: 25 } ]
```

### Find

- 첫 번째로 조건 만족하는 요소 하나를 **값**으로 반환

```jsx
const users = [
  { name: "철수", age: 25 },
  { name: "영희", age: 30 },
  { name: "민수", age: 25 }
];

const foundUser = users.find(user => user.age === 25);
console.log(foundUser); // { name: "철수", age: 25 }
```

### 🤔차이

| 메서드 | 반환값 | 조건에 맞는 요소가 없을 때 |
| --- | --- | --- |
| `filter` | **배열** (조건에 맞는 모든 요소) | 빈 배열 `[]` |
| `find` | **단일 값** (첫 번째로 찾은 요소) | `undefined` |
- 반복 횟수가 다름 → 프로그램의 효율 측면에서 중요✨

### Some 메소드

- 하나라도 조건 만족 시 `true` 반환

```jsx
const users = [
  { name: "철수", age: 25 },
  { name: "영희", age: 30 },
  { name: "민수", age: 15 }
];

const hasMinor = users.some(user => user.age < 18);
console.log(hasMinor); // true (민수의 나이가 15라서 조건 충족)

```

### Every 메소드

- 모든 요소가 조건 만족 시 `true` 반환

```jsx
const users = [
  { name: "철수", age: 25 },
  { name: "영희", age: 30 },
  { name: "민수", age: 15 }
];

const allAdults = users.every(user => user.age >= 18);
console.log(allAdults); // false (민수가 15세라서 조건 불충족)
```

### Reduce 메소드

- 누적값 계산 시 활용
- 첫 번째 parameter: 반복 동작할 콜백함수 / 두 번째: 초기값(콜백함수의 첫번째 parameter)

```jsx
const numbers = [1, 2, 3, 4];

// reduce
const sumAll = numbers.reduce((accumulator, element, index, array) => {
  return accumulator + element;
}, 0);

console.log(sumAll); // 10
```

### Sort 메소드

- 배열 정렬

```jsx
const letters = ['D', 'C', 'E', 'B', 'A'];
const numbers = [1, 10, 4, 21, 36000];

letters.sort();
numbers.sort();

console.log(letters); // (5) ["A", "B", "C", "D", "E"]
console.log(numbers); // (5) [1, 10, 21, 36000, 4]
```

- 오름차순

```jsx
const numbers = [1, 10, 4, 21, 36000];

// 오름차순 정렬
numbers.sort((a, b) => a - b);
console.log(numbers); // (5) [1, 4, 10, 21, 36000]

// 내림차순 정렬
numbers.sort((a, b) => b - a);
console.log(numbers); // (5) [36000, 21, 10, 4, 1]
```

📌주의할 점: 메소드를 실행하는 **원본** 배열의 요소들을 **정렬**

### Reverse 메소드

- 배열 순서 뒤집기
- parameter 존재 X

```jsx
const letters = ['a', 'c', 'b'];
const numbers = [421, 721, 353];

letters.reverse();
numbers.reverse();

console.log(letters); // (3) ["b", "c", "a"]
console.log(numbers); // (3) [353, 721, 421]
```

📌주의할 점: 메소드를 실행하는 **원본** 배열의 요소들을 **정렬**

### Map

- 이름있는 데이터 저장 = 객체
- 메소드를 통해 값 **추가**&**접근**

```jsx
// Map 생성
const codeit = new Map();

// set 메소드
codeit.set('title', '문자열 key');
codeit.set(2017, '숫자형 key');
codeit.set(true, '불린형 key');

// get 메소드
console.log(codeit.get(2017)); // 숫자형 key
console.log(codeit.get(true)); // 불린형 key
console.log(codeit.get('title')); // 문자열 key

// has 메소드
console.log(codeit.has('title')); // true
console.log(codeit.has('name')); // false

// size 프로퍼티
console.log(codeit.size); // 3

// delete 메소드
codeit.delete(true);
console.log(codeit.get(true)); // undefined
console.log(codeit.size); // 2

// clear 메소드
codeit.clear();
console.log(codeit.get(2017)); // undefined
console.log(codeit.size); // 0
```

- 일반 객체: **문자열**과 **심볼** 값만 key(프로퍼티 네임)로 사용
- **Map 객체**: 메소드로 값을 다룸 → **다양한 자료형**을 **key**로 활용

- 📚**주요 메서드**
    
    
    | 메서드 / 프로퍼티 | 설명 | 예제 코드 | 반환값 |
    | --- | --- | --- | --- |
    | `map.set(key, value)` | `key`를 이용해 `value` **추가** | `map.set("name", "철수");` | `Map` 객체 (체이닝 가능) |
    | `map.get(key)` | `key`에 해당하는 값 가져오기 (없으면 `undefined`) | `map.get("name");` | 값 또는 `undefined` |
    | `map.has(key)` | `key` **존재** 여부 확인 | `map.has("name");` | `true` 또는 `false` |
    | `map.delete(key)` | `key`에 해당하는 요소 **삭제** | `map.delete("name");` | `true` 또는 `false` |
    | `map.clear()` | 모든 요소 **제거** | `map.clear();` | 없음 (`void`) |
    | `map.size` | 요소 **개수** 반환 (메소드 아님) | `map.size;` | 요소 개수 (숫자) |

### Set

- 여러 개의 값을 순서대로 저장 = 배열
- 배열 메소드 사용 x
- Map과 비슷하게 Set만의 메소드로 값을 다룸

```jsx
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"영훈", "윤수"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}

// has 메소드
console.log(members.has('동욱')); // true
console.log(members.has('현승')); // false

// size 프로퍼티
console.log(members.size); // 4

// delete 메소드
members.delete('종훈'); // false
console.log(members.size); // 4
members.delete('태호'); // true
console.log(members.size); // 3

// clear 메소드
members.clear();
console.log(members.size); // 0
```

- 개별 값 접근
    - 일반 객체: 프로퍼티 네임
    - Map 객체: get 메소드
    - 배열: index
    - set: 존재 X

```jsx
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"영훈", "윤수"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}

for (const member of members) { // 반복되는 순간에 개별적으로 접
  console.log(member); // 영훈, 윤수, 동욱, 태호가 순서대로 한 줄 씩 콘솔에 출력됨.
}
```

- 개별 값에 접근 불가함에도 유용하게 사용되는 경우 = **중복 허용 X 값 모을 때**

```jsx
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"영훈", "윤수"}
members.add('영훈'); // Set(2) {"영훈", "윤수"} - **중복**
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"} 
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"} - **중복**
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}
members.add('동욱'); // Set(4) {"영훈", "윤수", "동욱", "태호"} - **중복**
```

- **💻사용**(배열 내 중복 값 제거한 것들의 묶음)

```jsx
const numbers = [1, 3, 4, 3, 3, 3, 2, 1, 1, 1, 5, 5, 3, 2, 1, 4];
const uniqNumbers = new Set(numbers);

console.log(uniqNumbers); // Set(5) {1, 3, 4, 2, 5}
```

- 📚**주요 메서드**

| 메서드 / 프로퍼티 | 설명 | 예제 코드 | 반환값 |
| --- | --- | --- | --- |
| `set.add(value)` | 값을 **추가** (Set 자신을 반환하여 체이닝 가능) | `set.add(1);` | `Set` 객체 |
| `set.has(value)` | 값이 **존재**하는지 확인 | `set.has(1);` | `true` 또는 `false` |
| `set.delete(value)` | 특정 값을 **제거** | `set.delete(1);` | `true` 또는 `false` |
| `set.clear()` | 모든 요소 **제거** | `set.clear();` | 없음 (`void`) |
| `set.size` | 요소 **개수** 반환 (메서드 아님) | `set.size;` | 요소 개수 (숫자) |

### 모듈화

- 코드의 효율적 관리
- 타 프로그램에서 재사용 O
- `<script type=”module” src=””></script>`: js파일에 모듈 스코프 생성
- Live Server: 모듈 문법 활용 시 서버를 통해 파일 실행 필요
- export하여 import된 script 태그는 작성하지 않아도 됨.
- export한 함수/변수는 import한 곳에서 사용되지만 실제 그곳에서 사용 X

```jsx
export function addMenu(data) { // 하위 함수들은 export하지 않아도 작동 O 
  const inputValue = addInput.value;

  if (inputValue === '') {
    emptyAlert();
  } else if (data.length > 4) {
    maxAlert();
  } else {
    add(data);
  }
}
```

 

### Export default

- 모듈에서 단 하나의 대표 기능 내보낼 때 사용
- export와 함께 import 가능!
- *로 import 시 default라는 parameter로 접근

```jsx
export function subtract(a, b) {
  return a - b;
}

**export default** function add(a, b) {
  return a + b;
}
```

```jsx
import **add**, { subtract } from "./math.js"; 

console.log(add(10, 5));      // 15 (default export)
console.log(subtract(10, 5)); // 5 (named export)
```

- 활용

```jsx
const title = '모던자바스크립트';

function print(value) {
	console.log(value);
}

export default { title, print }; // { title: title, print: print } 객체로 평가됨
```

```jsx
import printJS from './print.js';
import yujin, { title as membersTitle } from './members.js';

console.log(printJS.title);
console.log(membersTitle);
```

- 장점
    - import 부분의 코드 간결
    - 다른 모듈과의 이름 중복 방지
- 단점
    - 프로퍼티를 점(.) 표기법으로 접근
    - 각 대상 이름 변경 X

⇒ Named Export 사용 but default export 활용법도 알아두자~

- 📑차이

| 구분 | `export default` | `export` (named export) |
| --- | --- | --- |
| **내보내기 개수** | 한 모듈에 **1개만 가능** | 여러 개 가능 |
| **가져올 때 방식** | `{}` 없이 원하는 이름 사용 가능 | `{}` 안에 지정된 이름 사용 |
| **예제** | `export default function foo() {}` | `export function bar() {}` |
| **가져오는 방식** | `import foo from "./file.js";` | `import { bar } from "./file.js";` |