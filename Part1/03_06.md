# 📝정리 내용

- 프로그래밍과 데이터 in JavaScript

## 💡 처음 알게 된 사실

### for in 반복문

```jsx
let myObject = {
  300: '정수',
};

console.log(myObject['300']);
console.log(myObject.300); // Error!
```

- 숫자형(양수) 프로퍼티 네임은 문자열로 형 변환이 되어 사용

## 📌 기억할 것

### 프로퍼티 네임

```jsx
let myObject = {
  3: '정수3',
  name: 'codeit',
  1: '정수1',
  birthDay: '2017.5.17',
  2: '정수2',
};

for (let key in myObject) {
  console.log(key);
}
 
/* 1
2
3
name
birthDay */
```

- 객체는 정수형 프로퍼티 네임을 **오름차순**으로 먼저 정렬하고, 나머지 프로퍼티들은 추가한 순서대로 정렬하는 특징
- 의도치 않은 결과가 나올 수 있어 정수형 프로퍼티 사용 잘 X

→ 불가피한 경우 이해한 상태에서 사용, 가급적 의미 있는 프로퍼티 네임 사용 권장

### Date 객체

- Month(월) : 0부터 시작
- day(요일) : 0~6(일요일부터 시작)

```jsx
let myDate = new Date('2025-03-05');
let myDate = new Date(2017, 4, 18, 19, 11, 16); /* 2017년4월18일 오후7시11분16초 */
```

```jsx
let myDate = new Date();
console.log(Date.now() === myDate.getTime() === Number(myDate); // true
```

- `Date.now()`는 객체 생성 안해도 됨.

### 배열 메소드

1. `Splice`(추가, 삭제, 추가 내용)
    
    ```jsx
    	ages.splice(5);  /* 5번째 요소부터 뒤에까지 삭제 */
    fruits.splice(0, 1);   /* 맨 앞 요소 1개 삭제 */
    fruits.splice(1, 1, '사과', '청포도');  /* 인덱스 1부터 1개 삭제 후 두 개 추가 */
    ```
    
    | Method |         역할 |
    | --- | --- |
    | shift() | 맨 **앞** 요소 삭제 |
    | pop() | 맨 **뒤** 요소 삭제 |
    | unshift() | 맨 **앞** 요소 추가 |
    | push() | 맨 **뒤** 요소 추가 |
    | indexOf() | 특정 값 존재 시 index 반환, 여러 번 포함되어 있으면, **처음** 발견된 인덱스 return(1,-1) |
    | includes() | 특정 값 배열에 존재하는 지 여부만 확인(T/F) |
    | reverse() | 배열 순서 뒤집기 |
    
    ### for … of 반복문
    
    ```jsx
    let array = ['a','b','c','d']
    
    for (let i = 0; i < array.length; i++) {
    	console.log(array[i]);
    }
    
    **for (let element of array) {
    	console.log(element);
    }**
    
    for (let index in array) {
    	console.log(array[index]);
    }
    ```