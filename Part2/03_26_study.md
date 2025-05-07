# 📝정리 내용

- 자바스크립트로 리퀘 보내기

## 💡 처음 알게 된 사실

### Children

- Props의 특별한 프로퍼티
- 컴포넌트를 단일 태그가 아닌 여는 태그와 닫는 태그 형태로 작성 시 그 안에 작성된 코드가 바로 이 `children` 값에 담김

```jsx
function Button({ children }) {
  return <button>{children}</button>;
}

export default Button;
```

```jsx
import Button from './Button';
import Dice from './Dice';

function App() {
  return (
    <div>
      <div>
        <Button>던지기</Button>
        <Button>처음부터</Button>
      </div>
      <Dice color="red" num={2} />
    </div>
  );
}

export default App;
```

- 장점
    - 더 직관적인 코드 작성 O
    - 텍스트 작성을 넘어 컴포넌트 내에 컴포넌트 작성 O
    - 컴포넌트 내에 복잡한 태그 작성 O

❓어떻게 활용할 수 있을지

## 📌 기억할 것

### Props

- 컴포넌트에 지정한 속성들
- 속성 지정 → 각 속성이 하나의 객체로 모여 함수의 첫 파라미터로 전달

```jsx
import Dice from './Dice';

function App() {
  return (
    <div>
      <Dice color="red" num={2} />
    </div>
  );
}

export default App;
```

```jsx
import diceBlue01 from './assets/dice-blue-1.svg';
import diceBlue02 from './assets/dice-blue-2.svg';
// ...
import diceRed01 from './assets/dice-red-1.svg';
import diceRed02 from './assets/dice-red-2.svg';
// ...

const DICE_IMAGES = {
  blue: [diceBlue01, diceBlue02],
  red: [diceRed01, diceRed02],
};

function Dice({ color = 'blue', num = 1 }) {
  const src = DICE_IMAGES[color][num - 1];
  const alt = `${color} ${num}`;
  return <img src={src} alt={alt} />;
}

export default Dice;

```