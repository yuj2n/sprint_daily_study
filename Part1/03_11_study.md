# 📝정리 내용

- 인터랙티브 자바스크립트

## 💡 처음 알게 된 사실

### Class 태그 선택

```jsx
const myTags = document.getElementsByClassName('color-btn');
console.log(myTags);
console.log(myTags[1]);
console.log(myTags.length);

for(let tag of myTags) {
	conosole.log(tag);
}

// 존재하지 않는 값에 접근
console.log(myTags === null); // false 
console.log(myTags.length); // 0
```

- Index와 length가 있어 배열처럼 보이지만 `splice()`, `push()` 사용 불가
- 여러 태그를 한 번에 선택 가능
- **한 개**만 선택 **O**

### 유사 배열

1. 숫자 형태의 indexing 가능

<img src="https://github.com/user-attachments/assets/98c037f5-aca7-4430-9f8d-52da2a63c4d7" width="40%" height="40%">

1. length 프로퍼티 O

<img src="https://github.com/user-attachments/assets/d5749824-f488-4c96-a69a-abb585265296" width="40%" height="40%">

1. 배열의 기본 메소드 사용 X

```jsx
myTags.push('yujin');
myTags.splice('yujin');
```

- 내부 요소는 배열처럼 다루면서 배열 메소드 사용을 막고 싶거나 일반 배열에는 없는 특별한 메소드 제공을 원할 때 활용
1. `Array.isArray`(유사배열) = false

<img src="https://github.com/user-attachments/assets/78eccf04-e794-43ec-8e22-956cdfc58979" width="80%" height="80%">

- 배열과 비슷하지만 배열 X

※ 주의사항: 유사 배열은 다양하다!

- 특정 유사 배열의 경우 for …of 문 활용 X

### CSS 선택자로 태그 선택

```jsx
document.querySelector('#myNumber');
document.querySelectorAll('.color-btn'); // 해당 css 속성 가진 모든 태그 리턴
document.querySelectorAll('li'); // li 태그들이 모두 담긴 유사 배열 리턴
```

- querySelector는 여러 개의 클래스를 가진 요소들이 있어도 첫 요소만 선택
- querySelectorAll 메소드 활용 시 요소가 하나 밖에 없더라도 요소가 하나인 NodeList 반환
- **querySelector**: 존재하지 않는 요소를 선택 시 `null` 값 리턴
- **querySelectorAll**: 존재하지 않는 요소 선택 시 `undefined/null` 값이 아닌 비어있는 `NodeList` 리턴
- 장점
    - 메소드가 짧으면서 하나의 메소드로 유연하게 태그 선택 가능 → 활용도 높음
    - 다른 사람의 작성 코드 확인할 때를 대비해 `getElementsById/ClassName`도 알아두기

### Console.dir

```jsx
console.dir(123); // '123' 문자열
console.dir([1, 2, 3]); // Array(3)
console.dir({name: '전유진"}); // Object
console.dir(str, num, arr, obj, func); // '전유진'
console.dir(document.body); // Obj 형태
```

- `log` 메소드는 값 위주로 출력하는 반면, `dir` 메소드는 객체의 속성을 자세히 출력
- dir 메소드는 여러 값 전달 시 첫 값만 출력
- DOM 객체 다룰 때 `log` 메소드는 HTML 형태(태그)로 출력, `dir` 메소드는 객체 형태(`{ aLink: “” }`)로 출력

## 📌 기억해둘 것

### 요소 노드 프로퍼티

| **프로퍼티** | **내용** | **참고사항** |
| --- | --- | --- |
| **element.innerHTML** | 요소 노드 내부의 HTML코드 문자열로 리턴 | 요소 안의 정보를 확인할 수도 있지만,내부의 HTML 자체를 **수정**할 때 좀 더 자주 활용 |
| **element.outerHTML** | 요소 노드 자체의 전체적인 HTML 코드를 문자열로 리턴 | outerHTML은 새로운 값을 할당하면요소 자체가 **교체**되어 버리기 때문에 주의 |
| **element.textContent** | 요소 노드 내부의 내용들 중에서 HTML을 제외하고 텍스트만 리턴 | 말그대로 텍스트만 다루기 때문에HTML태그를 쓰더라도 모두 텍스트로 처리. 사용자의 입력 값을 웹페이지 **반영** 시 사용 |

```jsx
const myTag = document.querySelector('#list-1');

myTag.innerHTML += '<li>exotic</li>';
myTag.outerHTML = '<ul id="new-list"><li>Exotic</li></ul>';
myTag.textContent = '<li>new text!</li>';
```

### 요소 노드 다루기

1. 생성: `document.createElement('태그이름')`
2. 꾸미기: `element.textContent, element.innerHTML, ...`
3. 추가 혹은 이동: `element.prepend, element.append, element.after, element.before`
4. 삭제: `element.remove()`

### HTML 속성

```jsx
const div = tomorrow.firstElementChild;
console.log(div.className);

div.getAttribute('속성') // 속성 접근
div.setAttribute('속성', '값') // 속성 추가 or 수정
div.removeAttribute('속성') // 속성 제거
```

- HTML 태그의 class 속성은 **className**으로 생성
- 프로퍼티 이름으로 접근 시 className이지만 `getAttribute` 활용 시 **‘class’**를 직접 전달해주어야 함

### 스타일 다루기

```jsx
const today = document.querySelector('#today');
today.children[1].classList.add('done');
today.children[1].classList.remove('done');
today.children[1].classList.toggle('done');
today.children[1].className = 'done';
```

1. style 프로퍼티 활용하기: `element.style.styleName = 'value';`
2. class 변경을 통해 간접적으로 스타일 적용하기: `element.className`, `element.classList`
    - `className`: class 속성 값 통째로 변경
    - `classList`: class 속성 값 부분적 수정

| **메소드** | **내용** | **참고사항** |
| --- | --- | --- |
| **classList.add** | **클래스 추가하기** | **여러 개의 값을 전달하면 여러 클래스 추가 가능** |
| **classList.remove** | **클래스 삭제하기** | **여러 개의 값을 전달하면 여러 클래스 삭제 가능** |
| **classList.toggle** | **클래스 없으면 추가, 있으면 삭제하기** | **하나의 값만 적용 가능하고,두 번째 파라미터로 추가 또는 삭제 기능을 강제할 수 있음** |

### 비표준 속성

- 상황에 따라서 필요
- 활용 시 변화에 유동적이지 않은 `data-*` 형태 또는 `dataset` 프로퍼티 사용이 안전
