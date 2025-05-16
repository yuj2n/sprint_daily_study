# 📝정리 내용

- 프로그래밍 핵심 개념 in JS

## 📌 기억할 것

### 자료형

- `typeof typeof`8 = `typeof` ‘number’ = string

### 형 변환

- `Number`(문자) = “NaN”
- true = 1, false = 0
- `Boolean`(문자 or 숫자) = true
- `Boolean`(’ ’, 0, NaN) = false
- **falsy** : ’ ’, 0, NaN
- `+`연산자는 문자 우선
- 비교 연산자 값 계산 안되는 경우: false
- `==`는 동등/부등, `===`는 일치/불일치

```jsx
console.log(Boolean('문자')); /* true */
```

### Quiz

- `Boolean`(NaN) || `Boolean`('0') → ?
- console.log('5' / true != '5'); → ?

### 조건문

- if문 : **범위**를 만족하는 조건식 / **`===`**로 일치 비교 필수
- switch문: **특정 값** 만족하는 조건식 / 값 비교 시 자동으로 자료형 **엄격 구분**