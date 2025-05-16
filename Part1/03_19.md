# 📝정리 내용

- 비동기 자바스크립트

## 💡 처음 알게 된 사실

### try catch 오류 처리

- catch문에 `return`이 있어도 finally 사용 시 뒤의 코드 실행

```jsx
try {
	const response = await fetch('http:...');
	const data = await response.json();
	console.log(data);
} catch (err) {
	console.log(err);
	return;
} finally { //  
	console.log('done');
}
```

## 📌 기억할 것

### Promise란?

- 비동기 작업이 완료되면 값을 알려주는 객체
- 상태
    - Pending
    - Fullfilled
    - Rejected
- 사용
    1. async, await 문법
    2. .then() 메소드

### Async await 문법

- Promise객체 앞에 `await` 키워드 사용 시 fullfilled/rejected 대기
- `await`은 보통 `async` 함수 내부 사용
- `async` 함수는 내부 `await`을 마주치면, 함수 외부 코드 실행

```jsx
async function getEmployees() {
  const response = await fetch('https://learn.codeit.kr/api/employees');
  const data = await response.json();
  return data;
}

const employees = await getEmployees(); // await을 생략하면 employees에 Promise 객체가 할당됩니다.
```

- `async` 함수는 항상 `Promise` 리턴
    - 함수 안에서 `Promise` 리턴 시 그 `Promise` 그대로 리턴
    - 함수 안에서 평범한 값 리턴 시 그 값을 결괏값으로 갖는 `Promise` 리턴

### .then()

- Promise 객체의 메소드

```jsx
fetch('https://learn.codeit.krrrr/api/employees')
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.log('error!'))
  .finally(() => console.log('finished'));

```

- 앞선 Promise가 `fulfilled` 시 결괏값을 콜백의 아규먼트로 전달
- `return`: Promise

### Promise.all()

- 여러 Promise 동시 대기 시 사용

```jsx
async function getEmployee(id) {
  const response = await fetch(`https://learn.codeit.kr/api/employees/${id}`);
  const data = await response.json();
  return data;
}

const promises = [];

for (let i = 1; i < 11; i++) {
  promises.push(getEmployee(i));
}

let employees;

try {
  employees = await Promise.all(promises);
} catch (error) {
  console.log(error);
}

console.log(employees);
```

- `return`: Promise
- 모두 `fulfilled` 되면 리턴 Promise도 `fulfilled`
- 성공 결괏값의 배열 전달
- 하나라도 `rejected`시 `rejected`된 Promise의 결괏값(오류)을 가짐