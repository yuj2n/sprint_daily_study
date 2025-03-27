# 📝정리 내용

- React 웹 개발 시작하기

## 📌 기억할 것

### React 시작하기

- 프로젝트 생성: `npm create vite@latest . -- --template react`
- 필요 패키지 설치: `npm install`
- 실행: `npm run dev`
- 종료: `Ctrl + C`

### JSX

- JS 확장 문법
- 하나의 태그로 감싸기
    - <Fragment>또는 <> 추천!
- {}에는 JS 표현식만 사용 O, if문 또는 for문 함수 선언 X
- 📌**규칙**
    1. 속성명 Camel Case로 작성
    - onmousedown → onMouseDown
    1. JS 예약어와 같은 속성명 X
    - class → className
    - for → htmlFor

### JSX에서 JS

```jsx
const yujin = 'yujin';
const imageUrl = 'https://...';
function handleClick() {
	alert('곧 도착합니다!');
}

createRoot(document.getElementById('root')).render(
  <>
	<h1>{yujin}</h1>
	<img src={imageUrl} alt="pic" />
	<button onClick={handleClick}>확인</button>
</>
);
```

### 컴포넌트

- ( )로 감싸면 여러 줄에 나눠서 작성 O

```jsx
import Dice from "./Dice";

function App() {
    return (
        <div>
            <Dice />
        </div>
    );
}

export default App;
```

### 리액트 앨리먼트

- 리액트가 객체 형태의 값을 해석

```jsx
import ReactDOM from 'react-dom';

const element = <h1>안녕 리액트!</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### 리액트 컴포넌트

- 리액트 앨리먼트를 더 자유롭게 다루는 문법
- 장점
    - 함수 이름을 통해 하나의 태그처럼 활용
    - 모듈 문법으로 활용 시 더 독립적으로 컴포넌트 특성에 집중해 코드 작성 O
- ex) 함수

```jsx
import ReactDOM from 'react-dom';

function Hello() {
  return <h1>안녕 리액트</h1>;
}

const element = (
  <>
    <Hello />
    <Hello />
  </>
);

ReactDOM.render(element, document.getElementById('root'))
```

- ex2

```jsx
import diceBlue01 from './assets/dice-blue-1.svg';
// Dice.js
function Dice() {
  return <img src={diceBlue01} alt="주사위" />;
}

export default Dice;
```

```jsx
import **D**ice from './Dice';
// App.js
function App() {
  return (
    <div>
      <Dice />
    </div>
  );
}

export default App;
```

**✨**주의: ****첫 글자 **대문자**