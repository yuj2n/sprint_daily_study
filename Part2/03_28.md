# 📝정리 내용

- React 웹 개발 시작하기

## 💡 처음 알게 된 사실

### 편리하게 클래스네임 쓰는 방법

1. 템플릿 문자열 사용
- 개수가 늘면 알아보기 힘듦!

```jsx
function Button({ isPending, color, size, invert, children }) {
  const classNames = `Button ${isPending ? 'pending' : ''} ${color} ${size} ${invert ? 'invert' : ''}`;
  return <button className={classNames}>{children}</button>;
}

export default Button;
```

1. 배열 사용
- 지저분하고 반복 코드 작성의 번거로움

```jsx
function Button({ isPending, color, size, invert, children }) {
  const classNames = [
    'Button',
    isPending ? 'pending' : '',
    color,
    size,
    invert ? 'invert' : '',
  ].join(' ');
  return <button className={classNames}>{children}</button>;
}

export default Button;
```

→ 라이브러리 사용 

### classnames 라이브러리

- 설치: `npm install classnames`

```jsx
import classNames from 'classnames';

function Button({ isPending, color, size, invert, children }) {
  return (
    <button
      className={classNames(
        'Button',
        isPending && 'pending',
        color,
        size,
        invert && 'invert',
      )}>
     { children }
   </button >
  );
}

export default Button;
```

### 빌드

![image.png](attachment:da14c686-6dfe-4ee0-9846-044ed6d3d012:image.png)

| 빌드 | 의미 | 예 |
| --- | --- | --- |
| Transpliling | 최신 문법(예: JSX, ES6+)을 구형 코드로 변환 | Babel (JSX → JavaScript 변환), TypeScript (TS → JS 변환) |
| Bundling | 여러 파일을 하나로 묶어서 최적화 | Webpack, Rollup, Parcel, Vite (파일 묶음 및 최적화) |

⇒ 웹 사이트에 보여짐!

## 📌 기억할 것

### 디자인 적용 방법

1. 이미지 불러오기

```jsx
import diceImg from './assets/dice.png';

function Dice() {
  return <img src={diceImg} alt="주사위 이미지" />;
}

export default App;
```

1. 인라인 스타일
- 카멜케이스/ ‘ ‘ 주의!!

```jsx
import diceImg from './assets/dice.png';

const style = {
  borderRadius: '50%',
  width: '120px',
  height: '120px',
};

function Dice() {
  return <img style={style} src={diceImg} alt="주사위 이미지" />;
}

export default App;
```

1. CSS 파일 불러오기(from X)

```jsx
import diceImg from './assets/dice.png';
import './Dice.css';

function Dice() {
  return <img src={diceImg} alt="주사위 이미지" />;
}

export default App;
```

1. 클래스네임 사용
- `className` prop을 부모 컴포넌트에서 받으면 재사용성 향상

```jsx
import diceImg from './assets/dice.png';
import './Dice.css';

function Dice({ className = '' }) {
  const classNames = `Dice ${className}`;
  return <img className={classNames} src={diceImg} alt="주사위 이미지" />;
}

export default App;
```

### 명령어 복습하기

**프로젝트 생성**

```
npm init react-app .
```

터미널에서 원하는 디렉토리에 들어가서 `npm init react-app .`를 입력하면 현재 디렉토리에 리액트 프로젝트를 생성합니다.

**개발 모드 실행**

```
npm start (npm run start)
```

터미널에서 `npm run start`를 입력하면 개발 모드 서버가 실행됩니다.

**실행 중인 서버 종료**

```
ctrl + c
```

서버가 실행 중인 터미널에서 `ctrl + c`를 입력하면 서버가 종료됩니다.

**개발된 프로젝트 빌드**

```
npm run build
```

터미널에서 `npm run build`를 입력하면 빌드를 시작합니다.

**빌드한 것 로컬에서 실행**

```
npx serve build
```

터미널에서 `npx serve build`를 입력하면 serve 프로그램을 다운 받고 build 폴더에서 서버가 실행됩니다.